# Research: Collective Text Generation, Token Prediction & Human Computation

## 1. Shannon's Guessing Game (1951) — The Scientific Ancestor

Claude Shannon's paper "Prediction and Entropy of Printed English" is literally next-token prediction performed by humans.
- Humans predicted next letter correctly ~50% of the time on first guess
- With context, accuracy rose dramatically
- Estimated entropy of English at ~1.0-1.5 bits per character
- Proved natural language is highly redundant and predictable

**For The Human Neuron:** Frame the experience as "Shannon's Game, scaled to a crowd, upgraded to words."

## 2. Human vs. LLM Next-Word Prediction

### Goldstein et al. (2024)
- Directly compared human next-word prediction to GPT-2/GPT-3
- Humans and LLMs show surprisingly correlated prediction patterns
- They diverge in interesting ways: humans bring world knowledge, LLMs exploit statistical patterns

### Caucheteux & King (2022) — Nature Machine Intelligence
- Internal representations of LLMs align with brain activity (fMRI/MEG)
- Transformer "layers" loosely map to stages of human language processing

### Schrimpf et al. (2021) — PNAS
- Best language models are also best predictors of neural activity in human brain
- Better next-word prediction = better brain alignment
- **This validates the core metaphor — it's not just analogy, it's neuroscience**

### Fedorenko Lab (MIT)
- Human language network is fundamentally a prediction engine
- Brain regions show stronger activation for less predictable words (higher "surprisal")
- Exactly parallels how LLMs assign lower probability to surprising tokens

## 3. Crowd Collective Action Precedents

### Twitch Plays Pokemon (2014) — Most Important UX Precedent
- 1.16 million participants collectively played Pokemon via Twitch chat
- **Anarchy vs Democracy mode:** voting system where most popular command won every 20 seconds
- Crowd completed the game in 16 days despite apparent chaos
- Players created shared mythology (Helix Fossil as god)
- The "start9" rebellion showed how crowd systems can be gamed

**Key lesson:** The aggregation mechanism IS the design. The tension between chaos and order IS the entertainment.

### Reddit Place (2017, 2022)
- Every user places one colored pixel every 5 minutes on shared canvas
- Self-organization emerged without formal coordination
- **Key lesson:** Constraints create strategy. Rate-limiting forces strategic thinking.

## 4. Collective Text Generation Art

### Exquisite Corpse (Surrealist, ~1925)
- Each person sees only previous contribution and adds to it
- Partial-information aspect maps to "context window" in LLMs
- **Design lever:** Vary how much prior text participants can see

### Human Computation (Luis von Ahn)
- **ESP Game (2004):** Two strangers label images, score by matching. Proved humans can perform computation while playing.
- **reCAPTCHA (2007):** Turned CAPTCHA-solving into book digitization. Humans as processing units in a larger system.
- **Key insight:** Make the computation feel like play.

### Unanimous AI / Swarm Intelligence
- Groups of ~20-50 consistently outperformed individual experts
- Real-time, simultaneous input (not sequential voting) was crucial
- Correctly predicted Kentucky Derby superfecta at 540:1 odds
- **Key lesson:** Real-time feedback loops where participants see others' inputs creates emergent intelligence

## 5. Wisdom of Crowds (Surowiecki, 2004)

Four conditions for crowd wisdom:
1. Diversity of opinion
2. Independence (not influenced by neighbors)
3. Decentralization
4. Aggregation mechanism

**Design tension:** Independence conflicts with visible feedback. But in a neural network, neurons ARE influenced by each other — that's the point. Embrace herding to simulate weight reinforcement.

## 6. The Chinese Room Connection

Searle's thought experiment made real: each participant contributes a word without controlling the emerging text. The collective produces coherent language. Does the system "understand"?

**The philosophical "aha moment" IS the product.** The text is secondary — the real output is the audience realizing "WE are the language model."

## 7. Critical Design Principles

### From Shannon: Context is everything
Varying the visible context window is a powerful lever for difficulty/coherence.

### From TPP: The aggregation mechanism IS the design
How you turn 200 word submissions into one chosen word is the most important decision. Options: majority vote, weighted random sampling (temperature), ranked-choice, real-time tug-of-war.

### From Unanimous AI: Real-time feedback creates emergence
If participants see votes accumulating live, they adjust behavior, creating a dynamic system.

### From Von Ahn: Make computation feel like play
Gamification isn't optional — it's the engagement engine.

### From Wisdom of Crowds: Temperature is crucial
Too much consensus = boring text. Too much randomness = incoherent. The sweet spot is where the crowd "hallucinates" just enough to be surprising. This directly parallels LLM temperature.

### From Reddit Place: Constraints create strategy
Rate-limiting, turn-taking, or limited word options force careful thinking and better output.

### From Komar & Melamid's "Most Wanted Painting": Averaging = mediocrity
Simple majority voting produces bland, predictable text. Use weighted random sampling from top-K words, mimicking temperature in text generation.

## 8. Key Papers & Resources
1. Shannon (1951) — "Prediction and Entropy of Printed English"
2. Fedorenko et al. — MIT language and brain research: https://evlab.mit.edu/
3. Schrimpf et al. (2021) — "The Neural Architecture of Language" in PNAS
4. Surowiecki (2004) — The Wisdom of Crowds (book)
5. Von Ahn (2006) — "Games with a Purpose" in IEEE Computer
6. Unanimous AI research — https://unanimous.ai/research/
7. Caucheteux & King (2022) — "Brains and algorithms partially converge" in Nature Communications
8. Searle (1980) — "Minds, Brains, and Programs" in Behavioral and Brain Sciences
