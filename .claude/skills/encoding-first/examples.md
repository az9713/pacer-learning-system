# Encoding-First Examples

Scenarios comparing encoding-first vs retrieval-first approaches.

---

## Scenario 1: Medical Student Learning Pharmacology

### ❌ Retrieval-First Approach

**Day 1:**
```
Student: "I'll make Anki cards for all the drug classes."

Creates 200 flashcards:
- "What is the mechanism of ACE inhibitors?" → "Block angiotensin converting enzyme"
- "What are side effects of ACE inhibitors?" → "Cough, hyperkalemia, angioedema"
- [198 more cards...]
```

**Day 7:**
```
Student: "I have 400 cards to review. This is taking hours."
- Reviews cards mechanically
- Forgets context and connections
- Can answer cards but struggles with case-based questions
```

**Day 30:**
```
Student: "I can't keep up with reviews. I know isolated facts but can't
integrate them. When presented with a patient case, I freeze."
```

### ✅ Encoding-First Approach

**Day 1:**
```
Student: "Let me first understand the cardiovascular system and blood pressure
regulation. Then I'll see where drugs fit in."

Creates a GRINDE map:
- Blood pressure = cardiac output × peripheral resistance
- Mechanisms to lower: reduce volume, reduce heart rate, dilate vessels
- Drug classes map to these mechanisms
```

**Day 3:**
```
Student: "Now I see that ACE inhibitors work by blocking the RAAS system,
which reduces both volume (less aldosterone) and resistance (less angiotensin II).

The cough makes sense—bradykinin isn't broken down, accumulates in lungs."
```

**Day 7:**
```
Creates minimal flashcards for Reference-type info only:
- Specific dosages (truly arbitrary)
- Drug interactions to memorize

Total: 30 cards instead of 200
```

**Day 30:**
```
Student: "Given a case, I can reason through which drug class makes sense.
My cards are manageable. Understanding persists because it's connected to logic."
```

---

## Scenario 2: Learning JavaScript Promises

### ❌ Retrieval-First Approach

```javascript
// Makes flashcards with code snippets

Card 1:
Q: "How to create a Promise?"
A: "new Promise((resolve, reject) => { })"

Card 2:
Q: "How to handle Promise resolution?"
A: ".then(result => { })"

// Result: Can reproduce syntax but doesn't understand async flow
// When debugging: "Why isn't my .then() running?"
```

### ✅ Encoding-First Approach

```
Step 1: Understand the WHY (Layer 1 - Logic)

"Promises solve the callback hell problem. JavaScript is single-threaded
but needs to handle operations that take time (network requests, file reads).

A Promise is a 'placeholder' for a future value. It can be:
- Pending: Operation in progress
- Fulfilled: Operation succeeded, value available
- Rejected: Operation failed, error available"

Step 2: Build mental model with GRINDE map

┌─────────────────────┐
│  PROMISE CREATED    │
│  (pending state)    │
└─────────┬───────────┘
          │
          │ async operation runs
          ▼
    ┌─────┴─────┐
    │           │
    ▼           ▼
┌───────┐   ┌────────┐
│SUCCESS│   │ ERROR  │
│.then()│   │.catch()│
└───────┘   └────────┘

Step 3: Practice immediately (Procedural)

// Write actual async code, encounter real problems
// Debug real issues to deepen understanding

Step 4: Minimal flashcards for syntax details only

"await must be inside async function" - R-type, flashcard OK
```

---

## Scenario 3: Learning Economic Concepts

### ❌ Retrieval-First Approach

```
Student creates flashcard deck:

Q: "Define price elasticity of demand"
A: "Percentage change in quantity demanded divided by percentage change in price"

Q: "What is elastic demand?"
A: "Elasticity > 1"

Q: "What is inelastic demand?"
A: "Elasticity < 1"

[50 more definition cards]

Problem: Can define terms but can't analyze real markets.
"Is demand for insulin elastic or inelastic?" *blank stare*
```

### ✅ Encoding-First Approach

```
Step 1: Logic Layer

"Elasticity measures responsiveness. If I raise the price, do customers
have alternatives? Can they just not buy it?

Elastic = customers respond strongly (luxuries, many substitutes)
Inelastic = customers don't respond much (necessities, no substitutes)"

Step 2: Concept Map

┌────────────────────────────────────────┐
│         PRICE ELASTICITY               │
│                                        │
│     "How much do buyers respond        │
│      to price changes?"                │
└───────────────────┬────────────────────┘
                    │
        ┌───────────┴───────────┐
        │                       │
        ▼                       ▼
┌───────────────┐       ┌───────────────┐
│   ELASTIC     │       │   INELASTIC   │
│    (>1)       │       │    (<1)       │
│               │       │               │
│ • Luxuries    │       │ • Necessities │
│ • Substitutes │       │ • No subs     │
│ • Long-run    │       │ • Short-run   │
│ • Small % of  │       │ • Addiction   │
│   budget      │       │               │
└───────────────┘       └───────────────┘

Step 3: Application

"Insulin: Can diabetics just not buy it? No. Substitutes? No.
→ Inelastic. Drug companies can raise prices, quantity barely drops.

Movie tickets: Must-have? No. Substitutes? Many (streaming, books).
→ Elastic. Raise prices, people stay home."

Step 4: Only R-type for flashcards

"Formula for elasticity calculation" - worth a flashcard
"Elasticity = 1 is called 'unit elastic'" - terminology, flashcard OK
```

---

## Key Takeaways

| Situation | Retrieval-First Result | Encoding-First Result |
|-----------|----------------------|----------------------|
| Exam with novel questions | Struggles (memorized facts, not understanding) | Succeeds (can reason from principles) |
| Time spent reviewing | Hours daily | Minutes daily |
| Long-term retention | Poor (constant review needed) | Strong (understanding persists) |
| Ability to teach others | Reads flashcard answers | Explains from mental model |
| Problem-solving | Looks for memorized patterns | Reasons from first principles |

---

## When to Use Each Approach

### Encoding-First (Most Content)
- Conceptual understanding (C)
- Procedural skills (P) - through practice
- Analogies (A) - through critique
- Evidence (E) - through application

### Retrieval-OK (Limited Use)
- True Reference material (R)
- Arbitrary details after understanding is solid
- Maintaining already-understood material
- Exam-specific memorization (last resort)
