# Implementation Architecture: Justin Sung's Learning Systems in Claude Code

## Overview

Based on Claude Code's extension mechanisms and Justin Sung's learning frameworks, here's the recommended architecture for implementing the PACER system and related methodologies.

---

## Extension Mechanism Comparison

| Mechanism | Trigger | Best For | Context |
|-----------|---------|----------|---------|
| **Skills** | Auto (Claude decides) | Knowledge, guidance, how-to | Shared with main conversation |
| **Subagents** | Auto or explicit | Specialized tasks, isolation | Separate context window |
| **Slash Commands** | Explicit (`/command`) | Frequently-used prompts | Injected into conversation |
| **Hooks** | Event-based | Automation, validation | Background execution |

---

## Recommended Architecture

### Layer 1: Core Skills (Auto-Triggered Knowledge)

Skills are **model-invoked** - Claude automatically applies them when relevant. Perfect for embedding Sung's methodologies as "expert knowledge."

#### Skill 1: `pacer-classifier`
**Purpose**: Automatically classify information into P/A/C/E/R categories

```
~/.claude/skills/pacer-classifier/
├── SKILL.md
├── examples.md
└── decision-tree.md
```

**SKILL.md**:
```yaml
---
name: pacer-classifier
description: Classifies information into PACER categories (Procedural, Analogous, Conceptual, Evidence, Reference) and recommends appropriate digestion protocols. Use when learning new material, studying, reading, or processing information.
---

# PACER Information Classifier

When processing learning content, classify each piece of information:

## Classification Framework

### P - Procedural ("How")
- Instructions for executing tasks
- Step-by-step processes
- Coding syntax, clinical techniques
- **Protocol**: Practice immediately

### A - Analogous ("Like")
- Resembles existing knowledge
- Patterns you've seen before
- **Protocol**: Critique the analogy

### C - Conceptual ("What")
- Core theories and principles
- Abstract relationships
- The bulk of academic learning
- **Protocol**: Create mind map

### E - Evidence ("Proof")
- Data, statistics, case studies
- Concrete validation of concepts
- **Protocol**: Store & Rehearse (Application)

### R - Reference ("Minutiae")
- Arbitrary details (dates, constants)
- Low conceptual value
- **Protocol**: Store & Rehearse (Flashcards)

## Output Format
For each piece of content, provide:
1. **Category**: [P/A/C/E/R]
2. **Reasoning**: Why this classification
3. **Protocol**: Recommended digestion action
4. **Priority**: High (P/A/C) or Low (E/R)
```

#### Skill 2: `grinde-mapper`
**Purpose**: Guide creation of GRINDE-style mind maps for encoding

```yaml
---
name: grinde-mapper
description: Creates GRINDE-style mind maps for higher-order learning. Use when organizing concepts, creating study notes, mapping relationships between ideas, or visualizing knowledge structures.
allowed-tools: Read, Write, Edit
---

# GRINDE Mind Map Creator

## The 6 Principles

### G - Grouped
- Organize information into logical chunks
- Use boxes or visual containers
- Keep related concepts together

### R - Reflective
- Ask: "Why does this matter?"
- Ask: "How does this connect to what I know?"
- Pause to reflect, don't just transcribe

### I - Interconnected
- Draw connections between concepts
- Look for relationships across groups
- Create a web, not isolated islands

### N - Non-verbal
- Use symbols, doodles, sketches
- Minimize words
- Visual representation > text

### D - Directional
- Show cause and effect
- Indicate flow and processes
- Arrows should have meaning

### E - Emphasized
- Highlight the most important concepts
- Create visual hierarchy
- Identify the "backbone" of the topic

## Output Format
Generate a text-based representation showing:
1. Central concept
2. Major chunks (grouped)
3. Key relationships (interconnected)
4. Directional flows
5. Emphasis indicators (★ for critical concepts)
```

#### Skill 3: `layer-learning`
**Purpose**: Enforce proper learning sequence (Logic → Concepts → Details)

