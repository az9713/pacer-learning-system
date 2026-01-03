# PACER Classification Decision Tree

Use this flowchart to systematically classify information.

---

## Quick Decision Flowchart

```
                    ┌─────────────────────────────────────┐
                    │        START: New Information       │
                    └─────────────────┬───────────────────┘
                                      │
                    ┌─────────────────▼───────────────────┐
                    │  Does it tell you HOW to do         │
                    │  something step-by-step?            │
                    └─────────────────┬───────────────────┘
                                      │
                         ┌────────────┴────────────┐
                         │ YES                     │ NO
                         ▼                         ▼
                ┌─────────────────┐    ┌─────────────────────────┐
                │ P - PROCEDURAL  │    │  Is it comparing to     │
                │                 │    │  something you already  │
                │ Protocol:       │    │  know? ("like...",      │
                │ PRACTICE NOW    │    │  "similar to...")       │
                └─────────────────┘    └───────────┬─────────────┘
                                                   │
                                      ┌────────────┴────────────┐
                                      │ YES                     │ NO
                                      ▼                         ▼
                             ┌─────────────────┐    ┌─────────────────────┐
                             │ A - ANALOGOUS   │    │  Is it an abstract  │
                             │                 │    │  theory, principle, │
                             │ Protocol:       │    │  or relationship?   │
                             │ CRITIQUE IT     │    └───────────┬─────────┘
                             └─────────────────┘                │
                                                   ┌────────────┴────────────┐
                                                   │ YES                     │ NO
                                                   ▼                         ▼
                                          ┌─────────────────┐    ┌─────────────────────┐
                                          │ C - CONCEPTUAL  │    │  Is it data, stats, │
                                          │                 │    │  research findings, │
                                          │ Protocol:       │    │  or case studies?   │
                                          │ MIND MAP        │    └───────────┬─────────┘
                                          └─────────────────┘                │
                                                                ┌────────────┴────────────┐
                                                                │ YES                     │ NO
                                                                ▼                         ▼
                                                       ┌─────────────────┐    ┌─────────────────┐
                                                       │ E - EVIDENCE    │    │ R - REFERENCE   │
                                                       │                 │    │                 │
                                                       │ Protocol:       │    │ Protocol:       │
                                                       │ STORE & APPLY   │    │ FLASHCARD/SRS   │
                                                       └─────────────────┘    └─────────────────┘
```

---

## Detailed Decision Questions

### Question 1: Is it Procedural?

**Ask yourself:**
- Does it have steps I can follow?
- Is there a sequence of actions?
- Could I practice this right now?
- Is it a "how-to"?

**Examples that ARE Procedural:**
- Coding tutorials
- Cooking recipes
- Medical examination techniques
- Assembly instructions
- Exercise form guides

**Examples that are NOT Procedural:**
- Explaining why a technique works (Conceptual)
- Statistics about technique effectiveness (Evidence)
- Comparing technique to another (Analogous)

---

### Question 2: Is it Analogous?

**Ask yourself:**
- Is it being compared to something familiar?
- Are words like "like," "similar to," "just as" used?
- Is a metaphor being used to explain?
- Does it build on something I already know?

**Red flags for Analogous:**
- "Think of it as..."
- "It's like when..."
- "Similar to how..."
- "Just as X does Y, so too..."

**Important:** Analogies often appear INSIDE procedural or conceptual content. Extract and critique them separately.

---

### Question 3: Is it Conceptual?

**Ask yourself:**
- Is this a theory or principle?
- Does it explain WHY something works?
- Are there abstract relationships being described?
- Is this foundational knowledge in the field?
- Could I create a mind map of this?

**Conceptual indicators:**
- Definitions of core terms
- Cause-and-effect relationships
- Underlying mechanisms
- Theoretical frameworks
- Principles that apply broadly

---

### Question 4: Is it Evidence?

**Ask yourself:**
- Is this data supporting a concept?
- Are statistics or percentages cited?
- Is a research study being referenced?
- Is this a case study or example proving something?
- Does it validate or demonstrate a principle?

**Evidence indicators:**
- Numbers and percentages
- Study references (author, year)
- "Research shows..."
- Case study descriptions
- Before/after comparisons

---

### Question 5: Is it Reference?

**If you've reached this point, it's likely Reference.**

**Reference characteristics:**
- Arbitrary details (dates, names, constants)
- Things you'd normally look up
- Low standalone conceptual value
- Needed for precision but not understanding

---

## Handling Uncertainty

### When classification is unclear:

1. **Default to Conceptual (C)** - Mind mapping rarely hurts
2. **Check for nested types** - One paragraph may contain multiple types
3. **Ask: "What protocol would help most?"** - Let the protocol guide you
4. **Consider: "Would I look this up or need to know it?"**
   - Look up → Reference
   - Need to know → Likely Conceptual or Procedural

### Priority when multiple types present:

```
HIGH PRIORITY (address first):
├── P - Procedural (practice can't wait)
├── A - Analogous (misconceptions compound)
└── C - Conceptual (foundation for everything)

LOWER PRIORITY (handle after):
├── E - Evidence (supports concepts)
└── R - Reference (offload quickly)
```

---

## Quick Reference Card

| Category | Key Question | Protocol | Priority |
|----------|-------------|----------|----------|
| **P** | HOW do I do this? | Practice now | HIGH |
| **A** | What is this LIKE? | Critique it | HIGH |
| **C** | WHAT is it and WHY? | Mind map | HIGH |
| **E** | What PROVES this? | Store & apply | MEDIUM |
| **R** | Just DETAILS to lookup? | Flashcard/SRS | LOW |
