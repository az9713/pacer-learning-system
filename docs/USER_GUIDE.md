# PACER Learning System - Complete User Guide

## Table of Contents

1. [Introduction](#introduction)
2. [What is PACER?](#what-is-pacer)
3. [Installation](#installation)
4. [Getting Started](#getting-started)
5. [Understanding the 5 Information Types](#understanding-the-5-information-types)
6. [Using Commands](#using-commands)
7. [The 4 Layers of Learning](#the-4-layers-of-learning)
8. [GRINDE Mind Mapping](#grinde-mind-mapping)
9. [Best Practices](#best-practices)
10. [Frequently Asked Questions](#frequently-asked-questions)

---

## Introduction

### Who is This Guide For?

This guide is for anyone who wants to learn more efficiently. You don't need any technical background. If you:

- Struggle to remember what you study
- Spend hours making flashcards that don't stick
- Feel overwhelmed by information
- Want to learn faster with less effort

...then this system is for you.

### What Will You Learn?

By the end of this guide, you will:

1. Understand why most study methods are inefficient
2. Know how to classify any information for optimal learning
3. Use simple commands to process what you learn
4. Create powerful mind maps that stick in memory
5. Balance your learning between consuming and digesting

### The Big Idea

**Most people study wrong.** They try to memorize everything with flashcards. But here's the secret:

> "Lots of retrieval without proper encoding is like filling a leaky bucket faster."
> — Dr. Justin Sung

Instead of memorizing harder, you need to **understand better first**. This system teaches you how.

---

## What is PACER?

PACER is a system for classifying information into 5 types. Each type needs a different approach:

| Letter | Type | What It Means | What To Do |
|--------|------|---------------|------------|
| **P** | Procedural | A skill or technique | **Practice** it |
| **A** | Analogous | A comparison or metaphor | **Critique** it |
| **C** | Conceptual | An idea or theory | **Understand** it |
| **E** | Evidence | Data or examples | **Connect** it to concepts |
| **R** | Reference | Arbitrary facts | **Memorize** it (last resort!) |

### Why Does This Matter?

Most people treat ALL information like R-type (Reference). They try to memorize everything with flashcards. But:

- **Conceptual** information should be UNDERSTOOD, not memorized
- **Procedural** information should be PRACTICED, not flashcarded
- **Analogous** information should be CRITIQUED, not accepted blindly

Only truly **arbitrary** facts (like dates or phone numbers) need memorization.

### A Real Example

Let's say you're learning about photosynthesis. Here's how to classify the information:

| Information | Type | Why | What To Do |
|-------------|------|-----|------------|
| "Photosynthesis converts light to chemical energy" | C | Core concept | Understand the mechanism |
| "It's like a solar panel charging a battery" | A | Analogy | Critique: Where does this break down? |
| "Light reactions happen in thylakoid membrane" | C | Concept (location matters for understanding) | Map it |
| "The equation: 6CO₂ + 6H₂O → C₆H₁₂O₆ + 6O₂" | E | Evidence of the process | Connect to the concept |
| "Chlorophyll absorbs 680nm wavelength" | R | Arbitrary number | Memorize ONLY if exam requires |

Notice: Most information is **NOT** R-type!

---

## Installation

### What You Need

1. **Claude Code** - The AI assistant CLI tool
2. **This project folder** - Contains all the learning tools

### Step-by-Step Installation

#### Step 1: Verify Claude Code is Installed

Open your terminal (Command Prompt on Windows, Terminal on Mac/Linux) and type:

```bash
claude --version
```

You should see a version number like `1.0.0` or similar.

**If you get an error**: You need to install Claude Code first. Visit https://claude.ai/code and follow the installation instructions for your operating system.

#### Step 2: Navigate to the Project Folder

In your terminal, go to the folder containing this project:

**On Windows:**
```bash
cd C:\path\to\pacer_bestpartnerstv
```

**On Mac/Linux:**
```bash
cd /path/to/pacer_bestpartnerstv
```

Replace the path with wherever you saved this project.

#### Step 3: Start Claude Code

Type:

```bash
claude
```

This starts the Claude Code assistant with all the PACER tools loaded.

#### Step 4: Verify Installation

Once Claude is running, the PACER skills and commands are ready to use. Try:

```
What learning tools are available?
```

Claude should mention the PACER classification system and related commands.

---

## Getting Started

### Your First PACER Classification

Let's classify some content together. Follow these steps:

#### Step 1: Prepare Your Content

Think of something you're trying to learn. For example:

> "Machine learning is a subset of artificial intelligence where computers learn patterns from data instead of being explicitly programmed. A common example is email spam filtering."

#### Step 2: Ask Claude to Classify It

Simply tell Claude:

```
Classify this content:

Machine learning is a subset of artificial intelligence where
computers learn patterns from data instead of being explicitly
programmed. A common example is email spam filtering.
```

#### Step 3: Read the Classification

Claude will break down the content:

- **Conceptual**: "computers learn patterns from data" (understand this!)
- **Conceptual**: "subset of AI" (relationship to understand)
- **Evidence**: "email spam filtering" (example supporting the concept)

#### Step 4: Follow the Digestion Recommendation

Claude will suggest what to do next. For conceptual content, it might say:

> "Create a mind map showing how ML relates to AI and how the learning process works."

### Your First Mind Map

Now let's create a GRINDE mind map:

#### Step 1: Ask for a Map

Tell Claude:

```
Create a mind map for machine learning basics
```

#### Step 2: Receive Your Map

Claude will create an ASCII visual map like:

```
═══════════════════════════════════════════
        ★★★ MACHINE LEARNING ★★★
═══════════════════════════════════════════

┌─────────────────────────────────────┐
│  ★★ CORE CONCEPT                    │
│                                     │
│  Computers LEARN from DATA          │
│  (not explicitly programmed)        │
│                                     │
│  Why: Handles patterns too complex  │
│       for manual rules              │
└────────────────┬────────────────────┘
                 │
        ┌────────┴────────┐
        ▼                 ▼
┌──────────────┐   ┌──────────────┐
│ Supervised   │   │ Unsupervised │
│ (labeled     │   │ (find hidden │
│  examples)   │   │  patterns)   │
└──────────────┘   └──────────────┘
```

#### Step 3: Study the Map

- Notice the hierarchy (most important at top)
- See the relationships (arrows show connections)
- Read the "Why" notes (explains significance)

---

## Understanding the 5 Information Types

### P - Procedural (Practice It!)

**What it is**: Skills, techniques, methods, processes, "how to" information.

**Examples**:
- How to solve a quadratic equation
- Steps to perform CPR
- Cooking a recipe
- Writing a for-loop in code

**How to recognize it**: Ask yourself, "Is this something I need to DO?"

**What to do**: PRACTICE. Actually do the thing. Reading about it isn't enough.

**Common mistake**: Making flashcards about procedures instead of practicing them.

---

### A - Analogous (Critique It!)

**What it is**: Comparisons, metaphors, "it's like..." statements.

**Examples**:
- "The brain is like a computer"
- "DNA is like a blueprint"
- "Electricity flows like water"
- "The economy is like an ecosystem"

**How to recognize it**: Look for "like," "similar to," "as if," comparisons.

**What to do**: CRITIQUE. Ask:
- Where is this analogy accurate?
- Where does it break down?
- What might it mislead me about?

**Common mistake**: Accepting analogies without questioning their limits.

**Example critique**:

| Analogy: "The heart is like a pump" |
|-------------------------------------|
| ✅ Accurate: Moves fluid, has valves, creates pressure |
| ⚠️ Limitation: Heart is self-regulating, self-repairing |
| ❌ Misleading: Heart has electrical system, pumps aren't alive |

---

### C - Conceptual (Understand It!)

**What it is**: Ideas, theories, explanations, "why" information.

**Examples**:
- Why does inflation happen?
- What causes seasons?
- How does natural selection work?
- Why do heavier objects fall at the same rate as lighter ones?

**How to recognize it**: Ask, "Is this explaining WHY or HOW something works?"

**What to do**: Create GRINDE mind maps. Connect to existing knowledge. Explain it in your own words.

**Common mistake**: Trying to memorize concepts with flashcards instead of understanding them.

---

### E - Evidence (Connect It!)

**What it is**: Data, examples, case studies, statistics that SUPPORT concepts.

**Examples**:
- "In a 2020 study, 80% of participants..."
- "For example, consider what happened in 1929..."
- "The experiment showed that..."
- Specific data points

**How to recognize it**: Ask, "Does this support or illustrate a bigger idea?"

**What to do**: Connect the evidence to the concept it supports. Don't memorize it in isolation.

**Common mistake**: Memorizing statistics without knowing what concept they support.

---

### R - Reference (Memorize - Last Resort!)

**What it is**: Truly arbitrary information with no underlying logic.

**Examples**:
- Phone numbers
- Specific dates (sometimes)
- Arbitrary constants
- Names that must be recalled exactly

**How to recognize it**: Ask, "Is there NO WAY to derive or understand this?"

**What to do**: Use flashcards and spaced repetition. But ONLY after understanding related concepts.

**Common mistake**: Classifying conceptual information as R-type because it seems hard.

### The Golden Rule

> **Most information is NOT R-type!**
>
> If you're making hundreds of flashcards, you're probably classifying wrong.
> Challenge every R classification: "Can I understand this instead of memorize it?"

---

## Using Commands

### Overview of Available Commands

| Command | What It Does | When To Use |
|---------|-------------|-------------|
| Ask Claude to classify | Breaks content into P/A/C/E/R | When you have new material |
| Ask for a GRINDE map | Creates visual concept map | For conceptual content |
| Ask to digest content | Processes by type | After classification |
| Ask for balance check | Checks consumption vs digestion | After reading sessions |
| Ask for layer check | Verifies understanding depth | To find knowledge gaps |
| Ask for flashcards | Creates R-type cards | ONLY for arbitrary facts |

### How to Use Each Command

#### Classifying Content (PACER)

**Purpose**: Identify what type of information you're dealing with.

**How to use**:
```
Classify this content for learning:

[paste your content here]
```

**What you'll get**:
- Breakdown by type (P/A/C/E/R)
- Count of each type
- Recommended next steps

**Example**:
```
Classify this content for learning:

To make French press coffee, coarse grind your beans, add hot water
(not boiling - about 200°F), steep for 4 minutes, then slowly press
the plunger down. The coffee-to-water ratio is typically 1:15.
```

**Result**:
- 🔧 **P (Procedural)**: Grinding, water temperature, steeping, pressing
- 📚 **R (Reference)**: 200°F temperature, 4 minutes, 1:15 ratio
- **Recommendation**: Practice the procedure; memorize ratios only if needed

---

#### Creating Mind Maps (GRINDE)

**Purpose**: Create visual maps for deep understanding.

**How to use**:
```
Create a GRINDE mind map for [topic]
```

**What you'll get**:
- Visual ASCII diagram
- Grouped concepts
- Relationships shown with arrows
- "Why" annotations
- Understanding check questions

**Example**:
```
Create a GRINDE mind map for the water cycle
```

---

#### Digesting Content

**Purpose**: Process content using the right protocol for its type.

**How to use**:
```
Help me digest this [P/A/C/E/R] content:

[paste content]
```

**What you'll get**:

| Type | What You'll Receive |
|------|-------------------|
| P | Practice exercises, step-by-step breakdown |
| A | Critique questions, limits analysis |
| C | Mind map, understanding questions |
| E | Connection to parent concept |
| R | Minimal flashcards (with verification) |

**Example**:
```
Help me digest this Procedural content:

To solve a quadratic equation ax² + bx + c = 0, use the quadratic
formula: x = (-b ± √(b²-4ac)) / 2a
```

---

#### Checking Learning Balance

**Purpose**: See if you're consuming more than you're digesting.

**How to use**:
```
Check my learning balance for this session
```

**What you'll get**:
- Analysis of what you've read
- Analysis of what you've processed
- Balance percentage
- Recommendations

**When to use**:
- After a reading session
- When feeling overwhelmed
- Before ending a study session

---

#### Checking Understanding Layers

**Purpose**: Verify you've built knowledge in the right order.

**How to use**:
```
Check my understanding layers for [topic]
```

**What you'll get**:
- Questions testing each layer
- Assessment of gaps
- Recommendations for weak layers

**The 4 layers** (must be built in order):
1. **Logic** - WHY does this work?
2. **Concepts** - WHAT are the main ideas?
3. **Important Details** - WHICH specifics matter?
4. **Arbitrary Details** - What must be memorized?

---

#### Creating Flashcards

**Purpose**: Generate cards for TRUE R-type content only.

**How to use**:
```
Create flashcards for this reference information:

[paste ONLY arbitrary facts]
```

**What you'll get**:
- Verification that content is truly R-type
- Minimal card set
- Anki-compatible format
- Warnings if content should be understood instead

**Important**: Claude will challenge you if content isn't truly R-type!

---

## The 4 Layers of Learning

### Why Order Matters

Imagine building a house:
- You can't add the roof before the walls
- You can't add walls before the foundation

Learning works the same way. The 4 layers MUST be built in order:

```
Layer 4: Arbitrary Details  ← LAST (minimal)
Layer 3: Important Details  ← Third
Layer 2: Concepts           ← Second
Layer 1: Logic              ← FIRST (foundation)
```

### Layer 1: Logic (The Foundation)

**What it is**: Understanding WHY something works.

**Questions to ask**:
- Why does this exist?
- What problem does it solve?
- What's the underlying mechanism?

**Example** (Antibiotics):
> "Antibiotics work by targeting structures that bacteria have but human cells don't—like bacterial cell walls. That's WHY they kill bacteria without killing us."

**Sign you've mastered it**: You can explain the "why" without notes.

### Layer 2: Concepts (The Structure)

**What it is**: The major ideas and how they relate.

**Questions to ask**:
- What are the main components?
- How do they connect to each other?
- What's the big picture?

**Example** (Antibiotics):
> "There are different classes: beta-lactams target cell walls, macrolides target protein synthesis, fluoroquinolones target DNA. Each class has a spectrum (narrow vs broad)."

**Sign you've mastered it**: You can draw a concept map from memory.

### Layer 3: Important Details (The Finishing)

**What it is**: Specific information that crystallizes understanding.

**Questions to ask**:
- What distinguishes X from Y?
- What are the key exceptions?
- What matters for application?

**Example** (Antibiotics):
> "Penicillins are first-line for gram-positive. Azithromycin is backup for penicillin allergy. The distinctive cough from ACE inhibitors helps choose alternatives."

**Sign you've mastered it**: You can explain the specifics that matter for decisions.

### Layer 4: Arbitrary Details (The Decoration)

**What it is**: Facts that simply ARE, with no underlying logic.

**Questions to ask**:
- Can this be derived from understanding?
- Must this be recalled instantly?
- Is this truly arbitrary?

**Example** (Antibiotics):
> "Amoxicillin dosage is 500mg TID. That's an arbitrary number—memorize only if you must recall it without references."

**Sign you're here appropriately**: Your flashcard count is MINIMAL.

### The Common Mistake

**Wrong approach**:
```
Day 1: "Let me memorize all the drug dosages!" (Layer 4 first)
Result: Endless flashcards, poor retention, can't reason about cases
```

**Right approach**:
```
Day 1: "Why do antibiotics work? What are the mechanisms?" (Layer 1)
Day 2: "What are the major classes and their targets?" (Layer 2)
Day 3: "Which drugs for which infections? Why?" (Layer 3)
Day 4: "What specific dosages must I memorize?" (Layer 4 - minimal)
Result: Deep understanding, easy recall, can reason about new cases
```

---

## GRINDE Mind Mapping

### What is GRINDE?

GRINDE is a method for creating mind maps that stick in memory. Each letter represents a principle:

| Letter | Principle | What It Means |
|--------|-----------|---------------|
| **G** | Grouped | Chunk related information together |
| **R** | Reflective | Add "why" notes and personal understanding |
| **I** | Interconnected | Show relationships between ideas |
| **N** | Non-verbal | Use symbols, diagrams, visuals |
| **D** | Directional | Show flow, hierarchy, cause-effect |
| **E** | Emphasized | Mark importance levels (★★★, ★★, ★) |

### How to Create a GRINDE Map

#### Step 1: Identify the Backbone

Before mapping, find the ONE core insight that holds everything together.

**Example** (Supply and Demand):
> "Opposing forces (buyers want low prices, sellers want high) create equilibrium."

This is your backbone—everything else hangs off this.

#### Step 2: Group into Chunks (G)

Identify 3-5 major chunks of related information.

**Example**:
- Demand (buyer behavior)
- Supply (seller behavior)
- Equilibrium (where they meet)
- Disequilibrium (what happens when off-balance)

#### Step 3: Add Reflections (R)

For each chunk, add a "Why?" note explaining its significance.

**Example**:
```
┌─────────────────────────┐
│  DEMAND                 │
│  Price ↑ → Quantity ↓   │
│                         │
│  Why: Buyers seek deals │
│       and have limits   │
└─────────────────────────┘
```

#### Step 4: Show Interconnections (I)

Draw arrows between chunks to show relationships.

**Example**:
```
DEMAND ←──────────────→ SUPPLY
   │                      │
   └──────► EQUILIBRIUM ◄─┘
```

#### Step 5: Add Non-Verbal Elements (N)

Use symbols, emojis, or diagrams.

**Example**:
- 📈 for upward trends
- 📉 for downward trends
- ⚖️ for equilibrium
- ⚡ for changes

#### Step 6: Show Direction (D)

Use arrows and hierarchy to show flow.

**Example**:
```
Price too low
      │
      ▼
   SHORTAGE
      │
      ▼
Price rises
      │
      ▼
Returns to equilibrium
```

#### Step 7: Emphasize Importance (E)

Mark importance levels.

**Example**:
- ★★★ = Critical (must know)
- ★★ = Important (should know)
- ★ = Supporting (nice to know)

### Complete GRINDE Map Example

```
═══════════════════════════════════════════════════════════════
                    ★★★ SUPPLY & DEMAND ★★★
═══════════════════════════════════════════════════════════════

┌─────────────────────────┐         ┌─────────────────────────┐
│  ★★ DEMAND (Buyers)     │         │  ★★ SUPPLY (Sellers)    │
│                         │         │                         │
│  📉 Downward slope      │         │  📈 Upward slope        │
│  Price ↑ → Qty ↓        │         │  Price ↑ → Qty ↑        │
│                         │         │                         │
│  Why: Buyers want deals │         │  Why: Sellers want      │
│                         │         │       profit            │
└────────────┬────────────┘         └────────────┬────────────┘
             │                                   │
             └──────────────┬────────────────────┘
                            │
                            ▼
             ┌──────────────────────────────┐
             │  ★★★ EQUILIBRIUM             │
             │  ⚖️ Where curves cross        │
             │                              │
             │  Why: No pressure to change  │
             │       (market clears)        │
             └──────────────────────────────┘

═══════════════════════════════════════════════════════════════
BACKBONE: Opposing forces create balance; deviations self-correct
═══════════════════════════════════════════════════════════════
```

---

## Best Practices

### Do's

1. **Classify BEFORE studying**
   - Know what type of information you're dealing with
   - Apply the right strategy from the start

2. **Build layers in order**
   - Logic first, always
   - Don't skip to memorization

3. **Create maps for concepts**
   - Visual encoding is powerful
   - Connections aid memory

4. **Practice procedures**
   - Actually DO the thing
   - Reading isn't practicing

5. **Critique analogies**
   - Find the limits
   - Don't accept blindly

6. **Minimize flashcards**
   - Only for true R-type
   - After understanding is solid

7. **Check your balance**
   - Don't just consume
   - Digest what you read

### Don'ts

1. **Don't flashcard concepts**
   - Concepts need understanding
   - Flashcards are for arbitrary facts

2. **Don't skip the "why"**
   - Layer 1 is the foundation
   - Everything else depends on it

3. **Don't accept analogies blindly**
   - All analogies have limits
   - Some parts are misleading

4. **Don't treat everything as R-type**
   - Most information can be understood
   - Challenge R classifications

5. **Don't consume without digesting**
   - Reading is just the start
   - Processing makes it stick

6. **Don't memorize before understanding**
   - Memorization without understanding = leaky bucket
   - Understanding makes memorization easier

---

## Frequently Asked Questions

### General Questions

**Q: How is this different from regular flashcards?**

A: Regular flashcard approaches treat all information the same—as things to memorize. PACER recognizes that different types of information need different strategies. Most information should be UNDERSTOOD, not memorized.

**Q: Do I still need Anki/flashcards?**

A: Yes, but much less. Flashcards are for true R-type (Reference) information—arbitrary facts that can't be derived from understanding. Your flashcard count should be minimal.

**Q: How long does it take to see results?**

A: You should notice differences immediately. Information processed with the right strategy feels "stickier." Long-term, you'll spend less time reviewing because you've encoded properly.

### Classification Questions

**Q: What if I'm not sure which type something is?**

A: Ask Claude to classify it! Or use this quick test:
- Can I DO this? → Procedural
- Is this comparing things? → Analogous
- Does this explain WHY/HOW? → Conceptual
- Does this support another idea? → Evidence
- Is this completely arbitrary? → Reference

**Q: Most of my flashcards are for concepts. Is that wrong?**

A: Yes! Concepts should be understood through GRINDE mapping, not memorized with flashcards. If you're flashcarding concepts, you're treating them as R-type when they're actually C-type.

**Q: When should I use flashcards?**

A: Only for true R-type information after you've:
1. Understood the underlying concepts (Layers 1-3)
2. Verified the information is truly arbitrary
3. Confirmed it can't be looked up when needed

### Practical Questions

**Q: I have an exam next week. Should I just make flashcards?**

A: Resist the urge! Even with limited time:
1. Spend 60% on understanding (Layers 1-2)
2. Spend 30% on important details (Layer 3)
3. Spend 10% on memorization (Layer 4)

You'll actually remember more with this approach.

**Q: How do I use this for programming/coding?**

A: Programming is mostly Procedural (P):
- **Practice** writing code, not reading about it
- **Understand** concepts like why recursion works (C)
- **Critique** analogies like "variables are like boxes" (A)
- **Memorize** only syntax that you can't look up (R - minimal)

**Q: This seems like more work. Is it worth it?**

A: It's more work UPFRONT but much less work TOTAL. Think of it like:
- Old way: 1 hour reading + 5 hours reviewing = 6 hours
- PACER way: 1 hour reading + 1 hour processing + 0.5 hours reviewing = 2.5 hours

Proper encoding reduces the need for constant review.

---

## Next Steps

Now that you understand the basics:

1. **Try the Quick Start Guide** (`docs/QUICK_START.md`) - 10 hands-on tutorials
2. **Practice with real content** - Apply PACER to something you're learning
3. **Check your balance regularly** - Don't just consume, digest!
4. **Challenge your R-types** - Most can be understood instead

Remember:

> **Understanding is the shortcut. Memorization is the long way around.**

Happy learning!
