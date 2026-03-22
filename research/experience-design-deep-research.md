# The Human Neuron: Experience Design Deep Research

## 1. Mapping Neural Network Concepts to Human Actions

### What Does It FEEL Like to Be a Neuron?

The core experiential insight: a single neuron is profoundly simple but collectively powerful. Each participant should feel that their individual decision ("do I fire or not?") is trivial, but watching the network produce intelligent output from those trivial decisions is the revelatory moment.

#### Receiving Weighted Inputs from Neighbors

**The Human Experience:** Each participant receives signals from specific other participants — but not all signals are equal. Some connections are "strong" (the signal counts for a lot) and some are "weak" (easy to ignore). On a phone, this could appear as: "Player 7 sent you signal strength 3. Player 12 sent you signal strength 1. Player 15 sent you signal strength 5."

**Design Recommendation:** Use a simple numerical display. Participants see incoming signals as colored bars or numbers. The key felt experience is: "I have to add these up and decide if the total is enough." This mirrors the biological reality — a neuron sums its dendritic inputs weighted by synaptic strength.

**Analogy that works:** You're at a meeting where multiple people are advocating for a decision. Some people's opinions carry more weight (your boss vs. a stranger). You have to weigh all the input and decide whether to act.

#### Activation Functions (Threshold Decisions)

**The Human Experience:** Each neuron-participant has a personal threshold number displayed on their phone. They sum their weighted inputs. If the sum exceeds their threshold, they fire. If not, they stay silent.

**Why this works experientially:** The binary step function — the simplest activation function — maps perfectly to a human yes/no decision. Research confirms that "the binary step function uses a threshold value to determine whether or not a neuron should be activated" (Roboflow). Participants physically experience the tension of being right at threshold — "I'm at 6.5 and my threshold is 7... do I fire?" (In the strict version, no. But this creates the felt sense of what ReLU and sigmoid functions do.)

