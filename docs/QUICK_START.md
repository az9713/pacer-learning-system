# PACER Learning System - Quick Start Guide

## 10 Quick Wins: Hands-On Tutorials

This guide gives you 10 simple exercises to master the PACER Learning System. Each takes just 5-10 minutes and teaches you a core concept.

---

## Before You Begin

### Starting Claude Code

1. Open your terminal (Command Prompt, Terminal, or PowerShell)

2. Navigate to the project folder:
   ```bash
   cd path/to/pacer_bestpartnerstv
   ```

3. Start Claude:
   ```bash
   claude
   ```

4. You're ready! Type your messages and press Enter.

---

## Tutorial 1: Your First PACER Classification

**Goal**: Learn to classify content into P/A/C/E/R types.

**Time**: 5 minutes

### Step 1: Give Claude some content

Type this:

```
Classify this learning content:

"To tie your shoelaces, first cross the laces, loop one under,
pull tight, make two bunny ears, cross them, push one through
the hole, and pull tight."
```

### Step 2: Read the classification

Claude will respond with something like:

> **Classification**: 🔧 Procedural (P)
>
> **Why**: This is a skill with steps to follow. You need to PRACTICE it.
>
> **Recommendation**: Don't make flashcards! Practice tying shoes instead.

### What You Learned

- Content about "how to do something" is **Procedural**
- Procedures need **practice**, not memorization
- Claude automatically applies the PACER skill

**Quick Win!** You can now recognize Procedural content.

---

## Tutorial 2: Classify Conceptual Content

**Goal**: Distinguish Conceptual from Reference content.

**Time**: 5 minutes

### Step 1: Give Claude conceptual content

Type this:

```
Classify this content:

"Gravity is the force of attraction between objects with mass.
The larger the mass, the stronger the gravitational pull.
This is why Earth pulls objects toward its center."
```

### Step 2: Read the classification

Claude will respond:

> **Classification**: 🧠 Conceptual (C)
>
> **Why**: This explains WHY and HOW gravity works. It's not arbitrary.
>
> **Recommendation**: Create a mind map connecting mass → force → attraction.

### Step 3: Compare with Reference content

Now try:

```
Classify this content:

"The gravitational constant G = 6.674 × 10⁻¹¹ N⋅m²/kg²"
```

Claude will respond:

> **Classification**: 📚 Reference (R)
>
> **Why**: This is an arbitrary constant. There's no "why" for this specific number.
>
> **Recommendation**: Only memorize if required. Usually you can look this up.

### What You Learned

- Explanations of "why" are **Conceptual** → understand them
- Arbitrary numbers are **Reference** → memorize only if necessary
- Most content that seems like "facts to memorize" is actually Conceptual!

**Quick Win!** You can distinguish Conceptual from Reference content.

---

## Tutorial 3: Create Your First GRINDE Map

**Goal**: Create a visual mind map using GRINDE principles.

**Time**: 10 minutes

### Step 1: Request a map

Type this:

```
Create a GRINDE mind map for "Why the sky is blue"
```

### Step 2: Study the output

Claude will create something like:

```
═══════════════════════════════════════════════════════════════
                    ★★★ WHY THE SKY IS BLUE ★★★
═══════════════════════════════════════════════════════════════

┌─────────────────────────────────────┐
│  ★★ SUNLIGHT                        │
│                                     │
│  ☀️ White light = all colors        │
│  (rainbow spectrum)                 │
│                                     │
│  Why: Starting point - light        │
│       enters atmosphere             │
└────────────────┬────────────────────┘
                 │
                 │ hits atmosphere
                 ▼
┌─────────────────────────────────────┐
│  ★★★ SCATTERING                     │
│                                     │
│  Particles scatter shorter          │
│  wavelengths MORE                   │
│                                     │
│  Blue = short wavelength ← KEY!     │
│  Red = long wavelength              │
│                                     │
│  Why: Rayleigh scattering           │
└────────────────┬────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────┐
│  ★ RESULT                           │
│                                     │
│  Blue light bounces around sky      │
│  We see blue in all directions      │
└─────────────────────────────────────┘

═══════════════════════════════════════════════════════════════
BACKBONE: Short wavelengths (blue) scatter more than long (red)
═══════════════════════════════════════════════════════════════
```

