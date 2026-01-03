# /flashcards - Generate Anki-Compatible Flashcards

Generate flashcards for Reference (R-type) content only.

## Usage

```
/flashcards [content]
```

## Arguments

- `content`: The R-type content to create flashcards for (text or file path)

## Instructions

When the user invokes `/flashcards`, generate Anki-compatible flashcards with proper verification.

### Critical Warning

> ⚠️ Flashcards are for **R-type (Reference) content ONLY**.
>
> Before creating flashcards, verify the content is truly arbitrary and can't be:
> - Understood instead of memorized (→ use `/grinde`)
> - Practiced instead of memorized (→ use `/digest P`)
> - Derived from logic

### Pre-Flight Check

Before generating cards, run this verification:

```markdown
## Flashcard Pre-Flight Check

### Content Analysis

**Content to flashcard**: [brief description]

### Verification Questions

1. **Can this be understood instead of memorized?**
   - [ ] No, it's truly arbitrary (dates, names, constants)
   - [ ] Yes → STOP, use `/grinde` or `/digest C` instead

2. **Is the underlying concept solid?**
   - [ ] Yes, I understand Layers 1-3
   - [ ] No → STOP, build understanding first

3. **Will this be looked up in practice?**
   - [ ] No, must be recalled instantly
   - [ ] Yes → Consider NOT making flashcards

4. **Is this exam-required memorization?**
   - [ ] Yes, exam requires exact recall
   - [ ] No → Strongly reconsider necessity

### Verdict

[ ] ✅ PROCEED - Content is verified R-type
[ ] ❌ ABORT - Use encoding strategies instead
```

### Flashcard Generation (If Verified)

**Output Format**:

```markdown
## Flashcards: [Topic]

### Verification Status: ✅ R-Type Confirmed

### Card Set

---
**Card 1**

**Front**: [Question - clear, specific]

**Back**: [Answer - concise, accurate]

**Context**: [Related concept for organization]

**Tags**: #[topic] #[subtopic] #R-type

---
**Card 2**
...

### Summary Statistics

- **Total Cards**: [N] (smaller is better!)
- **Average Answer Length**: [X words]
- **Concept Coverage**: [What these cards relate to]

### Quality Checks Applied

- ✅ Minimum information principle (atomic cards)
- ✅ No orphan facts (all linked to concepts)
- ✅ Clear, unambiguous questions
- ✅ Single correct answer per card

### Anki Import Format

Copy this TSV for direct Anki import:

```tsv
[front1]	[back1]	#tags
[front2]	[back2]	#tags
```

### Study Recommendations

- **New cards per day**: 5-10 max (to avoid overwhelm)
- **Review schedule**: Daily until mature
- **Integration**: Review after concept study, not instead of

### Related Understanding

Before or while using these flashcards, ensure you've:
- [ ] Created a GRINDE map of the parent topic
- [ ] Understood WHY these facts exist (even if arbitrary)
- [ ] Practiced any related procedures
```

### Card Quality Principles

#### The 20 Rules of Formulating Knowledge

Apply these from Dr. Piotr Wozniak:

1. **Understand first** - Don't flashcard what you don't understand
2. **Start with the big picture** - Context before details
3. **Minimum information** - One fact per card
4. **Optimize wording** - Clear, precise, unambiguous
5. **Use cloze deletion** - For longer material
6. **Use imagery** - Visual memory is powerful
7. **Avoid sets** - Break into individual items
8. **Avoid enumerations** - Don't list memorize
9. **Combat interference** - Distinguish similar items
10. **Personalize** - Add personal connections

### Good vs Bad Cards

**❌ Bad Card (Conceptual - Should Be Understood)**:
```
Q: What is the mechanism of ACE inhibitors?
A: Block angiotensin converting enzyme, reducing angiotensin II
```
This is CONCEPTUAL - should be understood, not flashcarded!

**✅ Good Card (True R-Type)**:
```
Q: What is the typical starting dose of lisinopril?
A: 10mg once daily
```
This is truly ARBITRARY - a number that must be memorized.

**❌ Bad Card (Too Long)**:
```
Q: List all the side effects of ACE inhibitors
A: Cough, hyperkalemia, angioedema, hypotension, renal impairment...
```
Never flashcard lists! Break into individual items or understand patterns.

**✅ Good Card (Atomic)**:
```
Q: Most distinctive side effect of ACE inhibitors?
A: Dry cough (due to bradykinin accumulation)
```

### Encoding Before Retrieval Reminder

```
╔════════════════════════════════════════════════════════════╗
║  FLASHCARDS ARE THE LAST STEP, NOT THE FIRST               ║
║                                                            ║
║  Order of Operations:                                      ║
║  1. Understand (Layers 1-3)     ←── Most content here     ║
║  2. Map with GRINDE             ←── Encoding              ║
║  3. Practice if Procedural      ←── Doing                 ║
║  4. THEN flashcard R-type       ←── Minimal cards         ║
║                                                            ║
║  Flashcards without understanding = leaky bucket          ║
╚════════════════════════════════════════════════════════════╝
```

### Alternative Suggestions

If content fails verification, suggest alternatives:

| If Content Is... | Instead of Flashcards, Use... |
|-----------------|------------------------------|
| Conceptual | `/grinde [topic]` for mind mapping |
| Procedural | `/digest P [content]` for practice |
| Analogous | `/digest A [content]` for critique |
| Connected to concepts | `/digest E [content]` for integration |

## Example

```
/flashcards "Drug dosages for common antibiotics"
```

Output:
```markdown
## Flashcards: Antibiotic Dosages

### Verification Status: ✅ R-Type Confirmed

Dosages are truly arbitrary numbers that must be memorized.
(Assuming you already understand WHY each antibiotic is chosen)

### Card Set

---
**Card 1**

**Front**: Amoxicillin dose for strep throat (adults)?

**Back**: 500mg TID × 10 days

**Context**: First-line beta-lactam for gram-positive

**Tags**: #antibiotics #dosing #strep #R-type

---
**Card 2**

**Front**: Azithromycin dose for community pneumonia?

**Back**: 500mg day 1, then 250mg days 2-5

**Context**: Macrolide Z-pack regimen

**Tags**: #antibiotics #dosing #pneumonia #R-type

---

### Summary Statistics

- **Total Cards**: 2 (demonstrating minimum approach)
- **Parent Understanding Required**: Antibiotic classes, spectrum

### Anki Import Format

```tsv
Amoxicillin dose for strep throat (adults)?	500mg TID × 10 days	#antibiotics #dosing #strep
Azithromycin dose for community pneumonia?	500mg day 1, then 250mg days 2-5	#antibiotics #dosing #pneumonia
```

### Before Using These Cards

Confirm you've completed:
- [ ] GRINDE map of antibiotic classes
- [ ] Understanding of spectrum (gram +/-)
- [ ] Logic of why each drug for each infection
```