**Design Recommendation:** Start rounds with a simple binary threshold (fire/don't fire). In later rounds, introduce a "confidence" slider (0-1) to simulate sigmoid activation — how strongly they fire, not just whether they fire. This teaches that real neural networks don't just use on/off switches.

#### Forward Propagation

**The Human Experience:** The room is physically or virtually divided into layers. Layer 1 receives the initial input (e.g., an image, a word). They make their fire/don't-fire decisions. Their outputs become inputs for Layer 2. Layer 2 does the same, feeding Layer 3. The final layer produces the network's "answer."

**Key felt experience:** Watching the signal cascade through the room in real time. Participants in later layers are waiting, watching the visualization, seeing which neurons in the previous layer fired, then getting their own inputs and making their own decisions. This creates genuine suspense and a visceral sense of wave-like propagation.

**Design Recommendation:** Use a 3-second timer per layer to create visible propagation waves on the main screen. The audience sees the network "think" in real time, layer by layer.

**Analogy:** The telephone game — but structured, weighted, and with thresholds. Unlike telephone (which demonstrates lossy transmission), the neural network version demonstrates transformation and abstraction at each layer.

#### Backpropagation (Learning from Errors)

**The Human Experience:** The network produces an answer. The facilitator reveals the correct answer. The error is calculated. Now: the error signal flows BACKWARD through the network. Each participant sees a message: "The network was wrong. Your contribution to the error was X. Your connection weights are being adjusted."

**Why this is the hardest concept to embody — and the most important:** Backpropagation is "something deeply human: the art of learning from mistakes" (Medium). The analogy that works best: "It's like playing an instrument. When you make a mistake, you don't just know something went wrong. You retrace your steps to find what and where it happened. Maybe your timing was off, or your fingers were in the wrong place. That feedback helps you improve."

**Design Recommendation:** After a wrong answer, show each participant how their firing decision contributed to the error. Then show them their new adjusted weights for the next round. They'll see that the connections that led to the wrong answer got weaker, and the ones that would have led to the right answer got stronger. Over 3-5 rounds, participants viscerally experience how the network learns — not through any single neuron getting smarter, but through the collective adjustment of connection strengths.

#### Token Prediction / Next-Token Generation

**The Human Experience:** Present the network with a partial sentence: "The cat sat on the ___." The final layer neurons each represent a possible next word. The one that fires strongest is the network's prediction.

**Research insight:** Researchers created a "top-1 token prediction game" where human participants tried to guess the next token, achieving only 29% accuracy vs. language models (Buck et al., 2022). This demonstrates both how the task works and how superhuman LLMs have become at it. The activity of trying to predict the next token yourself, then seeing how the network does it through distributed computation, is a powerful "aha" moment.

**Design Recommendation:** Run 2-3 rounds of collective next-token prediction. The first round will likely fail. After backpropagation adjustments, the second round should be closer. By the third round, the audience experiences the network converging on a correct prediction — the "learning" moment.

#### Attention Mechanisms

**The Human Experience:** Instead of fixed connections, each neuron-participant gets to dynamically choose which other neurons to pay attention to for each specific input. The IBM definition captures it well: "an attention mechanism directs deep learning models to prioritize the most relevant parts of input data... inspired by the ability of humans to selectively pay more attention to salient details."

**Design Recommendation:** In an advanced round, give participants a "spotlight" mechanic. They see all available signals but choose which 2-3 to attend to most strongly. The visualization on the main screen shows attention patterns forming in real time — bright lines where neurons are attending to each other, dim lines where they're not. This teaches self-attention without using the term.

**Analogy:** "You're in a crowded room. Someone says your name — you immediately attend to that signal over all the background noise. Attention mechanisms do the same thing, but learned through data."

#### Weight Strengthening Through Repeated Use (Hebbian Learning)

**The Human Experience:** Over multiple rounds, participants watch their connection weights change. Connections that repeatedly contribute to correct answers get stronger (higher weight numbers, brighter visual lines). Connections that contribute to errors get weaker.

**The Hebb Rule made human:** "Neurons that fire together, wire together" (Hebb, 1949). When two connected participants consistently fire in the same round and the network gets the right answer, their shared connection visibly strengthens. This is long-term potentiation (LTP) made tangible.

**Design Recommendation:** Show a "relationship strength" metric between connected participants. After each round, highlight which connections got stronger and which got weaker. By the end of the session, the network has a clearly visible structure of strong and weak pathways — an emergent topology that nobody designed, that arose purely from learning.

---

## 2. Game Design for Educational Experiences

### James Paul Gee's Learning Principles (Applied to The Human Neuron)

Gee identified 36 principles of good learning built into good game design. The most directly applicable:

1. **Identity Principle:** Learners take on a new identity — they ARE a neuron. This isn't metaphorical; they literally play the role. Gee's research shows this identity commitment drives deeper engagement.

2. **Situated Meaning Principle:** Abstract terms like "weight," "activation," "threshold" gain meaning through situated experience. Participants don't learn definitions — they learn what these things FEEL like.

3. **Pleasant Frustration Principle:** The experience should be "frustrating enough to challenge them but easy enough that they believe they can overcome the problem." Early rounds should be easy (simple threshold, clear signals). Later rounds should introduce complexity (more connections, attention mechanics, ambiguous inputs).

4. **System Thinking Principle:** "Games make players think in a bigger picture, not just individual actions." Participants start focused on their own neuron, but gradually realize the network's intelligence emerges from the collective — no single neuron is "smart."

5. **Incremental Principle:** Learning situations should be ordered so that earlier ones are well designed to lead to later, more complex ones. Start with a single layer, then add layers, then add learning, then add attention.

6. **Regime of Competence Principle:** The experience should operate at the edge of the participant's competence — challenging but doable.

### Flow State Design (Csikszentmihalyi)

Flow occurs when challenge and skill are both high and in balance. For The Human Neuron:

- **Minutes 0-5 (Onboarding):** Very low challenge, building basic skill. Scan QR, see your neuron, understand the interface.
- **Minutes 5-15 (First Forward Pass):** Moderate challenge. Receive inputs, make a threshold decision, see the result.
- **Minutes 15-30 (Learning Rounds):** Rising challenge. Backpropagation, weight adjustment, trying to improve.
- **Minutes 30-45 (Complex Tasks):** High challenge, high skill. Attention mechanisms, multi-step prediction, the network tackling harder problems.
- **Minutes 45-55 (Peak Experience):** The network successfully completes a complex task. Collective triumph.

**Critical flow design element:** Immediate feedback. After each decision, participants instantly see whether the network got the answer right and how their individual decision contributed. Csikszentmihalyi identifies "unambiguous and immediate feedback" as a prerequisite for flow.

### Lessons from Immersive Theater and Meow Wolf

**From Sleep No More:**
- Masks create anonymity and reduce social inhibition — participants engage more freely when they feel less exposed. Consider: each participant IS their neuron identity, not "themselves."
- Multi-sensory engagement is essential. Sound design, visual spectacle on the main screen, haptic feedback on phones (vibration when firing).
- "Immersion is produced on multiple levels: systems, spatial, social/empathic, and narrative/sequential" (Studies in Theatre and Performance, 2023).

**From Meow Wolf:**
- Non-prescriptive exploration: "no right or wrong way to engage." The Human Neuron should feel like discovery, not instruction.
- Interactive elements should be touchable, responsive, and rewarding. Every tap on a phone should produce visible change.
- Narrative gives purpose to exploration. Frame the session as a story: "We're building a brain together. Can our collective brain learn to see? To speak? To predict?"

**From Escape Rooms:**
- Start with an easy puzzle to build confidence (Room2Educ8 Framework, MDPI 2022).
- Linear pathway structure is easier for large groups: one puzzle at a time, each unlocking the next.
- Cognitive load must be managed: alternate complex rounds with simple ones.
- Time pressure creates urgency but shouldn't create panic. Use visible timers for each round.

---

## 3. Embodied Cognition Research

### The Scientific Case for Learning Through Physical Experience

**The Enactment Effect — Meta-Analysis (Psychological Bulletin, 2022):**
A systematic review and meta-analysis across 145 behavioral studies found an average effect size of g = 1.23 for the enactment effect — meaning physically performing an action during learning produces dramatically better recall than reading, listening, or watching. This is a large effect size. The finding holds across children, adults, and elderly populations.

Key finding: "Assigned verb phrases are more recallable if the denoted action is performed during learning, compared to just getting the verbal information or seeing someone else perform the action."

**Application to The Human Neuron:** Participants don't watch a neural network — they perform its operations. They physically (via their phones) receive signals, make threshold decisions, propagate signals. The enactment effect predicts they will retain these concepts far better than from any lecture, video, or diagram.

**Embodied Cognition Taxonomy (Cognitive Research, 2018):**
Researchers distinguish between:
- **Passive embodied learning:** Moving your body, but not in a task-relevant way.
- **Active embodied learning:** Moving your body in ways directly mapped to the learning content.

"Active embodied learning is more effective in enhancing students' learning performance than passive embodied learning."

**Application:** The Human Neuron is active embodied learning by design. The physical action (tapping fire/don't fire, adjusting attention) IS the neural network operation. There's no gap between the embodied action and the concept being learned.

**Integration is Key (Frontiers in Psychology, 2019):**
"An integrated physical learning task leads to higher learning performance than letting learners perform bodily exercises without a relation to the learning contents."

**Application:** Every action participants take must be meaningfully connected to a real neural network operation. No arbitrary gamification — every tap, every decision, every visual feedback element should map to an actual concept.

**Gestures and Mathematical Learning:**
"Children who use gestures while learning mathematical concepts demonstrate significantly better retention and transfer than those who remain physically static."

**Application:** Even the small physical gestures involved in phone interaction (swiping, tapping, tilting) create motor encoding that strengthens memory of the experience.

### Why This Matters for The Human Neuron

The research is unambiguous: acting out a concept produces dramatically better understanding and retention than passive observation. The Human Neuron's core design — making each person a functional neuron — is not just a clever metaphor. It's a scientifically validated learning strategy with a large, well-replicated effect size.

---

## 4. Session Flow Design

### The 45-60 Minute Arc

Based on research from experiential learning design, Kolb's learning cycle, the 4MAT model, and large-group facilitation best practices:

#### Phase 1: Onboarding (0-5 minutes)

**Challenge: Getting 50-200 people set up in under 5 minutes.**

Research-backed strategies:
- **Giant QR code on screen** — no instructions needed, people know what to do with QR codes.
- **Progressive onboarding:** The phone experience starts the moment they scan. While others are still scanning, early joiners see their neuron appear on the main screen visualization, get a brief "you are neuron #23" identity moment, and can explore the simple interface.
- **Music and visual spectacle:** Play an ambient soundtrack. The main screen shows neurons appearing in real time as people join — this creates social pressure to join quickly and visual reward for joining.
- **No verbal instructions yet.** Let the technology onboard. People watch the screen, see others joining, understand implicitly.
- **Assistants in the room** help stragglers with WiFi/QR issues (research recommends 1 assistant per 30-50 people for large groups).

**The 5-minute target is achievable because:**
1. QR-to-browser requires zero account creation, zero app download.
2. Cookie persistence means disconnected users rejoin seamlessly.
3. The interface should be one screen with one obvious action.

#### Phase 2: Warm-Up / First Experience (5-15 minutes)

**Goal:** Everyone understands the basic mechanic before complexity is added.

- **Round 1 — "The Simplest Network" (5 min):** A tiny 2-layer network with a trivially easy task (e.g., "Is this number greater than 5?"). Only a few neurons in each layer. Most participants watch while a small group demonstrates. The facilitator narrates what's happening.
- **Round 2 — "Everyone In" (5 min):** Now the full room is the network. All layers, all neurons. A slightly harder task. Everyone makes their first fire/don't-fire decision. The result appears on screen. Whether the network gets it right or wrong, the facilitator explains what just happened.

**Key facilitation principle:** "Build confidence with an easy first puzzle" (escape room research). The warm-up should be impossible to fail. Everyone fires or doesn't, and the facilitator celebrates the result either way.

#### Phase 3: Core Experience — Learning Rounds (15-35 minutes)

**Goal:** The network learns. Participants experience backpropagation and weight adjustment.

- **Round 3 — "We Got It Wrong" (5 min):** Present a task the network will likely fail. Reveal the error. Introduce backpropagation: "Here's where your weights are being adjusted." Each phone shows the weight changes.
- **Round 4 — "Try Again" (5 min):** Same task type, adjusted weights. The network should perform better. Celebrate improvement.
- **Round 5 — "Now It's Getting Interesting" (5 min):** Introduce a harder task. The network struggles. More adjustment.
- **Round 6 — "The Network Learns" (5 min):** By now, through multiple rounds of weight adjustment, the network should visibly improve at the task category. This is the peak learning moment — participants FEEL the weights converging.

**Optional advanced round (if time allows):**
- **Round 7 — "Attention" (5 min):** Introduce the attention mechanic. Participants choose which inputs to attend to. The network tackles a task that requires selective attention (e.g., "Which word in this sentence is the subject?").

#### Phase 4: Peak Moment + Debrief (35-55 minutes)

- **The Grand Challenge (10 min):** The fully trained network attempts a complex, crowd-pleasing task (e.g., generating the next word in a sentence, classifying an image). When it succeeds, the room erupts.
- **The Reveal (5 min):** The facilitator shows the network topology on screen — the strong connections, the weak ones, the pathways that formed. "Nobody designed this structure. It emerged from your collective learning."
- **Debrief Discussion (5-10 min):** Structured reflection. "What surprised you? What did it feel like when your neuron didn't fire? When did you first notice the network getting smarter?" Research shows that debriefing is essential for converting experience into lasting understanding (Kolb's learning cycle: reflective observation following concrete experience).

#### Phase 5: Close (55-60 minutes)

- **Connect to the real world (3 min):** "What you just experienced is exactly what happens inside ChatGPT, inside image recognition, inside self-driving cars — except with billions of neurons instead of [audience count], running millions of times per second instead of the 6 rounds we just did."
- **Call to action / takeaway (2 min):** Share a URL for further exploration. Possibly let participants see their session data — their personal firing history, their weight changes, how they contributed to the network's learning.

### Large-Group Onboarding Best Practices (Research Summary)

From SessionLab, NASJE, and mega-workshop facilitation research:

1. **Visual scaffolding:** Display step-by-step instructions on the main screen, not just spoken.
2. **Think-pair-share for warm-up:** Even a 60-second "turn to your neighbor and predict what will happen" creates immediate engagement.
3. **Music as a transition signal:** Background music during active rounds, silence during explanation.
4. **Breakout-to-whole-group rhythm:** Alternate between small-group and whole-group attention.
5. **Assistants are essential:** "The larger the class, the more assistants you need."

---

## 5. What Concepts to Teach and In What Order

### Recommended Concept Progression (Simple to Complex)

Based on educational research on teaching neural networks to non-technical audiences, scaffolding principles, and the constraint of 45-60 minutes:

#### Tier 1: Foundation Concepts (Must Teach — Minutes 5-20)

**1. Neurons receive signals and make simple decisions.**
Start here. It's biologically intuitive — everyone knows brains have neurons. The mapping is: you receive input, you decide to fire or not. No math vocabulary needed.

**2. Connections have different strengths (weights).**
Immediately after. "Some signals matter more than others." The meeting analogy works: your boss's opinion carries more weight than a stranger's.

**3. Threshold / Activation.**
"You only fire if the total signal is strong enough." This is a yes/no decision everyone can make. It maps perfectly to a phone tap: fire or don't fire.

**4. Layers — signals flow forward.**
"You're in Layer 2. You receive signals from Layer 1 neurons. Your output goes to Layer 3." Simple spatial metaphor. Forward propagation as a wave through the room.

#### Tier 2: The Learning Mechanism (Should Teach — Minutes 20-40)

**5. The network can be wrong.**
Present a task, get the wrong answer. This is the setup for backpropagation.

**6. Error flows backward.**
"We got it wrong. Now we figure out which connections contributed to the mistake." Backpropagation as blame assignment / credit assignment.

**7. Weights adjust based on errors.**
"The connections that led to the wrong answer get weaker. The ones that would have been right get stronger." Show this on each participant's phone and on the main visualization.

**8. Repeated rounds = learning.**
Multiple rounds of forward pass -> error -> weight adjustment -> improved performance. This IS training a neural network. Participants experience epochs.

#### Tier 3: Advanced Concepts (Nice to Teach — Minutes 40-55)

**9. Attention — dynamic focus.**
"Instead of fixed connections, you choose what to pay attention to." This maps to the transformer architecture's key innovation, but participants experience it as: "For this specific input, which of my neighbors' signals are most relevant?"

**10. Next-token prediction.**
"Language models do what we just did — predict the next word, one token at a time." Connect the session's activities to what ChatGPT actually does.

**11. Emergent intelligence from simple parts.**
The philosophical capstone. "No individual neuron is intelligent. Intelligence emerges from the collective." This is the big takeaway — it applies to brains, to AI, and arguably to societies.

#### What NOT to Try to Teach in 45-60 Minutes

- Gradient descent mathematics
- Specific activation function formulas (ReLU, sigmoid, tanh)
- Convolutional or recurrent architectures
- Loss functions beyond "right vs. wrong"
- Regularization, dropout, batch normalization
- Specific model architectures (GPT, BERT, etc.)

The goal is intuition, not technical precision.

### Why This Order Works

The progression follows research-backed pedagogical principles:

1. **Concrete before abstract** (Kolb): Start with the physical experience of being a neuron before introducing system-level concepts.
2. **Build understanding before analysis** (LinkedIn AI education research): Let people feel it, then explain what they felt.
3. **Simple to complex** (Gee's Incremental Principle): Each concept builds on the previous one. You can't understand backpropagation without first understanding forward propagation.
4. **Experience failure before explaining correction** (escape room design): The network must fail before backpropagation makes emotional sense.

---

## 6. Precedents in CS/AI Education

### CS Unplugged and AI Unplugged

**CS Unplugged (University of Canterbury, NZ):**
The original "teaching computer science without computers" project. Their AI activities include:
- **The Sweet Learning Computer / Intelligent Piece of Paper:** A machine made of sweets that learns to play Hexapawn through negative reinforcement — when it loses, the sweet representing the losing move is removed. After enough games, the machine plays perfectly. This is a direct precedent for The Human Neuron — it makes a learning algorithm tangible.
- **Brain-in-a-Bag:** Explains how neurons work and builds an artificial version.

**AI Unplugged (Northwestern University & German researchers):**
A dedicated collection of unplugged AI activities. Published activities include:
- Training decision trees with physical cards
- Training artificial neural networks with children using physical manipulation of weights
- A board game that simulates neural network training

**Key research finding (ACM Global Computing Education Conference 2025):** "Let's Play! Introducing Neural Networks with Unplugged Resources" — a peer-reviewed paper on using unplugged activities to introduce neural networks, confirming the pedagogical validity of this approach.

**Machine Learning Unplugged (TU Wien / Springer, 2023):**
"Two low-abstraction hands-on unplugged activities on the training aspects of artificial neural networks and decision trees" were developed, tested, and shown effective. Critically: "The process of training a machine learning model can be taught using an unplugged activity, without oversimplifying the concept to a point of abstraction that may leave students under a false impression of how a machine learns from examples."

**ISTE's 3 Unplugged Activities for Teaching About AI:**
1. Facial recognition simulation (students break down images into features)
2. Tic Tac Toe AI (a piece of paper "programmed" to play)
3. Turing Test role-play (students act as AI and judge)

### What The Human Neuron Adds Beyond These Precedents

Every existing unplugged AI activity has one of these limitations:
- **Small scale** — designed for a classroom of 20-30 students, not 50-200.
- **Observer-based** — participants watch the algorithm work, they don't embody it.
- **Single-concept** — they teach one concept (decision trees OR neural networks OR the Turing test), not a progressive sequence.
- **Not real-time** — they're turn-based paper activities, not synchronized digital experiences.

The Human Neuron is genuinely novel because it combines:
1. Each participant IS a computational unit (not watching one).
2. Real-time synchronization across 50-200 phones.
3. Progressive concept introduction within a single session.
4. Visual spectacle on a shared screen showing the collective computation.
5. Multiple rounds that demonstrate actual learning/weight adjustment.

### The Tech Interactive's Machine Learning Unplugged

The Tech Interactive (San Jose) developed a "Machine Learning Unplugged" workshop where students physically sort and classify data. Relevant design lesson: they found that physical manipulation of data made the concept of "training data" immediately intuitive in a way that digital tools didn't.

### Hour of Code Approaches

Hour of Code's design philosophy is directly applicable:
- **Zero-to-something in minutes:** Participants should produce a meaningful result within 5 minutes of starting.
- **No prerequisites:** Assume zero technical knowledge.
- **Guided discovery over instruction:** The system teaches through doing, not through explanation.

### The Next-Token Prediction Game (Buck et al., 2022)

Researchers created a website where participants tried to predict the next token in text sequences. Sixty participants achieved only 29% accuracy, significantly worse than even small language models. "Playing the game for half an hour gives useful perspective on what it's like to be a language model."

**Application:** This research directly validates the idea that having humans attempt a neural network's task creates visceral understanding. The Human Neuron takes this further by making participants not just attempt the task individually, but collectively produce the answer through actual network computation.

---

## Summary of Actionable Recommendations

### Highest-Confidence Design Decisions

1. **The fire/don't-fire threshold decision is the core mechanic.** Everything else builds on this. Make it a single tap on a phone. Make the threshold visible. Make the consequence visible on the main screen.

2. **Run 5-7 rounds with progressive complexity.** Start with simple forward propagation, introduce error and backpropagation by round 3, show convergent learning by round 5-6.

3. **The main screen visualization is as important as the phone experience.** The shared visual spectacle — neurons lighting up, signals cascading through layers, weights strengthening — is what creates the collective "wow" moment and makes the experience memorable.

4. **Debrief is non-negotiable.** Without structured reflection, embodied experience doesn't convert to conceptual understanding. Budget at least 5-10 minutes for debrief.

5. **Onboard through technology, not lectures.** QR scan -> immediate visual feedback (your neuron appears on screen) -> first action within 60 seconds of scanning.

6. **Weight adjustment is the emotional core.** The moment participants see their connections changing — strengthening when they contributed to correct answers, weakening when they contributed to errors — is when the concept of "learning" clicks at a gut level.

7. **Frame the whole session as a story.** "Can our collective brain learn to [task]?" gives narrative purpose to every round.

8. **Keep it to 3 layers maximum for the main experience.** More layers = more complexity to explain, more latency between rounds. Three layers (input, hidden, output) teaches the essential architecture without overwhelming.

9. **End with the emergent intelligence revelation.** Show the final network topology. "Nobody designed these pathways. They emerged from our collective learning." This is the philosophical payoff that makes the experience stick.

10. **The attention mechanism round is a powerful bonus but not essential.** If time is tight, cut it. The core story (forward pass -> error -> backprop -> learning) is complete without it.

---

## Sources

### CS/AI Education
- [CS Unplugged — AI Activities](https://classic.csunplugged.org/activities/community-activities/artificial-intelligence/)
- [AI Unplugged](https://www.aiunplugged.org/)
- [AI Unplugged — Northwestern University](https://sites.northwestern.edu/aiunplugged/)
- [Let's Play! Introducing Neural Networks with Unplugged Resources (ACM 2025)](https://dl.acm.org/doi/10.1145/3736251.3747320)
- [Machine Learning Unplugged — TU Wien (Springer)](https://link.springer.com/chapter/10.1007/978-3-030-33759-9_11)
- [Machine Learning Unplugged — Training Decision Trees and ANNs with Children](https://repositum.tuwien.at/handle/20.500.12708/177245)
- [ISTE — 3 Unplugged Activities for Teaching About AI](https://iste.org/blog/3-unplugged-activities-for-teaching-about-ai)
- [Machine Learning Unplugged — The Tech Interactive](https://www.thetech.org/education/education-resources/lessons/machine-learning-unplugged/)
- [Unplugged Activities in the Context of AI (Springer)](https://link.springer.com/chapter/10.1007/978-3-030-33759-9_10)

### Embodied Cognition
- [The Enactment Effect: Systematic Review and Meta-Analysis (Psychological Bulletin, 2022)](https://pubmed.ncbi.nlm.nih.gov/35878067/)
- [Using Actions to Enhance Memory: Enactment, Gestures, and Exercise (Frontiers in Psychology)](https://pmc.ncbi.nlm.nih.gov/articles/PMC3536268/)
- [Embodied Learning Taxonomy (Cognitive Research, 2018)](https://cognitiveresearchjournal.springeropen.com/articles/10.1186/s41235-018-0092-9)
- [Embodied Learning: Why at School the Mind Needs the Body (Frontiers in Psychology, 2019)](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2019.02098/full)
- [Research Avenues Supporting Embodied Cognition (Educational Psychology Review, 2024)](https://link.springer.com/article/10.1007/s10648-024-09847-4)
- [Embodied Cognition in Education (Structural Learning)](https://www.structural-learning.com/post/embodied-cognition)

### Game Design and Flow
- [James Paul Gee's 16 Principles for Game-Based Learning](https://www.legendsoflearning.com/blog/james-paul-gee-game-based-learning/)
- [James Paul Gee — Learning Principles](https://mason.gmu.edu/~lsmithg/jamespaulgee2print.html)
- [Gee — 36 Learning Principles in Games](http://donaldclarkplanb.blogspot.com/2021/11/gee-36-learning-principles-in-games.html)
- [Flow Theory — Game Design Toolkit](https://tkdev.dss.cloud/gamedesign/toolkit/flow-theory/)
- [Flow in Games — Jenova Chen MFA Thesis](https://www.jenovachen.com/flowingames/Flow_in_games_final.pdf)
- [The Flow Theory Applied to Game Design](https://thinkgamedesign.com/flow-theory-game-design/)

### Immersive Experience Design
- [Audience Behavior in Immersive Theatre: Sleep No More (Studies in Theatre and Performance, 2023)](https://www.tandfonline.com/doi/full/10.1080/14682761.2023.2185928)
- [Together Here: Immersive Theatre, Audience, and Space](https://digitalcommons.trinity.edu/cgi/viewcontent.cgi?article=1004&context=hct_honors)
- [Meow Wolf — Immersive Art Experience Design](https://blooloop.com/brands-ip/in-depth/meow-wolf-immersive-art/)
- [The Meow Wolf Effect: Why Immersive Experiences Matter](https://geekmom.com/2019/01/the-meow-wolf-effect-why-immersive-experiences-matter/)

### Escape Room and Educational Game Design
- [Room2Educ8: Framework for Educational Escape Rooms (MDPI Education, 2022)](https://www.mdpi.com/2227-7102/12/11/768)
- [Escape Education: Systematic Review (Computers & Education, 2020)](https://www.sciencedirect.com/science/article/pii/S1747938X20300531)
- [Why Puzzle Flow Is Key to Escape Room Design](https://www.rushescapegame.com.au/rush-blog/2025/6/6/why-good-puzzle-flow-is-essential-to-building-a-great-escape-roomnbsp)

### Workshop Facilitation
- [Mega-Workshop Facilitation Tips](https://gojko.net/2021/09/09/mega-workshop-facilitation-tips/)
- [Facilitating Large Group Discussions (NASJE)](https://nasje.org/facilitating-large-group-discussions-and-activities-make-numbers-count/)
- [How to Create an Unforgettable Training Session (SessionLab)](https://www.sessionlab.com/blog/training-session-plan/)
- [Planning and Presenting Workshops That Work (MedEdPORTAL / PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC8110637/)

### Neural Network Concepts and Teaching
- [Backpropagation: How Neural Networks Learned to Learn](https://medium.com/@igquinteroch/backpropagation-how-neural-networks-learned-to-learn-8f0d6654e914)
- [What is an Attention Mechanism? (IBM)](https://www.ibm.com/think/topics/attention-mechanism)
- [Hebbian Theory — Neurons That Fire Together Wire Together](https://fancycomma.com/2024/10/19/neuroscience-hebbs-law/)
- [Language Models Are Better Than Humans at Next-Token Prediction](https://arxiv.org/html/2212.11281v2)
- [A Visual and Interactive Guide to Neural Networks (Jay Alammar)](https://jalammar.github.io/visual-interactive-guide-basics-neural-networks/)
- [Teaching Neural Networks to Non-Technical Audiences (LinkedIn)](https://www.linkedin.com/advice/0/how-can-you-teach-non-technical-audiences)