### Step 3: Identify GRINDE elements

Look for:
- **G**rouped: Three clear boxes
- **R**eflective: "Why" notes explain significance
- **I**nterconnected: Arrows show flow
- **N**on-verbal: ☀️ emoji, visual layout
- **D**irectional: Top-to-bottom progression
- **E**mphasized: ★★★ marks most important concept

### What You Learned

- GRINDE maps are visual and structured
- The "backbone" captures the core insight
- Maps encode information better than text lists

**Quick Win!** You can create and read GRINDE maps.

---

## Tutorial 4: Critique an Analogy

**Goal**: Learn to properly handle Analogous (A) content.

**Time**: 5 minutes

### Step 1: Give Claude an analogy

Type this:

```
Help me digest this Analogous content:

"The brain is like a computer - it processes input, stores memory,
and produces output."
```

### Step 2: Read the critique

Claude will provide:

> **Analogy Critique: "The brain is like a computer"**
>
> ✅ **Strengths (Keep)**:
> - Both process information
> - Both have input and output
> - Both have memory storage
>
> ⚠️ **Limitations (Be Careful)**:
> - Computers are digital; brains are analog
> - Brains change physically when learning; computers don't
> - Brains are massively parallel; most computers are serial
>
> ❌ **Misleading (Discard)**:
> - Implies consciousness is just computation
> - Suggests memory is stored in specific locations (it isn't)
> - Implies brains can be "rebooted" or "reformatted"
>
> **Refined Understanding**:
> Both process information, but through completely different mechanisms.
> Don't expect computer troubleshooting to work on brains!

### What You Learned

- Analogies are **partially true** and **partially misleading**
- Always critique: What works? What breaks down?
- Extract the useful parts, discard the misleading parts

**Quick Win!** You can critically evaluate analogies.

---

## Tutorial 5: Check Your Learning Layers

**Goal**: Verify you're building knowledge in the right order.

**Time**: 5 minutes

### Step 1: Request a layer check

Type this:

```
Check my learning layers for "How vaccines work"
```

### Step 2: Answer the questions

Claude will ask questions for each layer:

> **Layer 1 (Logic)**: Can you explain WHY vaccines work?
>
> **Layer 2 (Concepts)**: What are the main components (immune system, antigens, antibodies)?
>
> **Layer 3 (Details)**: What distinguishes live attenuated from inactivated vaccines?
>
> **Layer 4 (Arbitrary)**: What specific vaccine schedules must you memorize?

### Step 3: Identify your gaps

If you can't answer Layer 1, you have a foundation problem!

**Example gap**: "I know vaccine schedules (Layer 4) but can't explain why vaccines work (Layer 1)."

**Fix**: Go back to Layer 1 before memorizing schedules.

### What You Learned

- Layers MUST be built in order: 1 → 2 → 3 → 4
- Knowing Layer 4 without Layer 1 = fragile knowledge
- Layer checks reveal where to focus

**Quick Win!** You can diagnose your own learning gaps.

---

## Tutorial 6: Practice a Procedure

**Goal**: Learn the right way to handle Procedural content.

**Time**: 10 minutes

### Step 1: Give Claude a procedure

Type this:

```
Help me digest this Procedural content:

"To calculate compound interest: A = P(1 + r/n)^(nt)
where P is principal, r is annual rate, n is compounds per year,
t is time in years."
```

### Step 2: Get practice exercises

Claude will provide:

> **Procedural Digestion: Compound Interest Calculation**
>
> **Core Steps**:
> 1. Identify values: P, r, n, t
> 2. Convert rate to decimal (5% → 0.05)
> 3. Calculate (1 + r/n)
> 4. Raise to power (nt)
> 5. Multiply by P
>
> **Practice Exercise 1 (Basic)**:
> P = $1000, r = 5%, n = 1 (annual), t = 2 years
> Calculate A.
>
> [Solution: A = 1000(1 + 0.05/1)^(1×2) = 1000(1.05)² = $1102.50]
>
> **Practice Exercise 2 (Intermediate)**:
> P = $5000, r = 4%, n = 12 (monthly), t = 3 years
> Calculate A.

### Step 3: Actually do the exercises

Don't just read—calculate! Grab a calculator and work through.

### What You Learned

- Procedures need PRACTICE, not flashcards
- Start simple, increase difficulty
- Reading about a procedure ≠ knowing it

**Quick Win!** You know how to properly learn procedures.

---

## Tutorial 7: Connect Evidence to Concepts

**Goal**: Learn to integrate Evidence (E) with parent concepts.

**Time**: 5 minutes

### Step 1: Give Claude evidence

Type this:

```
Help me digest this Evidence:

"In a 2019 study, students who used spaced repetition retained
85% of material after 30 days, compared to 20% for massed practice."
```

### Step 2: See the integration

Claude will respond:

> **Evidence Integration**
>
> **Parent Concept**: Spaced repetition enhances long-term retention
>
> **The Evidence**:
> - Type: Study data
> - Finding: 85% vs 20% retention
> - Timeframe: 30 days
>
> **Connection**:
> This evidence SUPPORTS the concept that spacing out practice is
> more effective than cramming (massed practice).
>
> **Integration into Map**:
> ```
> Spaced Repetition (Concept)
>        │
>        └── 📊 85% vs 20% retention (Evidence)
>                └── Supports: spacing works!
> ```
>
> **Don't**: Memorize "85%" in isolation
> **Do**: Remember this supports the spacing effect

### What You Learned

- Evidence supports concepts; don't memorize it alone
- Always link evidence to its parent concept
- Statistics are meaningless without context

**Quick Win!** You can properly integrate supporting evidence.

---

## Tutorial 8: The Flashcard Reality Check

**Goal**: Learn when flashcards ARE and AREN'T appropriate.

**Time**: 5 minutes

### Step 1: Request flashcards for conceptual content

Type this:

```
Create flashcards for:

"Photosynthesis converts light energy to chemical energy. Plants
capture sunlight in chloroplasts, split water molecules, and use
the energy to combine CO2 into glucose."
```

### Step 2: Get challenged

Claude will push back:

> ⚠️ **Flashcard Pre-Flight Check: FAILED**
>
> This content is **Conceptual (C)**, not Reference (R).
>
> **Why this shouldn't be flashcarded**:
> - "Light → chemical energy" is a mechanism to UNDERSTAND
> - The process has logical steps to COMPREHEND
> - This would create surface-level recognition, not understanding
>
> **Instead, you should**:
> - Create a GRINDE map of the photosynthesis process
> - Trace the energy transformation step by step
> - Understand WHY each step happens
>
> **If you still want cards**: Use them to TEST understanding,
> not as the primary learning method.

### Step 3: Try with true R-type content

```
Create flashcards for:

"Chlorophyll a absorbs at 430nm and 662nm wavelengths."
```

Now Claude will create cards:

> ✅ **Verified R-Type**: These specific wavelengths are arbitrary.
>
> **Card 1**:
> Q: What wavelengths does chlorophyll a absorb?
> A: 430nm and 662nm
> Context: Relates to why plants are green (absorb red/blue)

### What You Learned

- Claude challenges inappropriate flashcard requests
- Concepts → understanding, not flashcards
- Only true R-type gets flashcards

**Quick Win!** You'll never over-flashcard again.

---

## Tutorial 9: Check Your Learning Balance

**Goal**: Monitor consumption vs digestion.

**Time**: 5 minutes

### Step 1: Simulate a reading session

Tell Claude:

```
I just spent 2 hours reading a textbook chapter on cell biology.
I highlighted key points and took some notes. Check my learning balance.
```

### Step 2: Get the assessment

Claude will analyze:

> **Learning Balance Check**
>
> **Consumption**: HIGH
> - 2 hours of reading
> - Highlighting (passive)
> - Note-taking (semi-active)
>
> **Digestion**: LOW
> - No mind maps created
> - No practice exercises
> - No self-explanation
>
> ```
> CONSUMPTION ████████████░░░░░░ 80%
> DIGESTION   ████░░░░░░░░░░░░░░ 20%
> ```
>
> **Status**: ⚠️ IMBALANCED
>
> **Recommendations**:
> 1. **Stop consuming new content**
> 2. Create GRINDE maps for major concepts
> 3. Identify P/A/C/E/R types in your notes
> 4. Don't read more until you've processed this

### Step 3: Plan your digestion

Ask Claude to help:

```
Help me create a GRINDE map for cell membrane structure
```

### What You Learned

- Consuming without digesting = wasted time
- Balance check reveals imbalances
- Must process before consuming more

**Quick Win!** You can self-monitor your learning balance.

---

## Tutorial 10: The Complete Workflow

**Goal**: Put it all together with a real learning task.

**Time**: 15 minutes

### Step 1: Start with classification

Type this:

```
I'm learning about Newton's Laws of Motion. Here's the content:

1. An object at rest stays at rest unless acted upon by a force.
2. F = ma (Force equals mass times acceleration).
3. For every action, there's an equal and opposite reaction.
4. Newton published the Principia in 1687.
5. "Objects in motion are like rolling balls - they keep going."

Classify this using PACER and tell me how to learn each part.
```

### Step 2: Review the classification

Claude will break it down:

> **PACER Classification**:
>
> | Content | Type | Action |
> |---------|------|--------|
> | First Law (inertia) | C | Create map |
> | F = ma | P | Practice calculations |
> | Third Law (action-reaction) | C | Create map |
> | "1687" | R | Memorize (only if needed) |
> | "Rolling balls" analogy | A | Critique it |

### Step 3: Create a mind map

```
Create a GRINDE map connecting Newton's three laws
```

### Step 4: Practice the procedure

```
Help me practice F = ma calculations with 3 exercises
```

### Step 5: Critique the analogy

```
Critique the analogy: "Objects in motion are like rolling balls"
```

### Step 6: Final check

```
Check my learning layers for Newton's Laws
```

### What You Learned

The complete workflow:
1. **Classify** content (PACER)
2. **Map** conceptual content (GRINDE)
3. **Practice** procedural content
4. **Critique** analogies
5. **Minimize** flashcards (true R-type only)
6. **Verify** with layer check

**Quick Win!** You can apply the full PACER system to any topic.

---

## Summary: Your 10 Quick Wins

| Tutorial | What You Learned |
|----------|-----------------|
| 1 | Recognize Procedural content |
| 2 | Distinguish Conceptual from Reference |
| 3 | Create GRINDE mind maps |
| 4 | Critique analogies properly |
| 5 | Check learning layers |
| 6 | Practice procedures correctly |
| 7 | Connect evidence to concepts |
| 8 | Know when to use flashcards |
| 9 | Monitor learning balance |
| 10 | Apply the complete workflow |

---

## What's Next?

Now that you've completed these quick wins:

1. **Apply to your real learning** - Use PACER on actual study material
2. **Read the full User Guide** - `docs/USER_GUIDE.md` for deeper understanding
3. **Check the Troubleshooting Guide** - `docs/TROUBLESHOOTING.md` if you get stuck
4. **Build the habit** - Use PACER every time you learn something new

---

## Quick Reference Card

### The PACER Types

| Type | Symbol | Action | NOT This |
|------|--------|--------|----------|
| **P**rocedural | 🔧 | Practice | Flashcards |
| **A**nalogous | 🔄 | Critique | Accept blindly |
| **C**onceptual | 🧠 | Map | Memorize |
| **E**vidence | 📊 | Connect | Isolate |
| **R**eference | 📚 | Memorize | (Last resort) |

### The 4 Layers (In Order!)

1. **Logic** - WHY does it work?
2. **Concepts** - WHAT are the ideas?
3. **Details** - WHICH specifics matter?
4. **Arbitrary** - What must be memorized?

### The Golden Rules

1. Understand before memorizing
2. Practice procedures, don't flashcard them
3. Critique analogies, don't accept blindly
4. Minimize R-type classification
5. Balance consumption with digestion

---

**Congratulations!** You've completed the Quick Start Guide. Go learn something! 🎓
