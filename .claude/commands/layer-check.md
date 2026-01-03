# /layer-check - Verify Learning Layer Sequence

Check if you're learning in the proper layer sequence.

## Usage

```
/layer-check [topic]
```

## Arguments

- `topic`: The subject or concept to check layer understanding for

## Instructions

When the user invokes `/layer-check`, assess their understanding across the 4 layers and identify gaps.

### The 4 Layers of Learning

| Layer | Name | Focus | Question |
|-------|------|-------|----------|
| 1 | Logic | WHY | "Why does this work?" |
| 2 | Concepts | WHAT | "What are the major ideas?" |
| 3 | Important Details | WHICH | "Which specifics matter?" |
| 4 | Arbitrary Details | MEMORIZE | "What can only be memorized?" |

**Critical Rule**: Always build layers IN ORDER. Layer 1 → 2 → 3 → 4.

### Layer Check Process

1. **Ask diagnostic questions** for each layer
2. **Assess understanding** based on responses
3. **Identify gaps** and layer violations
4. **Recommend remediation**

### Output Format

```markdown
## Layer Check: [Topic]

### Diagnostic Questions

I'll ask you some questions to check your understanding at each layer.
Please answer honestly - gaps help us know where to focus!

#### Layer 1: Logic (WHY)
1. Why does [topic] work the way it does?
2. What's the underlying mechanism or principle?
3. What problem does [topic] solve?

[Wait for user response, then assess]

#### Layer 2: Concepts (WHAT)
1. What are the 3-5 main components of [topic]?
2. How do these components relate to each other?
3. Can you draw a rough map of the structure?

[Wait for user response, then assess]

#### Layer 3: Important Details (WHICH)
1. What details distinguish [variant A] from [variant B]?
2. What are the key exceptions or edge cases?
3. What specifics matter for application?

[Wait for user response, then assess]

#### Layer 4: Arbitrary Details
1. What truly arbitrary facts do you need to memorize?
2. (Most content should NOT be here)

[Wait for user response, then assess]

### Assessment Results

```
Layer 1 (Logic):     ████████░░ 80% ✅
Layer 2 (Concepts):  ██████░░░░ 60% ⚠️
Layer 3 (Details):   ████░░░░░░ 40% ⚠️
Layer 4 (Arbitrary): ██████████ 100% ⚡ RED FLAG
```

### Gap Analysis

**Strong Layers**: [List]
**Weak Layers**: [List]

### Layer Violation Detection

⚡ **Warning Signs Found**:
- [ ] Knows Layer 4 details but not Layer 1 logic
- [ ] Can recall facts but can't explain WHY
- [ ] Details feel disconnected from concepts
- [ ] Creating flashcards before understanding
- [ ] Can answer recognition but not free recall

### Diagnosis

[One of these:]

**🔴 Inverted Learning**: You know details but not logic.
This is the "leaky bucket" problem - you're trying to memorize
what should be understood.

**🟡 Partial Foundation**: Some layers solid, gaps in others.
Need to strengthen weak layers before progressing.

**🟢 Solid Foundation**: All layers built in order.
Continue building or review for maintenance.

### Remediation Plan

**If Layer 1 is weak**:
1. Step back from details entirely
2. Focus on: "WHY does this work?"
3. Seek the underlying mechanism
4. Use: `/grinde [topic]` focusing on logic

**If Layer 2 is weak**:
1. Don't add more details yet
2. Map the major concepts
3. Identify relationships
4. Use: `/grinde [topic]` for structure

**If Layer 3 is weak**:
1. Good foundation exists
2. Identify which details actually matter
3. Connect details to concepts
4. Use: `/digest C [content]` for integration

**If Layer 4 is overdeveloped**:
1. STOP memorizing
2. Check if items can be understood instead
3. Move items to Layer 3 (understand) or drop
4. Minimize true memorization

### Quick Fix Actions

1. [Immediate action based on diagnosis]
2. [Second priority action]
3. [Follow-up action]

---

## Completed Check Example

After user answers all questions:

```markdown
## Layer Check Results: Photosynthesis

### Layer Scores

```
Layer 1 (Logic):     ████████░░ 80%
Layer 2 (Concepts):  ██████░░░░ 60%
Layer 3 (Details):   ██░░░░░░░░ 20%
Layer 4 (Arbitrary): ████░░░░░░ 40%
```

### What's Working ✅
- You understand WHY photosynthesis happens (energy conversion)
- You know it's a two-stage process

### Gaps Identified ⚠️
- Layer 2: Relationship between light reactions and Calvin cycle unclear
- Layer 3: Missing key details about where each stage occurs

### Red Flags 🚩
- You're trying to memorize enzyme names (Layer 4)
  before fully understanding the concept (Layer 2)

### Recommended Actions

1. **Immediate**: Create GRINDE map of the two stages
   `/grinde photosynthesis stages`

2. **Next**: Add "where" details (thylakoid vs stroma)
   to your concept map

3. **Later**: Only memorize enzyme names IF exam requires them

4. **Don't**: Make flashcards for concepts - understand them instead
```
```

### Rapid Layer Check

For quick assessment, use these single questions:

| Layer | Quick Question | Pass Indicator |
|-------|---------------|----------------|
| 1 | "Explain WHY in one sentence" | Clear mechanism stated |
| 2 | "Draw the concept map from memory" | 3+ concepts with relationships |
| 3 | "What makes X different from Y?" | Specific distinguishing detail |
| 4 | "What's truly arbitrary here?" | Short list, not everything |