```yaml
---
name: layer-learning
description: Guides learning through the 4 layers in proper sequence. Use when studying complex topics, building understanding, or when user jumps to details prematurely.
---

# 4 Layers of Learning Framework

## The Correct Sequence

### Layer 1: Logic (Foundation) 🏗️
**Must master FIRST**
- WHY things work the way they do
- Foundational logical framework
- The "engine" of the topic

### Layer 2: Concepts 📚
**Build AFTER logic**
- Main ideas fleshed out
- Depth and nuance
- Mind maps invaluable here

### Layer 3: Important Details 📝
**AFTER concepts are solid**
- Key specifics that crystallize understanding
- Integrate with bigger picture

### Layer 4: Arbitrary Details 🔢
**LAST and LEAST**
- Rarely crucial
- Can clutter if handled too early
- Use flashcards/SRS if needed

## Anti-Pattern Detection
If user is focusing on Layer 4 before Layer 1, gently redirect:
"I notice we're looking at specific details. Let's first establish the logical foundation..."
```

#### Skill 4: `encoding-first`
**Purpose**: Promote encoding over retrieval strategies

```yaml
---
name: encoding-first
description: Guides efficient learning by prioritizing encoding over retrieval. Use when discussing study strategies, flashcards, active recall, or spaced repetition.
---

# Encoding-First Learning Strategy

## Core Principle
"Lots of retrieval without proper encoding is like filling a leaky bucket faster."

## When User Mentions Flashcards/Active Recall
Suggest encoding FIRST:
1. Create GRINDE map to build understanding
2. Identify key relationships
3. Connect to existing knowledge
4. THEN use flashcards for Reference-type info

## Encoding Techniques (High Priority)
- Mind mapping (GRINDE method)
- Elaboration (connecting to prior knowledge)
- Chunking (grouping related info)
- Higher-order thinking (analyze, evaluate, create)

## Retrieval Techniques (Lower Priority)
- Flashcards (for R-type only)
- Active recall (after encoding)
- Spaced repetition (maintenance, not primary learning)

## Key Message
If encoding is good, forgetting curve is slow → fewer reviews needed.
```

---

### Layer 2: Subagents (Specialized Tasks)

Subagents run in **separate context** and can be delegated complex tasks.

#### Subagent 1: `learning-analyzer`
**Purpose**: Deep analysis of learning content, classification, and strategy

```markdown
# .claude/agents/learning-analyzer.md
---
name: learning-analyzer
description: Analyzes learning content using PACER classification, recommends optimal study strategies. Use PROACTIVELY when user is studying or learning new material.
tools: Read, Grep, Glob, WebFetch
model: sonnet
skills: pacer-classifier, layer-learning
---

You are a learning science expert specializing in Justin Sung's PACER methodology.

When analyzing learning content:

1. **Classify** all information using PACER (P/A/C/E/R)
2. **Structure** content using the 4 Layers of Learning
3. **Recommend** specific digestion protocols for each section
4. **Identify** opportunities for analogies to existing knowledge
5. **Flag** content that should be offloaded (E/R types)

Output a structured learning plan with:
- Information classification breakdown
- Recommended study sequence
- Time allocation suggestions
- Encoding vs retrieval balance
```

#### Subagent 2: `digestion-coach`
**Purpose**: Guide user through active digestion protocols

```markdown
# .claude/agents/digestion-coach.md
---
name: digestion-coach
description: Coaches user through PACER digestion protocols (Practice, Critique, Map, Store). Use when user has consumed content and needs to process it.
tools: Read, Write, Edit, Bash
model: sonnet
skills: grinde-mapper, encoding-first
---

You are a learning coach guiding active digestion.

Based on information type, execute the appropriate protocol:

## For Procedural (P)
- Generate practice exercises
- Create hands-on application tasks
- Do NOT let user just read - they must DO

## For Analogous (A)
- Prompt critical analysis questions
- "How is X like Y? Where does it break down?"
- Challenge the analogy rigorously

## For Conceptual (C)
- Guide GRINDE map creation
- Identify relationships and connections
- Build the knowledge network

## For Evidence (E)
- Format for second-brain storage
- Create application scenarios
- Link to relevant concepts

## For Reference (R)
- Generate Anki-style flashcards
- Format for SRS systems
- Keep minimal, offload quickly
```

#### Subagent 3: `learner-diagnostic`
**Purpose**: Assess user's learning approach across 5 dimensions

