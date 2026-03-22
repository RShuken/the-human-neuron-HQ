# The Human Neuron: Technical Deep Dive Research

*Compiled: 2026-03-19*

---

## 1. Real-Time Multi-User Phone Systems

### How Kahoot/AhaSlides/Mentimeter Work Under the Hood

These platforms all use a **host-participant WebSocket architecture**:

- **Host** creates a session, gets a room code/QR code
- **Participants** connect via browser (no app install), join the room
- **Communication** is primarily WebSocket-based pub/sub messaging
- **State** is managed server-side; clients receive state updates via broadcast

**Kahoot specifically** uses a WebSocket connection established through a Session class that handles authentication and creates adapters for real-time communication. Its Player adapter communicates via WebSocket for bidirectional data flow.

**Capacity benchmarks (real-world):**
- Kahoot: Claims 2,000 participants on paid plans, but users report severe lag/crashes above 500
- Mentimeter: Supports up to 5,000 participants reliably
- AhaSlides: Markets to large groups, real-time word clouds and polls
- Crowdpurr: Specifically designed for mobile-driven interactive live event experiences

### Realtime Framework Comparison for The Human Neuron

#### Option A: Ably (RECOMMENDED for production)
- **Free tier**: 200 concurrent connections, 200 channels, 6M messages/month, 500 msg/sec -- **perfectly fits our 50-200 user target at zero cost**
- **Paid**: $29/month Standard (10K connections), $399/month Pro (50K connections)
- Serves more WebSocket connections than any other pub/sub platform globally
- Auto-scales across multiple global regions without configuration
- Guaranteed message delivery, ordering, history, and state recovery
- Presence tracking built-in (know who's online/offline)
- Sub-250ms latency target
- Channel-based architecture: `host-admin-ch`, `game-ch`, `player-[id]-ch`
- **Verdict**: Free tier covers our exact use case. Battle-tested at massive scale. Best reliability guarantees.

#### Option B: Supabase Realtime (STRONG CONTENDER -- already in your stack)
- **Free tier**: 200 peak connections, 2M messages/month
- **Pro tier ($25/mo)**: 500 peak connections, 5M messages/month
- Three modes: **Broadcast** (ephemeral client-to-client), **Presence** (shared state sync), **Postgres Changes** (DB listeners)
- Default limit: 200 concurrent users per channel, 100 channels per tenant
- Broadcast mode is ideal for our use case -- low-latency ephemeral messaging
- Presence mode gives us who's connected and their state for free
- **Verdict**: Already in your stack (Cora uses Supabase). Free tier exactly covers 200 users. Broadcast + Presence is the perfect combo for this project.

#### Option C: PartyKit / Cloudflare Durable Objects (BEST DX, edge-native)
- Now owned by Cloudflare (acquired Oct 2025)
- Each "party" (room) runs in a Durable Object on the edge -- server logic runs close to users
- Deploy to your own Cloudflare account for free, pay only for resources
- **Free tier (Workers Free)**: 100K requests/day, WebSocket messages billed at 20:1 ratio (100 WS messages = 5 requests)
- Works with Y.js, Automerge, tldraw, XState
- JavaScript/TypeScript server logic, familiar DX
- **Verdict**: Best developer experience. Edge-native = lowest latency. Free tier is generous for event use. Newer ecosystem, smaller community.

#### Option D: Socket.IO (self-hosted, full control)
- A chat room with 200 people sending 1 msg/sec uses ~2% server capacity
- Rooms/namespaces for logical grouping
- Must self-host (Node.js server on Fly.io, Railway, etc.)
- Scaling beyond one server requires Redis adapter
- **Verdict**: Works great for 200 users on a single server. More ops overhead. Full control over everything.

#### Option E: Firebase Realtime Database
- Best offline persistence -- auto-syncs when connectivity returns
- Well-documented, large ecosystem
- Can be expensive at scale
- **Verdict**: Overkill for this use case. Better for apps needing offline-first persistence.

### Recommended Architecture

```
[QR Code] -> [Phone Browser]
                  |
            [WebSocket Connection]
                  |
         [Realtime Service (Ably/Supabase/PartyKit)]
                  |
          [Game Server (Node.js)]
                  |
         [Big Screen Display Client]
```

**Primary recommendation: Supabase Realtime** (already in stack, free tier fits, Broadcast + Presence is purpose-built for this) **or PartyKit** (if you want edge performance and modern DX).

---

## 2. Neural Network Visualization

### Library Recommendations (Ranked)

#### Tier 1: Best Fit for The Human Neuron

**1. Pixi.js + D3-force (RECOMMENDED for 2D)**
- Pixi.js uses WebGL for hardware-accelerated 2D rendering
- D3's force-layout algorithms handle node positioning and physics
- Hybrid approach: D3 computes layout, Pixi.js renders to GPU
- Handles 10,000+ animated particles at 60fps (our 200 nodes is trivial)
- SVG-based D3 starts lagging at ~1,000 nodes; Pixi.js eliminates this entirely
- Mature ecosystem, well-documented hybrid pattern
- **Best for**: Beautiful 2D network with animated signal propagation, glow effects, particle trails

**2. React Three Fiber + Three.js (RECOMMENDED for 3D "wow factor")**
- React wrapper for Three.js -- declarative 3D scenes
- Proven for neural network visualization specifically
- Instanced meshes for hundreds of nodes (one draw call for all nodes)
- UnrealBloomPass for sci-fi glow effects on active neurons
- requestAnimationFrame for smooth 60fps signal propagation animation
- Node brightness = activation energy; colors from real data
- **Best for**: Immersive 3D "big screen" experience, cinematic quality

**3. Canvas 2D + Custom Rendering (SIMPLEST)**
- Raw HTML5 Canvas with requestAnimationFrame
- Full control, no library overhead
- Animated bezier curves for connections, circles for neurons
- Glow effects via canvas shadows and compositing
- **Best for**: Fastest to prototype, lightest weight, easy to customize

#### Tier 2: Existing Frameworks to Learn From

**TensorFlow Playground** (https://playground.tensorflow.org/)
- Built with TypeScript + D3.js
- The gold standard for interactive neural network education in browser
- Open source on GitHub: github.com/tensorflow/playground
- Shows real-time training, weight visualization, decision boundaries
- **Lesson for us**: Proves D3.js is sufficient for educational NN visualization

**TensorSpace.js** (https://tensorspace.org/)
- 3D neural network visualization framework
- Built on TensorFlow.js + Three.js + Tween.js
- Keras-like API to build layers, load models, generate 3D viz
- Interactive: click, drag, scroll, expand layers
- Works on mobile browsers
- **Lesson for us**: Shows how to make 3D NN viz that works on phones

**Adam Harley's NN Visualization** (https://adamharley.com/nn_vis/)
- Interactive visualization of CNN behavior with user-drawn input
- Users draw digits, watch activations propagate through layers in real-time
- Built with WebGL + custom JavaScript
- 4 visualization modes: 3D/2D x fully-connected/convolutional
- **Lesson for us**: The "draw and watch it propagate" model is exactly our interaction pattern

**NNStudio** (github.com/zuck30/NNStudio)
- Interactive 3D NN visualization with TensorFlow.js + Three.js + React
- Good reference implementation

#### Visualization Design Recommendations

For the big-screen display, the visualization needs:
1. **200 nodes** arranged in layers (input -> hidden -> output)
2. **Animated connections** showing signal flow (glowing pulses traveling along edges)
3. **Node activation states** (color/size/glow intensity based on participant input)
4. **Real-time updates** as participants interact on their phones
5. **Emergent patterns** visible -- pathways that strengthen over time get brighter/thicker

**Recommended stack for big screen**: React Three Fiber + Three.js with UnrealBloomPass for the "wow factor" 3D visualization. Pixi.js + D3-force as a fallback if 3D proves too complex.

**For phone UI**: Simple Canvas 2D or even just styled HTML/CSS showing the participant's individual neuron state, incoming signals, and activation threshold slider.

---

## 3. Existing "Human Neural Network" Exercises and Games

### Direct Precedents Found

#### The Human Neural Network Game (Oak Ridge National Laboratory)
- **Created by**: Catherine Schuman, Steven Young, Thomas Proffen, and Dasha Herrmannova
- **Context**: Developed for the TechGirlz program at Oak Ridge National Laboratory
- **Concept**: Students physically role-play as components of a neural network
- **Key mechanic**: Demonstrates weighted input summation and threshold activation -- each student-neuron receives signals, analyzes them, and makes a decision
- Catherine Schuman is a neuromorphic computing researcher at ORNL focused on teaching computers to learn like brains
- **Status**: This is the closest known precedent, but it's a physical card-based activity, not a phone-connected real-time system

#### The Neural Network Game (Project GUTS / Everyday AI)
- **Created by**: Irene Lee for Project GUTS (2019), building on the Oak Ridge game
- **Augmentation**: Added evaluation and backpropagation rounds
- **Activity flow**: Students choose 4 words to describe an image, feed them forward through the network, evaluate results, adjust input weights (backpropagation)
- **Materials**: 34 colored notecards, colored paper pieces (26 yellow, 8 green, 2 pink), pencils
- **Class structure**: Groups of ~9 students across 2 games
- **Covers**: Feedforward, evaluation, and backpropagation vocabulary
- URL: https://everyday-ai.org/resources/neural-network-game-activity
- **Status**: Paper-based classroom activity. Proves the pedagogical concept works. No digital/phone component.

#### Tangible Interactive Games for AI Education (2025 Paper)
- **Source**: arXiv:2506.00651v1 -- academic paper on tangible games for AI learning in elementary education
- Proposed activities include "Classroom Neural Network (CNN)" simulating neuron interactions
- Students role-play different NN components
- Demonstrates weighted input summation and threshold activation
- Emphasizes hands-on physical materials and social collaboration enhance understanding
- **Status**: Academic validation that embodied NN learning works

#### Embodied Neural Communication Demonstration (Nature, 2020)
- **Source**: Nature npj Science of Learning (PMC7718869)
- Classroom demonstration introducing students to neural communication through embodied learning
- Published peer-reviewed evidence that physically acting out neural processes improves conceptual understanding
- **Status**: Scientific backing for the approach

#### TensorFlow Playground
- Not a crowd game, but the most successful educational NN visualization
- Proves that interactive, visual, no-code NN learning is incredibly effective
- 1:2:1 default architecture, real-time training visualization
- **Lesson**: Our "big screen" should feel as intuitive as TF Playground

### What Makes The Human Neuron Different From All of These

**None of these precedents combine all three elements:**
1. Digital/phone-connected (not paper cards)
2. Real-time synchronized across 50-200 people simultaneously
3. Projected visualization showing the collective network behavior

The Oak Ridge game and Everyday AI activity are paper-based small-group exercises. TF Playground is single-user digital. The Human Neuron is genuinely novel in combining crowd-scale, phone-connected, real-time neural network simulation.

---

## 4. QR Code to Web Session Architecture

### Recommended Flow

```
[Projected QR Code]
    -> Phone camera scans
    -> Opens browser to: neuron.app/join?session=ABC123
    -> Server assigns anonymous identity (UUID)
    -> Sets cookie: { neuronId: "uuid-xxx", sessionId: "ABC123" }
    -> WebSocket connects to realtime service
    -> Participant appears on big screen as a neuron
```

### Session Management Best Practices

**Anonymous/No-Auth Pattern:**
- Generate UUID on first visit, store in `localStorage` + cookie
- Pre-authentication cookie tracks anonymous users (OWASP pattern)
- Cookie includes session ID + timestamp for replay attack prevention
- On reconnection, check localStorage for existing neuronId, rejoin same position in network

**Cookie + localStorage Dual Storage:**
```javascript
// On first visit
const neuronId = localStorage.getItem('neuronId') || crypto.randomUUID();
localStorage.setItem('neuronId', neuronId);
document.cookie = `neuronId=${neuronId}; path=/; max-age=86400; SameSite=Strict`;
```

**Reconnection Logic:**
1. Phone screen locks -> WebSocket disconnects
2. User unlocks phone -> page is still loaded in browser
3. JavaScript detects `navigator.onLine` and `visibilitychange` events
4. Automatically reconnects WebSocket with stored neuronId
5. Server re-associates connection with same neuron position
6. Supabase Realtime and Ably both have built-in reconnection with state recovery

**QR Code Generation:**
- Use `qrcode` npm package or `qr-code-styling` for branded QR codes
- QR encodes URL: `https://yourdomain.com/join?s=SESSION_CODE`
- Short session codes (6 chars) for manual entry fallback
- Display QR code prominently on big screen with join URL text below it

### PWA Considerations

For a conference session (45-60 min), a full PWA is overkill. Instead:
- **Service Worker**: Register one for offline fallback page ("reconnecting...")
- **Manifest**: Add basic web app manifest so the browser bar shows nicely
- **Viewport meta**: Lock orientation, disable zoom, set theme color
- **No install prompt**: Keep it web-only, zero friction
- **Wake Lock API**: Prevent phone screen from sleeping during session (`navigator.wakeLock.request('screen')`)

---

## 5. Similar Interactive Art/Tech Installations

### Directly Relevant Precedents

#### Marshmallow Laser Feast -- "Dream" (2021)
- Shakespeare's A Midsummer Night's Dream reimagined as a live digital performance
- **Audiences directly influenced the live performance from their phone, desktop, or tablet** via the Dream website
- Reached 65,000 people online over 10 live performances in 8 days
- Collaboration with Royal Shakespeare Company
- **Relevance**: Proves phone-to-projected-experience at massive scale works. Audiences shaping a live performance from personal devices is exactly our model.

#### Marshmallow Laser Feast -- "A Colossal Wave!" (SXSW)
- Large-scale interactive installation accepted into SXSW Art Program
- One participant drops a bowling ball from three stories; others "sing to populate an aquatic world with voice fruit"
- VR umbrella at epicenter, mixed reality for surrounding participants
- **Relevance**: Multi-participant collective experience where individual actions create emergent group results

#### Emerge Agency -- Crowd-Sourced Phone Display
- Transformed 20,000+ iPhone and Android screens into a single crowd-sourced display
- Combined audience phones in a venue to create a massive pixel array (500px x 50px resolution for 500-seat x 50-row venue)
- Each phone screen becomes one "pixel" in a venue-wide animation
- **Relevance**: Directly demonstrates phone-as-display-unit in a crowd. Our model is phone-as-neuron rather than phone-as-pixel, but the technical connectivity pattern is identical.

#### Crowdr
- Creates interactive synchronized experiences of sounds and lights for concerts, festivals, corporate events
- Unique algorithm transfers data to mobile devices by sound (audio watermarking)
- No WiFi dependency -- uses audio for synchronization
- **Relevance**: Interesting alternative sync mechanism. Could be a fallback if WiFi is congested.

#### teamLab (Borderless, Planets, etc.)
- Japanese art collective creating immersive digital installations
- Uses sensors (motion, touch, shadow) for real-time audience interaction
- Installations respond to physical presence and movement -- flowers bloom, butterflies appear
- "The existence of others inherently shapes the experience"
- teamLab Borderless: world's first truly boundary-free digital art museum
- **Relevance**: Gold standard for collective immersive experiences. Our digital-only (phone) input is lighter-weight than their sensor arrays but aims for the same feeling of collective emergence.

#### Moment Factory
- Montreal-based studio creating immersive multimedia environments
- Expanding into permanent and touring experiences globally
- Projection mapping + interactive elements
- **Relevance**: Production quality benchmark for projected experiences

### Key Design Lessons From These Installations

1. **Individual agency must feel real**: When groups exceed ~25, individuals lose sense of their personal impact. Design feedback so each person can see THEIR neuron's contribution.
2. **Emergence is the magic**: The moment the crowd realizes they're collectively producing something none of them could alone -- that's the peak experience.
3. **Phone as input, projection as output**: This split (personal device for control, shared screen for collective result) is a proven pattern.
4. **Low latency is non-negotiable**: Delays between phone input and screen response destroy the feeling of agency.
5. **Audio feedback amplifies impact**: Consider sound design -- when your neuron fires, subtle audio cues reinforce the connection.

---

## 6. Scalability for 50-200 Concurrent Users

### WebSocket/Realtime Capacity

**The good news: 200 users is a small-scale problem.**

- Socket.IO: 200 users sending 1 msg/sec = ~2% server capacity. Trivial.
- Ably free tier: 200 concurrent connections included. Exactly our ceiling.
- Supabase free tier: 200 peak connections included. Exactly our ceiling.
- PartyKit/Cloudflare: 100K requests/day free. With 20:1 WebSocket billing ratio, that's effectively 2M WebSocket messages/day free.
- A single Node.js server can handle thousands of WebSocket connections

**Message volume estimate for a 60-minute session:**
- 200 users, each sending ~1 action every 5 seconds = 40 messages/sec inbound
- Server broadcasts state updates ~10x/sec to all = 2,000 messages/sec outbound
- Total: ~2,040 msg/sec sustained, ~7.3M messages per hour
- Ably free tier (500 msg/sec) may be tight; Supabase (2M/month) would be exceeded in one session
- **Recommendation**: Design message protocol to be efficient. Batch updates. Send deltas, not full state. Or use PartyKit where the room logic runs on the edge and you only pay for compute, not messages.

### WiFi: The Real Bottleneck

**Conference WiFi is the #1 risk factor.** The realtime server is never the problem; the local network is.

#### The Problem
- Conference venues share WiFi across all attendees (potentially thousands)
- Typical venue WiFi: 50-100 devices per access point
- With 200 phones + attendees' other devices, you could saturate available APs
- WiFi congestion causes: connection drops, high latency, failed reconnects

#### Mitigation Strategies

**Strategy 1: Bring Your Own Network (RECOMMENDED)**
- Rent a portable event WiFi kit ($200-500/day)
- **Fello Hardware**: Cradle routers supporting 200 devices on Verizon 4G LTE, mesh capability for up to 2,000 devices
- **Trade Show Internet**: 5G Mega Internet Kit supports up to 300 devices
- **Made By WiFi**: Bonded cellular + enterprise APs
- Plug-and-play setup in under 5 minutes
- Dedicated bandwidth, no sharing with venue network
- Display your own SSID on the big screen: "Connect to: HumanNeuron-WiFi"

**Strategy 2: Coordinate with BSW Venue**
- Request a venue with enterprise-grade WiFi
- Ask for a dedicated VLAN or SSID for your session
- Modern WiFi 6 APs handle 200 clients per radio; WiFi 6E handles 400
- Best practice: keep client count below 50% of AP max capacity
- Request APs placed overhead for line-of-sight in the session room

**Strategy 3: Minimize Bandwidth Per Client**
- Our app is tiny: initial page load ~100-500KB
- WebSocket messages are small: ~50-200 bytes each
- No video, no large images, no streaming
- Design for 2G-level bandwidth tolerance
- Cache everything possible with Service Worker
- Pre-load all assets on initial page load before the session starts

**Strategy 4: Hybrid Connectivity Fallback**
- Allow participants on cellular data (5G/LTE) as fallback
- Many phones will have strong cellular signal even if WiFi is congested
- Display both WiFi SSID and a "Use your cell data" option
- WebSocket connections work identically over cellular

#### WiFi Architecture Best Practices
- Prioritize 5 GHz band (more non-overlapping channels, less interference)
- Limit channel width to 20 MHz in high-density areas
- Use wired Ethernet backhaul for access points (never wireless mesh)
- Network segmentation: dedicated network for session participants
- Monitor: latency p50/p95/p99, connection count, drop rate

### Hosting Infrastructure

For a single-event use case (BSW), keep it simple:

**Option A: Serverless + Managed Realtime (RECOMMENDED)**
- Frontend: Vercel or Netlify (static site hosting, free tier)
- Realtime: Supabase Realtime or PartyKit (free tier)
- No server to manage, auto-scales, zero ops
- Total cost: $0

**Option B: Single Server**
- Fly.io or Railway: Node.js server with Socket.IO
- $5-10/month, or free tier
- Single server is more than enough for 200 users
- Deploy game logic and WebSocket server together

**Option C: Edge-Native**
- PartyKit on Cloudflare Workers
- Game room runs in a Durable Object at the edge
- Lowest possible latency, auto-scales globally
- Free tier covers event use

---

## Technical Recommendations Summary

### Recommended Tech Stack

| Component | Primary Pick | Backup Pick |
|-----------|-------------|-------------|
| **Realtime** | Supabase Realtime (Broadcast + Presence) | PartyKit (Cloudflare) |
| **Frontend Framework** | Next.js or SvelteKit | Vanilla JS + Vite |
| **Big Screen Viz** | React Three Fiber + Three.js | Pixi.js + D3-force |
| **Phone UI** | Simple HTML/CSS/Canvas | React with minimal deps |
| **Hosting** | Vercel (frontend) + Supabase (realtime) | Cloudflare Pages + PartyKit |
| **QR Code** | `qr-code-styling` npm package | Any QR library |
| **WiFi** | Portable event WiFi kit (Fello/TSI) | Venue WiFi + cellular fallback |

### Key Architectural Decisions

1. **Supabase Realtime is the path of least resistance** -- you already use Supabase for Cora, the free tier covers 200 connections, and Broadcast + Presence are purpose-built for this exact use case.

2. **React Three Fiber for the big screen** -- the 3D "wow factor" of watching a neural network light up is worth the investment. Instanced meshes handle 200 nodes easily. Bloom/glow effects make it cinematic.

3. **Bring your own WiFi** -- this is non-negotiable for a reliable experience. A $200-500 rental eliminates the #1 failure mode. BSW venue WiFi is shared across 5,000 attendees.

4. **Anonymous sessions with localStorage** -- zero friction entry. QR scan -> browser opens -> UUID assigned -> cookie set -> WebSocket connects -> you're a neuron. Under 3 seconds from scan to participation.

5. **Message efficiency** -- design the protocol so each participant sends minimal data (their activation state, ~50 bytes) and the server computes/broadcasts the network state. Batch broadcasts at 10-20fps to the big screen.

---

## Sources

### Real-Time Systems
- [Ably: Multiplayer Quiz App Architecture](https://ably.com/topic/multiplayer-quiz-app-architecture)
- [Ably: Pricing](https://ably.com/pricing)
- [Ably: Scaling WebSockets](https://ably.com/topic/the-challenge-of-scaling-websockets)
- [Ably: Socket.IO vs Supabase Realtime (2026)](https://ably.com/compare/socketio-vs-supabase)
- [Ably: Firebase vs Socket.IO (2026)](https://ably.com/compare/firebase-vs-socketio)
- [Ably: Pusher vs Socket.IO (2026)](https://ably.com/compare/pusher-vs-socketio)
- [Supabase Realtime: Pricing](https://supabase.com/docs/guides/realtime/pricing)
- [Supabase Realtime: Limits](https://supabase.com/docs/guides/realtime/limits)
- [Supabase Realtime: Broadcast](https://supabase.com/docs/guides/realtime/broadcast)
- [Supabase Realtime: Architecture](https://supabase.com/docs/guides/realtime/architecture)
- [PartyKit Documentation](https://docs.partykit.io/)
- [PartyKit: Building Real-Time Collaborative Apps in 2026](https://latestfromtechguy.com/article/partykit-realtime-collaboration-2026)
- [Cloudflare acquires PartyKit](https://blog.cloudflare.com/cloudflare-acquires-partykit/)
- [Cloudflare Durable Objects Pricing](https://developers.cloudflare.com/durable-objects/platform/pricing/)
- [Socket.IO Performance Tuning](https://socket.io/docs/v4/performance-tuning/)
- [Benchmarking Socket.IO Servers](https://sahaj.dev/blog/socketio-benchmark)
- [Kahoot API Architecture (DeepWiki)](https://deepwiki.com/idiidk/kahoot-api/2-core-architecture)
- [WebSockets at Scale (WebSocket.org)](https://websocket.org/guides/websockets-at-scale/)
- [PubNub: Concurrent Connections at Scale](https://www.pubnub.com/blog/users-and-concurrent-connections-scale/)

### Neural Network Visualization
- [TensorFlow Playground](https://playground.tensorflow.org/)
- [TensorFlow Playground GitHub](https://github.com/tensorflow/playground)
- [TensorSpace.js](https://tensorspace.org/)
- [TensorSpace GitHub](https://github.com/tensorspace-team/tensorspace)
- [Building a Real-Time Neural Network Visualizer with React Three Fiber](https://www.erikjs.com/blog/building-neural-network-visualizer)
- [Adam Harley's Interactive NN Visualization](https://adamharley.com/nn_vis/)
- [NNStudio (Three.js + TF.js + React)](https://github.com/zuck30/NNStudio)
- [Visualizing Neural Networks in 3D](https://arogozhnikov.github.io/3d_nn/)
- [D3.js + Pixi.js Performance Comparison](https://blog.octo.com/d3-js-transitions-killed-my-cpu-a-d3-js-pixi-js-comparison)
- [Scale Up D3 Graph with Pixi.js](https://graphaware.com/blog/scale-up-your-d3-graph-visualisation-webgl-canvas-with-pixi-js/)
- [React Three Fiber Neural Network Tutorial](https://sbcode.net/react-three-fiber/neural-network/)
- [Neural Network Visualization (animated SVG)](https://codepen.io/hariharans1995/details/MWVPXgr)
- [Rendering 1M Datapoints with D3 and WebGL](https://blog.scottlogic.com/2020/05/01/rendering-one-million-points-with-d3.html)
- [Comparison of JS Graph Visualization Libraries](https://www.cylynx.io/blog/a-comparison-of-javascript-graph-network-visualisation-libraries/)

### Human Neural Network Exercises
- [Everyday AI: Neural Networks Lesson](https://everyday-ai.org/resources/12-neural-networks-lesson)
- [Everyday AI: Neural Network Game Activity](https://everyday-ai.org/resources/neural-network-game-activity)
- [Embodied Neural Communication Classroom Demo (Nature)](https://www.nature.com/articles/s41539-020-00077-1)
- [Tangible Interactive Games for AI Education (arXiv 2025)](https://arxiv.org/html/2506.00651v1)
- [Traversing the Pass: Serious Game Teaching Neural Networks (Uni Wuerzburg)](https://hci.uni-wuerzburg.de/topics/20220119-mlgame-krop/)
- [Catherine Schuman -- ORNL Neuromorphic Computing](https://www.ornl.gov/blog/catherine-schuman-teaching-neuromorphic-computers-learn)
- [Google's Understanding NN with TF Playground](https://cloud.google.com/blog/products/ai-machine-learning/understanding-neural-networks-with-tensorflow-playground)

### QR Code / Session Architecture
- [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)
- [QR Code Authentication Implementation (OwnID)](https://www.ownid.com/blog/how-to-implement-qr-code-authentication-a-walkthrough)
- [PWA Guide 2025 (Codebrand)](https://www.codebrand.us/blog/progressive-web-apps-pwa-guide-2025/)
- [Architect's Guide to PWAs (Ionic)](https://ionic.io/resources/articles/architects-guide-to-progressive-web-apps)

### Interactive Installations
- [Marshmallow Laser Feast: Dream](https://marshmallowlaserfeast.com/project/dream/)
- [Marshmallow Laser Feast Overview (Factory International)](https://factoryinternational.org/factoryplus/an-introduction-to-marshmallow-laser-feast/)
- [teamLab Borderless](https://www.teamlab.art/e/living_digital_space/)
- [Emerge Agency: Crowd-Sourced Phone Display](https://www.emergeagency.com/work/detail/transforming-mobile-phones-into-a-crowd-sourced-interactive-display/)
- [Crowdr: Interactive Synchronized Experience](https://crowdr.app/)
- [PubNub: Stimulus for Crowd Participation](https://www.pubnub.com/blog/realtime-tech-the-stimulus-for-interactive-crowd-participation-apps/)
- [Second Screen Engagement of Event Spectators (Wiley)](https://onlinelibrary.wiley.com/doi/10.1155/2018/3845123)
- [Large-Scale Audience Participation in Live Music via Smartphones](https://www.tandfonline.com/doi/full/10.1080/09298215.2020.1722181)
- [Multi-User Interactive Art Methodologies (Interactive Architecture Lab)](https://www.interactivearchitecture.org/methodologies-and-reasons-for-exploring-meaningful-group-experience-through-multi-user-interactive-art.html)
- [Moment Factory Growth (blooloop)](https://blooloop.com/technology/in-depth/moment-factory-growth-plan/)

### WiFi / Infrastructure
- [Event WiFi Best Practices (Planning Pod)](https://blog.planningpod.com/2015/03/25/event-wifi-how-to-get-it-right/)
- [Fello Event WiFi Rentals](https://fello.com/event-wifi)
- [Trade Show Internet: 5G Mega Kit](https://tradeshowinternet.com/services/5g-mega-internet-kit)
- [Cisco: Wireless for Large Public Networks Design Guide](https://www.cisco.com/c/en/us/support/docs/wireless/catalyst-9800-series-wireless-controllers/222000-design-guide-cx-wireless-for-large-pub.html)
- [Event Network Requirements (Nomadix)](https://nomadix.com/qa-event-network-requirements/)
- [WiFi for a 100-Person Conference](https://ma.juii.net/blog/wifi-for-a-conference)
