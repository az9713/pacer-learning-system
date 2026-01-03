# /pacer - Quick PACER Classification

Classify content using the PACER framework.

## Usage

```
/pacer [content or file path]
```

## Arguments

- `content`: Text content to classify, OR
- `file path`: Path to a file to analyze

## Instructions

When the user invokes `/pacer`, perform a quick classification of the provided content using the PACER framework:

1. **Read the content** (from argument or file)

2. **Classify each distinct piece of information** into one of:
   - **P** (Procedural): Skills, techniques, methods requiring practice
   - **A** (Analogous): Comparisons, metaphors requiring critique
   - **C** (Conceptual): Core ideas, theories requiring understanding
   - **E** (Evidence): Data, examples supporting concepts
   - **R** (Reference): Arbitrary facts requiring memorization (minimize!)

3. **Output in this format**:

```markdown
## PACER Classification

### Content Summary
[Brief description of what was analyzed]

### Classification Breakdown

| Category | Count | Items |
|----------|-------|-------|
| 🔧 P (Procedural) | X | [List items] |
| 🔄 A (Analogous) | X | [List items] |
| 🧠 C (Conceptual) | X | [List items] |
| 📊 E (Evidence) | X | [List items] |
| 📚 R (Reference) | X | [List items] |

### Dominant Type: [P/A/C/E/R]

### Recommended Digestion
- [Type-appropriate protocol suggestion]
- Use `/digest [TYPE] [content]` to process

### R-Type Warning
[If R count is high, challenge classifications]
```

4. **Apply classification principles**:
   - Challenge every R classification - most can be understood or derived
   - C-type is the most common for educational content
   - Look for hidden procedures (things to practice)
   - Identify analogies that need critique

## Examples

### Example 1: Code Tutorial
```
/pacer "To create a React component, use function syntax or class syntax. The useState hook manages local state. Props are passed from parent to child."
```

Output:
```markdown
## PACER Classification

### Content Summary
React component basics tutorial

### Classification Breakdown

| Category | Count | Items |
|----------|-------|-------|
| 🔧 P (Procedural) | 2 | Creating components, Using useState |
| 🧠 C (Conceptual) | 2 | Component types, Props data flow |
| 📚 R (Reference) | 0 | - |

### Dominant Type: P (Procedural)

### Recommended Digestion
- Practice creating components with both syntaxes
- Practice implementing useState in different scenarios
- Use `/digest P` to generate practice exercises
```

### Example 2: History Passage
```
/pacer "The Treaty of Versailles was signed on June 28, 1919. It imposed harsh penalties on Germany, creating economic hardship that contributed to the rise of Nazi ideology."
```

Output:
```markdown
## PACER Classification

### Content Summary
Post-WWI Treaty of Versailles and consequences

### Classification Breakdown

| Category | Count | Items |
|----------|-------|-------|
| 🧠 C (Conceptual) | 2 | Cause-effect of harsh penalties, Link to Nazi rise |
| 📊 E (Evidence) | 1 | Economic hardship as supporting evidence |
| 📚 R (Reference) | 1 | Date (June 28, 1919) |

### Dominant Type: C (Conceptual)

### Recommended Digestion
- Map the causal chain: Treaty → Penalties → Hardship → Ideology
- Use `/grinde` to create concept map of causes and effects
- Date only needs memorization if exam requires it

### R-Type Warning
The date can often be derived from context (end of WWI + negotiation time).
Consider if you truly need to memorize it vs. understanding the sequence.
```