```markdown
# .claude/agents/learner-diagnostic.md
---
name: learner-diagnostic
description: Assesses learning approach across 5 dimensions (Deep Processing, Self-Regulation, Retrieval, Self-Management, Mindset). Use when user wants to understand their learning style or improve study habits.
tools: Read, Bash
model: sonnet
---

You are a learning diagnostician assessing across 5 dimensions:

## 1. Deep Processing
- How well do they analyze and connect concepts?
- Do they seek relationships or memorize in isolation?

## 2. Self-Regulation
- Do they monitor their own learning?
- Can they adapt strategies when something isn't working?

## 3. Retrieval
- What retrieval strategies do they use?
- Is retrieval balanced with encoding?

## 4. Self-Management
- Time management habits
- Focus and concentration patterns
- Stress handling

## 5. Mindset
- Growth vs fixed mindset indicators
- Response to challenges and failures

Generate a diagnostic report with:
- Current strengths
- Areas for improvement
- Specific recommendations
- Suggested techniques from PACER methodology
```

---

### Layer 3: Slash Commands (Explicit Actions)

Slash commands require **explicit invocation** - perfect for on-demand tools.

#### Command: `/pacer`
**Purpose**: Quick PACER classification of current content

```markdown
# .claude/commands/pacer.md
---
description: Classify content using PACER (Procedural, Analogous, Conceptual, Evidence, Reference)
argument-hint: [content or file path]
---

Analyze the following content using the PACER classification system:

$ARGUMENTS

For each distinct piece of information, identify:
1. Category (P/A/C/E/R)
2. Brief reasoning
3. Recommended protocol (Practice/Critique/Map/Store-Apply/Store-Flashcard)

Present as a structured table.
```

#### Command: `/grinde`
**Purpose**: Create a GRINDE-style mind map

```markdown
# .claude/commands/grinde.md
---
description: Create a GRINDE mind map from content
argument-hint: [topic or content]
---

Create a GRINDE-style mind map for:

$ARGUMENTS

Apply all 6 principles:
- **G**rouped: Organize into logical chunks
- **R**eflective: Include "why this matters" notes
- **I**nterconnected: Show relationships between concepts
- **N**on-verbal: Use symbols and minimal text
- **D**irectional: Show cause-effect with arrows
- **E**mphasized: Mark critical concepts with ★

Output as ASCII/text-based visual map.
```

#### Command: `/digest`
**Purpose**: Execute appropriate digestion protocol

```markdown
# .claude/commands/digest.md
---
description: Execute PACER digestion protocol for content
argument-hint: [P|A|C|E|R] [content]
---

Execute the digestion protocol for:

Type: $1
Content: $ARGUMENTS

Based on type:
- **P**: Generate practice exercises
- **A**: Create critique questions for the analogy
- **C**: Build GRINDE map structure
- **E**: Format for second-brain + application scenarios
- **R**: Generate Anki flashcards
```

#### Command: `/balance-check`
**Purpose**: Check consumption vs digestion balance

```markdown
# .claude/commands/balance-check.md
---
description: Check your consumption vs digestion balance
---

Review this conversation to assess:

## Consumption Activities (Stage 1)
- Information read/received
- Concepts introduced
- New material encountered

## Digestion Activities (Stage 2)
- Practice exercises completed
- Critiques performed
- Mind maps created
- Content stored/formatted

## Balance Assessment
- Ratio of consumption to digestion
- Recommendations for rebalancing
- Specific next actions to digest unprocessed content

Remember: ~90% forgetting rate without proper digestion!
```

#### Command: `/layer-check`
**Purpose**: Verify proper learning layer sequence

```markdown
# .claude/commands/layer-check.md
---
description: Check if learning is following proper layer sequence
argument-hint: [topic]
---

For topic: $ARGUMENTS

Assess current understanding across 4 layers:

1. **Logic Layer** (Foundation)
   - [ ] Core "why" understood?
   - [ ] Foundational framework clear?

2. **Concepts Layer**
   - [ ] Main ideas fleshed out?
   - [ ] Depth achieved?

3. **Important Details Layer**
   - [ ] Key specifics integrated?
   - [ ] Connected to bigger picture?

4. **Arbitrary Details Layer**
   - [ ] Handled last?
   - [ ] Stored in SRS if needed?

Flag any layer skipping and recommend correction.
```

#### Command: `/flashcards`
**Purpose**: Generate Anki-compatible flashcards for R-type info

