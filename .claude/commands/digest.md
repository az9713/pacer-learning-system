# /digest - Execute Digestion Protocol

Process content using the appropriate PACER digestion protocol.

## Usage

```
/digest [P|A|C|E|R] [content]
```

## Arguments

- `type`: One of P, A, C, E, or R (required)
- `content`: The content to digest (text or file path)

## Instructions

When the user invokes `/digest`, execute the type-specific digestion protocol:

---

### `/digest P [content]` - Procedural Digestion

**Goal**: Convert knowledge into executable skill through practice

**Output Format**:

```markdown
## Procedural Digestion: [Skill Name]

### Core Procedure
1. [Step 1]
2. [Step 2]
3. [Step 3]
...

### Decision Points
- If [condition]: [action]
- If [condition]: [action]

### Practice Exercises

#### Level 1: Basic (Do First)
**Exercise 1.1**: [Simple application]
- Setup: [Context]
- Task: [What to do]
- Solution: [Answer]

**Exercise 1.2**: [Another simple one]
...

#### Level 2: Intermediate
**Exercise 2.1**: [Moderate complexity]
...

#### Level 3: Advanced
**Exercise 3.1**: [Complex scenario with edge cases]
...

### Common Mistakes
❌ [Mistake 1]: [Why it happens] → [How to avoid]
❌ [Mistake 2]: [Why it happens] → [How to avoid]

### Practice Schedule
- Day 1: Exercises 1.1-1.3
- Day 3: Exercises 2.1-2.2
- Day 7: Exercises 3.1, review weak areas
```

---

### `/digest A [content]` - Analogous Digestion

**Goal**: Extract accurate understanding, discard misleading parts

**Output Format**:

```markdown
## Analogy Critique: "[Analogy Statement]"

### The Mapping
| Familiar (Source) | → | Learning (Target) |
|-------------------|---|-------------------|
| [Element 1] | → | [Mapped element] |
| [Element 2] | → | [Mapped element] |

### Strengths ✅ (Keep These)
- **[Mapping 1]**: [Why this works well]
- **[Mapping 2]**: [Why this is accurate]

### Limitations ⚠️ (Be Careful)
- **[Limit 1]**: [Where the analogy breaks down]
- **[Limit 2]**: [What it oversimplifies]

### Misleading Aspects ❌ (Discard)
- **[Problem 1]**: [What NOT to transfer from this analogy]
- **[Problem 2]**: [Misconception it might create]

### Refined Understanding
After critique, the accurate takeaway is:
[Clear statement of what to actually understand]

### Better Analogy?
[Suggest a more accurate analogy if one exists]
```

---

### `/digest C [content]` - Conceptual Digestion

**Goal**: Create deeply encoded understanding through mapping

**Output Format**:

```markdown
## Concept Digestion: [Topic]

### Layer 1: Logic (The WHY)
[Foundational understanding - why does this work/exist?]

### Layer 2: Major Concepts
[Mind map structure - see /grinde for full map]

┌─────────────────┐
│ Core Concept    │
└────────┬────────┘
    ┌────┴────┐
    ▼         ▼
[Sub 1]    [Sub 2]

### Layer 3: Key Details
- [Important detail that crystallizes understanding]
- [Exception that matters]
- [Distinguishing characteristic]

### Elaboration Questions
1. Why does [X] happen?
2. What would change if [Y]?
3. How does this connect to [prior knowledge]?

### Self-Explanation
Explain this concept as if teaching someone:
"[Template for the user to complete]"

### Understanding Verification
- [ ] Can I explain the WHY without notes?
- [ ] Can I draw the concept map from memory?
- [ ] Can I apply this to a new scenario?
```

---

### `/digest E [content]` - Evidence Digestion

**Goal**: Attach evidence to concepts for reinforcement

**Output Format**:

```markdown
## Evidence Integration

### The Evidence
**Type**: [Example | Data | Study | Case]
**Content**: [The actual evidence]
**Source**: [Where it comes from]

### Parent Concept
This evidence supports: **[Concept Name]**

Connection to concept:
[Explain HOW this evidence supports the concept]

### Strength Assessment
[Strong | Moderate | Weak] because [reason]

### Integration
Add to your concept map:

[Parent Concept]
       │
       └── 📊 [This evidence]
              └── [Key takeaway]

### Memory Hook
[A memorable way to remember this evidence with its concept]
```

---

### `/digest R [content]` - Reference Digestion

**Goal**: Efficient minimal memorization for truly arbitrary info

**IMPORTANT**: First verify this is truly R-type!

**Output Format**:

```markdown
## Reference Digestion: [Topic]

### R-Type Verification
Before making flashcards, confirm:
- [ ] This CANNOT be derived from logic
- [ ] This MUST be recalled (can't look up when needed)
- [ ] This is genuinely arbitrary (no pattern)
- [ ] I already understand the underlying concepts

⚠️ If any box is unchecked, consider `/digest C` instead!

### Minimal Flashcard Set

**Card 1**
Front: [Question]
Back: [Answer]
Context: [Related concept]
Tags: #[topic] #[subtopic]

**Card 2**
...

### Total Cards: [N]
(Target: as few as possible!)

### Mnemonics (if helpful)
- [Memory device for remembering]

### Anki Import Format
```csv
[question]	[answer]	[tags]
```

### Spaced Repetition Schedule
- New cards: 5-10 per day max
- Review: Daily until stable
- Intervals: Default Anki settings
```

---

## Type Detection

If user doesn't specify type, ask:

```markdown
I can help digest this content. What type is it?

- **P** - It's a procedure/skill to practice
- **A** - It's an analogy to evaluate
- **C** - It's a concept to understand
- **E** - It's evidence supporting a concept
- **R** - It's arbitrary info to memorize (verify this is truly arbitrary!)

Or use `/pacer [content]` first to classify automatically.
```
