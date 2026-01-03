# /balance-check - Check Learning Balance

Assess the balance between content consumption and digestion.

## Usage

```
/balance-check
```

## Arguments

None required. Analyzes the current session or recent learning activity.

## Instructions

When the user invokes `/balance-check`, assess their consumption vs digestion balance:

### The Balance Principle

> "Lots of retrieval without proper encoding is like filling a leaky bucket faster."

Learning requires **balance**:
- **Consumption**: Reading, watching, listening, absorbing new information
- **Digestion**: Processing, mapping, practicing, encoding information

Imbalance leads to:
- Too much consumption → information overload, poor retention
- Too much digestion → diminishing returns, need fresh input

### Session Analysis

**Check for signs of imbalance**:

| Consumption Indicators | Digestion Indicators |
|----------------------|---------------------|
| Reading files | Creating mind maps |
| Fetching web content | Generating practice exercises |
| Watching/processing videos | Critiquing analogies |
| Copying/highlighting | Explaining concepts |
| Passive questions | Active practice |

### Output Format

```markdown
## Learning Balance Check

### Session Analysis

**Content Consumed**:
- [List of materials read/viewed]
- Approximate volume: [Low/Medium/High]

**Digestion Activities**:
- [List of encoding activities performed]
- Approximate depth: [None/Shallow/Deep]

### Balance Assessment

```
CONSUMPTION ████████████░░░░░░ 65%
DIGESTION   ████░░░░░░░░░░░░░░ 20%
```

**Status**: ⚠️ IMBALANCED / ✅ BALANCED

### Imbalance Type

[ ] 📥 Over-consumption (too much input, not enough processing)
[ ] 🔄 Over-digestion (diminishing returns, need fresh input)
[ ] ✅ Balanced (good ratio of input to processing)

### Recommendations

**If Over-Consuming**:
1. Stop new content intake
2. Process what you have using:
   - `/grinde [topic]` for conceptual content
   - `/digest P [content]` for procedures
   - `/digest A [content]` for analogies
3. Don't consume more until current content is encoded

**If Over-Digesting**:
1. You've processed current material well
2. Consider introducing new related content
3. Build on solid foundation

**If Balanced**:
1. Continue current pattern
2. Consider depth check: Is digestion quality high?

### The Leaky Bucket Reminder

```
Poor Encoding:                Strong Encoding:

  Info │   ┌───┐               Info │   ┌───────┐
  In   │   │   │ ← small           │   │       │ ← large
   ↓   │   │💧💧│                ↓   │   │💧💧💧💧│
       │   └─┬─┘ leaking           │   └───┬───┘
       │   💧💧💧                   │      💧  slow loss

Result: constant re-learning   Result: lasting memory
```

### Next Actions

1. [Specific action based on balance status]
2. [Second recommendation]
3. [Third recommendation]

Use `/digest` commands to process undigested content.
```

### Quick Balance Rules

| Consumption Amount | Required Digestion |
|-------------------|-------------------|
| 1 article/chapter | At least 1 GRINDE map |
| 1 tutorial | Practice exercises |
| Multiple sources | Integrated summary |
| New concept | Full Layer 1-3 encoding |

### Warning Signs

**Stop consuming if**:
- You can't explain what you just read
- Information feels like a blur
- You're highlighting without understanding
- Details seem random and disconnected

**Resume consuming after**:
- You can teach the material
- Concepts connect to prior knowledge
- You've practiced applicable skills
- Mind map is complete and understood

## Example Output

```markdown
## Learning Balance Check

### Session Analysis

**Content Consumed**:
- `docs/api-reference.md` - Read
- Web article on authentication patterns - Fetched
- 3 Stack Overflow answers - Browsed

Approximate volume: **Medium-High**

**Digestion Activities**:
- Brief discussion of concepts
- No mind maps created
- No practice exercises completed

Approximate depth: **Shallow**

### Balance Assessment

```
CONSUMPTION ████████████░░░░░░ 65%
DIGESTION   ████░░░░░░░░░░░░░░ 20%
```

**Status**: ⚠️ IMBALANCED

### Imbalance Type

[x] 📥 Over-consumption (too much input, not enough processing)
[ ] 🔄 Over-digestion
[ ] ✅ Balanced

### Recommendations

You've consumed significant content without proper encoding.

**Immediate Actions**:
1. **Stop** reading new content
2. Run `/pacer` on the API reference to classify content types
3. Run `/grinde authentication` to map the authentication concepts
4. Run `/digest C` for the main authentication patterns

**Before consuming more**:
- [ ] Create GRINDE map for each major concept
- [ ] Explain the authentication flow without notes
- [ ] Practice implementing at least one pattern

### Next Actions

1. `/grinde authentication patterns`
2. `/digest P` for any code examples you want to remember
3. Take a break, then test recall
```