```markdown
# .claude/commands/flashcards.md
---
description: Generate Anki flashcards for Reference-type information
argument-hint: [content]
allowed-tools: Write
---

Extract Reference-type (R) information from:

$ARGUMENTS

Generate Anki-compatible flashcards in format:
```
Front: [Question]
Back: [Answer]
Tags: [topic]
```

Rules:
- Only arbitrary details (dates, constants, names)
- Keep minimal - don't over-flashcard
- Include only what MUST be recalled from memory
```

---

### Layer 4: Hooks (Automation)

Hooks run on **events** - useful for tracking and automation.

#### Hook: `consumption-tracker`
**Purpose**: Track reading/consumption events

```json
// .claude/settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Read|WebFetch",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date +%s),consumption,$TOOL_NAME\" >> ~/.claude/learning-balance.log"
          }
        ]
      }
    ]
  }
}
```

#### Hook: `digestion-reminder`
**Purpose**: Prompt for digestion after consumption

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "prompt",
            "prompt": "Check if this session had significant consumption (reading, learning new info) without corresponding digestion (practice, mapping, storing). If imbalanced, remind user to digest before ending. Input: $ARGUMENTS"
          }
        ]
      }
    ]
  }
}
```

---

## Implementation Priority

### Phase 1: Core Skills (Week 1)
1. `pacer-classifier` - The foundation
2. `grinde-mapper` - Key encoding tool
3. `layer-learning` - Sequence enforcer

### Phase 2: Slash Commands (Week 2)
4. `/pacer` - Quick classification
5. `/grinde` - Map creation
6. `/digest` - Protocol execution

### Phase 3: Subagents (Week 3)
7. `learning-analyzer` - Deep analysis
8. `digestion-coach` - Active guidance

### Phase 4: Advanced Features (Week 4)
9. `/balance-check` - Session balance
10. `learner-diagnostic` - Full assessment
11. Hooks for automation

---

## File Structure

```
~/.claude/
├── skills/
│   ├── pacer-classifier/
│   │   ├── SKILL.md
│   │   ├── examples.md
│   │   └── decision-tree.md
│   ├── grinde-mapper/
│   │   ├── SKILL.md
│   │   └── examples.md
│   ├── layer-learning/
│   │   └── SKILL.md
│   └── encoding-first/
│       └── SKILL.md
├── agents/
│   ├── learning-analyzer.md
│   ├── digestion-coach.md
│   └── learner-diagnostic.md
├── commands/
│   ├── pacer.md
│   ├── grinde.md
│   ├── digest.md
│   ├── balance-check.md
│   ├── layer-check.md
│   └── flashcards.md
└── settings.json (hooks)
```

---

## Decision Matrix: When to Use What

| Sung's System | Implementation | Trigger | Rationale |
|--------------|----------------|---------|-----------|
| PACER Classification | **Skill** | Auto | Core knowledge, applies to all learning contexts |
| GRINDE Maps | **Skill** + `/grinde` | Auto + Explicit | Knowledge + on-demand creation |
| 4 Layers | **Skill** | Auto | Should catch improper sequencing automatically |
| Digestion Protocols | **Slash Commands** | Explicit | User chooses when to digest |
| Encoding-First | **Skill** | Auto | Should intervene when user over-relies on retrieval |
| Learning Analyzer | **Subagent** | Delegated | Deep analysis needs separate context |
| Digestion Coach | **Subagent** | Delegated | Interactive guidance session |
| Balance Tracking | **Hook** | Automatic | Background monitoring |
| Learner Diagnostic | **Subagent** + `/diagnose` | Explicit | Complex assessment |

---

## Improvement Opportunities

### Beyond Sung's System

1. **Integration with external tools**
   - Anki API for flashcard export
   - Obsidian/Notion templates for second-brain
   - Spaced repetition scheduling

2. **Progress tracking**
   - Learning session logs
   - Consumption/digestion metrics over time
   - Skill development tracking

3. **Adaptive recommendations**
   - Learn user's patterns
   - Personalized protocol suggestions
   - Weak area identification

4. **Content-specific optimizations**
   - Domain-specific classification hints
   - Subject-matter examples
   - Pre-built conceptual frameworks

---

## Sources

- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills.md)
- [Claude Code Subagents Documentation](https://code.claude.com/docs/en/sub-agents.md)
- [Claude Code Slash Commands Documentation](https://code.claude.com/docs/en/slash-commands.md)
- [Claude Code Hooks Documentation](https://code.claude.com/docs/en/hooks.md)
