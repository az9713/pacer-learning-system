# PACER Learning System - Developer Guide

## Table of Contents

1. [Introduction for Developers](#introduction-for-developers)
2. [Understanding Claude Code Extensions](#understanding-claude-code-extensions)
3. [Project Architecture](#project-architecture)
4. [The Four Extension Mechanisms](#the-four-extension-mechanisms)
5. [Skills - Deep Dive](#skills---deep-dive)
6. [Subagents - Deep Dive](#subagents---deep-dive)
7. [Commands - Deep Dive](#commands---deep-dive)
8. [Hooks - Deep Dive](#hooks---deep-dive)
9. [How to Add New Features](#how-to-add-new-features)
10. [Testing Your Changes](#testing-your-changes)
11. [Common Patterns and Examples](#common-patterns-and-examples)
12. [Debugging and Troubleshooting](#debugging-and-troubleshooting)
13. [Contributing Guidelines](#contributing-guidelines)

---

## Introduction for Developers

### Who This Guide Is For

This guide is for developers who want to:
- Understand how this project works
- Add new features to the PACER system
- Fix bugs or improve existing functionality
- Create similar Claude Code extensions for other projects

### Prerequisites

**You don't need to know**:
- Web development or full-stack development
- JavaScript/TypeScript (though it helps)
- Any specific programming language

**You should understand**:
- Basic programming concepts (variables, functions, files)
- How to use a terminal/command line
- How to read and write Markdown files
- Basic YAML syntax (key: value pairs)

### What is Claude Code?

Claude Code is an AI assistant that runs in your terminal. It can:
- Read and write files
- Run shell commands
- Search the web
- Understand your codebase

**Extensions** let you customize how Claude behaves in your project. This project uses Claude Code extensions to implement the PACER learning methodology.

### Key Concept: Prompt Engineering

Most of this project is **prompt engineering**, not traditional coding. The files in `.claude/` are mostly Markdown files containing instructions that tell Claude how to behave.

Think of it like:
- Traditional coding: Write code that machines execute
- Claude Code extensions: Write instructions that Claude follows

---

## Understanding Claude Code Extensions

### The Big Picture

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLAUDE CODE                               │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                   USER CONVERSATION                       │   │
│  │                                                           │   │
│  │  User: "Help me learn about photosynthesis"              │   │
│  │                                                           │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│                              ▼                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                   EXTENSION LAYER                         │   │
│  │                                                           │   │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐     │   │
│  │  │ Skills  │  │ Agents  │  │Commands │  │ Hooks   │     │   │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘     │   │
│  │                                                           │   │
│  │  Loaded from: .claude/ directory                          │   │
│  └──────────────────────────────────────────────────────────┘   │
│                              │                                   │
│                              ▼                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                   CLAUDE RESPONSE                         │   │
│  │                                                           │   │
│  │  "Let me classify this content using PACER..."           │   │
│  │                                                           │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### The Four Mechanisms

Claude Code has four ways to extend its behavior:

| Mechanism | Trigger | Best For | Files Location |
|-----------|---------|----------|----------------|
| **Skills** | Claude decides to use them | Expertise, patterns | `.claude/skills/*/SKILL.md` |
| **Agents** | Spawned for specific tasks | Complex multi-step work | `.claude/agents/*.md` |
| **Commands** | User types `/command` | Quick actions, shortcuts | `.claude/commands/*.md` |
| **Hooks** | System events | Automation, logging | `.claude/settings.json` |

### Where Files Go

```
your-project/
├── .claude/                    ← Extension directory
│   ├── skills/                 ← Skills go here
│   │   └── skill-name/
│   │       └── SKILL.md        ← Required: main skill file
│   ├── agents/                 ← Agents go here
│   │   └── agent-name.md
│   ├── commands/               ← Commands go here
│   │   └── command-name.md
│   ├── settings.json           ← Hooks configuration
│   └── settings.local.json     ← Local overrides (gitignored)
├── CLAUDE.md                   ← Project context for Claude
└── ... (rest of your project)
```

---

## Project Architecture

### This Project's Structure

```
pacer_bestpartnerstv/
├── .claude/
│   ├── skills/
│   │   ├── pacer-classifier/      ← Auto-classifies P/A/C/E/R
│   │   │   ├── SKILL.md
│   │   │   ├── examples.md
│   │   │   └── decision-tree.md
│   │   ├── grinde-mapper/         ← Creates mind maps
│   │   │   ├── SKILL.md
│   │   │   └── examples.md
│   │   ├── layer-learning/        ← Enforces 4 layers
│   │   │   ├── SKILL.md
│   │   │   └── examples.md
│   │   └── encoding-first/        ← Prioritizes encoding
│   │       ├── SKILL.md
│   │       └── examples.md
│   ├── agents/
│   │   ├── learning-analyzer.md   ← Analyzes content
│   │   ├── digestion-coach.md     ← Guides processing
│   │   └── learner-diagnostic.md  ← Assesses learner
│   ├── commands/
│   │   ├── pacer.md               ← /pacer command
│   │   ├── grinde.md              ← /grinde command
│   │   ├── digest.md              ← /digest command
│   │   ├── balance-check.md       ← /balance-check command
│   │   ├── layer-check.md         ← /layer-check command
│   │   └── flashcards.md          ← /flashcards command
│   ├── settings.json              ← Hooks
│   └── settings.local.json        ← Permissions
├── docs/
│   ├── USER_GUIDE.md
│   ├── DEVELOPER_GUIDE.md         ← You are here
│   ├── QUICK_START.md
│   ├── TROUBLESHOOTING.md
│   ├── PACER_RESEARCH_COMPREHENSIVE.md
│   ├── IMPLEMENTATION_ARCHITECTURE.md
│   └── CLAUDE_CODE_EXTENSION_ARCHITECTURE.md
├── CLAUDE.md                       ← Project context
└── README.md
```

### How Components Connect

```
┌─────────────────────────────────────────────────────────────────┐
│                     USER INTERACTION                             │
└─────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│   COMMANDS    │    │    SKILLS     │    │    HOOKS      │
│               │    │               │    │               │
│ User types    │    │ Auto-trigger  │    │ System events │
│ /pacer        │    │ when learning │    │ trigger       │
│ /grinde       │    │ discussed     │    │ automatically │
└───────┬───────┘    └───────┬───────┘    └───────┬───────┘
        │                    │                    │
        └─────────────────────┼────────────────────┘
                              ▼
                    ┌───────────────────┐
                    │     AGENTS        │
                    │                   │
                    │ Spawned for       │
                    │ complex tasks     │
                    └───────────────────┘
```

---

## The Four Extension Mechanisms

### Quick Comparison

| Aspect | Skills | Agents | Commands | Hooks |
|--------|--------|--------|----------|-------|
| **Who triggers** | Claude | Claude/User | User | System |
| **Context** | Shared | Separate | Shared | N/A |
| **Invocation** | Automatic | Task tool | /command | Events |
| **Complexity** | Any | Complex | Simple | Simple |
| **File format** | SKILL.md | Markdown | Markdown | JSON |

### When to Use Each

```
Decision Tree: Which mechanism should I use?

START
  │
  ▼
Is this triggered by a system event (file read, session end)?
  │
  ├─YES─► Use a HOOK
  │
  └─NO──► Does the user explicitly invoke it?
            │
            ├─YES─► Use a COMMAND
            │
            └─NO──► Does it need its own context window?
                      │
                      ├─YES─► Use an AGENT
                      │
                      └─NO──► Use a SKILL
```

---

## Skills - Deep Dive

### What is a Skill?

A Skill is a set of instructions that Claude can choose to follow based on the conversation context. Skills are like "expertise" that Claude applies when relevant.

### File Structure

```
.claude/skills/
└── your-skill-name/
    ├── SKILL.md           ← Required: Main skill file
    ├── examples.md        ← Optional: Examples for Claude
    ├── decision-tree.md   ← Optional: Decision logic
    └── any-other-file.md  ← Optional: Supporting content
```

### SKILL.md Format

```markdown
---
name: skill-name
description: One sentence that tells Claude WHEN to use this skill. This is critical - Claude uses this to decide when to activate the skill.
allowed-tools: Read, Write, Edit  # Optional: Restrict tool access
---

# Skill Title

## Purpose
[What this skill does]

## When to Use
[More details on when Claude should apply this]

## Instructions
[Step-by-step instructions for Claude to follow]

## Examples
[Examples of proper usage]
```

### The `description` Field is Critical

The `description` in the frontmatter is how Claude decides whether to use a skill. Make it specific and include trigger phrases.

**Good description**:
```yaml
description: Classifies information into PACER categories (Procedural, Analogous, Conceptual, Evidence, Reference) and recommends digestion protocols. Use when learning new material, studying, reading educational content, or when user asks about how to study or remember something.
```

**Bad description**:
```yaml
description: Helps with learning.  # Too vague!
```

### Example: The pacer-classifier Skill

File: `.claude/skills/pacer-classifier/SKILL.md`

```markdown
---
name: pacer-classifier
description: Classifies information into PACER categories (Procedural, Analogous, Conceptual, Evidence, Reference) and recommends appropriate digestion protocols. Use when learning new material, studying, reading educational content, processing information for retention, or when user asks about how to study or remember something.
---

# PACER Classification Skill

## The PACER Framework

PACER classifies information into 5 types...

[Rest of skill content]
```

### Supporting Files

Skills can have additional files for organization:

**examples.md** - Real examples for Claude to learn from:
```markdown
# Examples

## Example 1: Medical Content
Input: "Antibiotics target bacterial structures..."
Classification: Conceptual
Reasoning: Explains mechanism, needs understanding

## Example 2: Recipe
Input: "Preheat oven to 350°F..."
Classification: Procedural
Reasoning: Steps to follow, needs practice
```

**decision-tree.md** - Logic for complex decisions:
```markdown
# Decision Tree

1. Ask: Is this something to DO?
   - YES → Procedural
   - NO → Continue

2. Ask: Is this a comparison?
   - YES → Analogous
   - NO → Continue

[etc.]
```

### How Skills Auto-Trigger

1. User says something about learning/studying
2. Claude reads the skill's `description`
3. If relevant, Claude loads and follows the skill
4. Skill instructions guide Claude's response

```
User: "I need to learn about photosynthesis for my exam"
          │
          ▼
Claude checks skill descriptions:
  - pacer-classifier: "...learning new material, studying..."
  - grinde-mapper: "...organizing concepts, creating study notes..."
  - layer-learning: "...studying complex topics..."
          │
          ▼
Multiple skills match! Claude applies them:
  1. Classifies content (pacer-classifier)
  2. Suggests mind map (grinde-mapper)
  3. Checks layer sequence (layer-learning)
```

---

## Subagents - Deep Dive

### What is a Subagent?

A Subagent is a separate Claude instance spawned to handle a specific task. It has its own context window and can use specified tools.

### When to Use Agents

Use agents when:
- The task is complex and multi-step
- You need isolated context (not polluting main conversation)
- You want to delegate work

### File Format

File: `.claude/agents/agent-name.md`

```markdown
---
name: agent-name
description: What this agent does and WHEN to spawn it. Include trigger phrases.
tools: Read, Write, Grep, Glob  # Tools the agent can use
model: sonnet                     # or opus, haiku
skills: skill1, skill2            # Skills the agent inherits
---

# Agent Title

## Your Role
[Who this agent is and what it does]

## Workflow
[Step-by-step instructions]

## Output Format
[How to structure outputs]
```

### Example: learning-analyzer Agent

File: `.claude/agents/learning-analyzer.md`

```markdown
---
name: learning-analyzer
description: Analyzes learning content using PACER classification and Layer Learning. Use PROACTIVELY when user is studying, reading educational content, or processing information for learning.
tools: Read, Grep, Glob, WebFetch
model: sonnet
skills: pacer-classifier, layer-learning
---

# Learning Analyzer Agent

## Your Role
When users provide learning content, you:
1. Classify using PACER
2. Apply Layer Learning
3. Generate structured output

## Analysis Workflow
...
```

### How to Spawn an Agent

Agents are spawned in two ways:

**1. Claude decides to spawn** (based on description):
```
User: "Analyze this textbook chapter for learning"
Claude: (reads agent descriptions)
Claude: (spawns learning-analyzer agent)
```

**2. User explicitly requests**:
```
User: "Use the learning-analyzer agent to process this"
```

### Agent vs Skill: When to Choose

| Situation | Use Skill | Use Agent |
|-----------|-----------|-----------|
| Quick classification | ✅ | |
| Deep analysis of long document | | ✅ |
| Pattern to apply to many things | ✅ | |
| Multi-step process with state | | ✅ |
| Expertise that enhances responses | ✅ | |
| Isolated task that shouldn't pollute context | | ✅ |

---

## Commands - Deep Dive

### What is a Command?

A Command is a user-invoked action triggered by typing `/command-name`. Think of it as a shortcut for common tasks.

### File Format

File: `.claude/commands/command-name.md`

```markdown
# /command-name - Short Description

Brief explanation of what this command does.

## Usage

```
/command-name [arguments]
```

## Arguments

- `arg1`: Description of first argument
- `arg2`: Description of second argument (optional)

## Instructions

When the user invokes `/command-name`, do the following:

1. [First step]
2. [Second step]
3. [Third step]

## Output Format

```markdown
[Template for output]
```

## Examples

### Example 1
```
/command-name example-input
```
Output:
```
[example output]
```
```

### Example: The /grinde Command

File: `.claude/commands/grinde.md`

```markdown
# /grinde - Generate GRINDE Mind Map

Create a GRINDE-style mind map for deep encoding.

## Usage

```
/grinde [topic]
```

## Arguments

- `topic`: The subject or concept to map

## Instructions

When the user invokes `/grinde`, create a GRINDE mind map following these principles:

### GRINDE Principles

| Letter | Principle | Application |
|--------|-----------|-------------|
| **G** | Grouped | Chunk related information |
| **R** | Reflective | Add "Why?" annotations |
...

## Output Format

```markdown
## GRINDE Map: [Topic]

### The Backbone
[Core insight]

### Map
[ASCII visual]
```
```

### How Commands Work

1. User types `/command-name argument`
2. Claude finds the command file
3. Claude follows the instructions in the file
4. Claude generates output according to the format

```
User: "/grinde photosynthesis"
          │
          ▼
Claude loads: .claude/commands/grinde.md
          │
          ▼
Claude follows instructions:
  1. Identify backbone
  2. Create chunks
  3. Add connections
  4. Format as ASCII map
          │
          ▼
Claude outputs the GRINDE map
```

---

## Hooks - Deep Dive

### What is a Hook?

A Hook is code that runs automatically when certain events occur. It's like a trigger that fires when something happens.

### Available Events

| Event | When It Fires | Use Case |
|-------|---------------|----------|
| `PreToolUse` | Before a tool runs | Validate, modify, block |
| `PostToolUse` | After a tool runs | Log, analyze, react |
| `Notification` | On notifications | Custom handling |
| `Stop` | Session ends | Cleanup, reminders |

### Configuration File

File: `.claude/settings.json`

```json
{
  "hooks": {
    "EventName": [
      {
        "matcher": "pattern",
        "hooks": [
          {
            "type": "command",
            "command": "shell command to run"
          }
        ]
      }
    ]
  }
}
```

### Hook Types

**1. Command Hook** - Runs a shell command:
```json
{
  "type": "command",
  "command": "echo 'Something happened' >> log.txt"
}
```

**2. Prompt Hook** - Gives Claude additional instructions:
```json
{
  "type": "prompt",
  "prompt": "Remind the user about X if condition Y"
}
```

### Example: This Project's Hooks

File: `.claude/settings.json`

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Read|WebFetch",
        "hooks": [
          {
            "type": "command",
            "command": "echo [$(date +%Y-%m-%dT%H:%M:%S)] CONSUMPTION: $TOOL_NAME >> \"$CLAUDE_PROJECT_DIR/.claude/learning-balance.log\""
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "prompt",
            "prompt": "Before ending, check if significant content was consumed without digestion. If imbalanced, remind the user."
          }
        ]
      }
    ]
  }
}
```

**What this does**:
1. Every time `Read` or `WebFetch` is used, log it (tracking consumption)
2. When session ends, remind about digestion if needed

### Environment Variables in Hooks

| Variable | Description |
|----------|-------------|
| `$TOOL_NAME` | Name of the tool that triggered |
| `$TOOL_INPUT` | JSON input to the tool |
| `$TOOL_OUTPUT` | JSON output from the tool |
| `$CLAUDE_PROJECT_DIR` | Project directory path |

---

## How to Add New Features

### Step 1: Decide the Mechanism

Use this decision tree:

```
What do you want to add?
│
├─ Triggered by system event?
│   └─ YES → Add a HOOK to settings.json
│
├─ User explicitly invokes it?
│   └─ YES → Create a COMMAND in .claude/commands/
│
├─ Needs separate context for complex work?
│   └─ YES → Create an AGENT in .claude/agents/
│
└─ Expertise Claude should apply automatically?
    └─ YES → Create a SKILL in .claude/skills/
```

### Step 2: Create the Files

#### For a Skill:

```bash
# Create directory
mkdir .claude/skills/my-new-skill

# Create main skill file
touch .claude/skills/my-new-skill/SKILL.md
```

Edit `SKILL.md`:
```markdown
---
name: my-new-skill
description: [When should Claude use this? Be specific!]
---

# My New Skill

[Instructions for Claude]
```

#### For an Agent:

```bash
touch .claude/agents/my-new-agent.md
```

Edit `my-new-agent.md`:
```markdown
---
name: my-new-agent
description: [When should this agent be spawned?]
tools: Read, Write  # What tools can it use?
model: sonnet       # What model?
---

# My New Agent

[Instructions for the agent]
```

#### For a Command:

```bash
touch .claude/commands/my-command.md
```

Edit `my-command.md`:
```markdown
# /my-command - Brief Description

## Usage
```
/my-command [arguments]
```

## Instructions
[What to do when invoked]
```

#### For a Hook:

Edit `.claude/settings.json`:
```json
{
  "hooks": {
    "EventName": [
      {
        "matcher": "ToolPattern",
        "hooks": [
          {
            "type": "command|prompt",
            "command": "shell command",
            "prompt": "instructions"
          }
        ]
      }
    ]
  }
}
```

### Step 3: Test Your Addition

See the [Testing Your Changes](#testing-your-changes) section.

### Step 4: Document Your Addition

1. Update `CLAUDE.md` with the new capability
2. Add user-facing documentation if needed
3. Update this developer guide if it's a significant addition

---

## Testing Your Changes

### Testing Skills

1. Start Claude Code in the project:
   ```bash
   cd your-project
   claude
   ```

2. Ask about something that should trigger the skill:
   ```
   [Type something that matches the skill's description triggers]
   ```

3. Verify Claude applies the skill:
   - Check if the response follows the skill's format
   - Check if the skill's principles are applied

### Testing Agents

1. Start Claude Code

2. Explicitly request the agent:
   ```
   Use the [agent-name] agent to [task]
   ```

3. Verify:
   - Agent is spawned correctly
   - Agent uses the right tools
   - Agent produces expected output

### Testing Commands

1. Start Claude Code

2. Type the command:
   ```
   /command-name [arguments]
   ```

3. If you get "Unknown slash command":
   - This is expected for project-level commands
   - Instead, ask Claude to follow the command:
     ```
     Follow the /command-name instructions for: [arguments]
     ```

### Testing Hooks

1. For PostToolUse hooks, trigger the tool:
   ```
   Read the file [filename]
   ```

2. Check if the hook ran:
   - For command hooks, check the expected side effects (logs, etc.)
   - For prompt hooks, observe Claude's behavior

3. For Stop hooks:
   - End the session
   - Restart and check for expected behavior

### Debugging Tips

1. **Skill not triggering?**
   - Check the `description` field
   - Make it more specific with trigger phrases

2. **Command not found?**
   - Project-level commands may need explicit invocation
   - Ask Claude to "follow the /command instructions"

3. **Agent not spawning?**
   - Check the `description` field
   - Check the `tools` field for typos

4. **Hook not firing?**
   - Check the JSON syntax
   - Check the `matcher` pattern
   - Check file paths use the right format for your OS

---

## Common Patterns and Examples

### Pattern 1: Skill with Supporting Files

```
.claude/skills/my-skill/
├── SKILL.md           ← Main instructions
├── examples.md        ← Examples for Claude to learn from
├── templates.md       ← Output templates
└── rules.md           ← Specific rules to follow
```

In `SKILL.md`, reference other files:
```markdown
## Examples
See [examples.md](examples.md) for detailed examples.

## Templates
Use the templates in [templates.md](templates.md).
```

### Pattern 2: Command with Verification

```markdown
# /dangerous-command - Does Something Risky

## Usage
```
/dangerous-command [target]
```

## Instructions

### Pre-Flight Check
Before executing, verify:
- [ ] User has confirmed intent
- [ ] Target is valid
- [ ] No destructive side effects

### Execution
[Only proceed if all checks pass]
```

### Pattern 3: Agent with Skills

```yaml
---
name: specialized-agent
description: Use for [specific task]
tools: Read, Write, Edit
model: sonnet
skills: skill-a, skill-b
---
```

The agent inherits the skills, combining their capabilities.

### Pattern 4: Hook Chain

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'File written' >> activity.log"
          },
          {
            "type": "prompt",
            "prompt": "A file was written. Verify it matches requirements."
          }
        ]
      }
    ]
  }
}
```

Multiple hooks can fire for the same event.

---

## Debugging and Troubleshooting

### Common Issues

#### "Unknown slash command"

**Cause**: Project-level commands don't register as built-in commands.

**Solution**: Ask Claude to follow the command instructions explicitly:
```
Please follow the /pacer command instructions for this content: [content]
```

Or reference the command file:
```
Use the instructions in .claude/commands/pacer.md to classify: [content]
```

#### Skill Not Triggering

**Cause**: The `description` doesn't match the conversation context.

**Solution**: Make the description more specific:
```yaml
# Bad
description: Helps with studying

# Good
description: Classifies learning content into PACER categories. Use when user mentions studying, learning, flashcards, memorization, or asks how to remember something.
```

#### Hook Not Firing

**Cause**: Often a JSON syntax error or wrong event name.

**Solution**:
1. Validate JSON syntax: Use an online JSON validator
2. Check event name spelling: `PreToolUse`, `PostToolUse`, `Stop`
3. Check matcher pattern: Use `|` for OR, escape special characters

#### Agent Has Wrong Tools

**Cause**: Typo in the `tools` field.

**Solution**: Use exact tool names:
```yaml
tools: Read, Write, Edit, Bash, Grep, Glob, WebFetch, WebSearch
```

### Debugging Workflow

1. **Add logging**:
   ```json
   {
     "type": "command",
     "command": "echo DEBUG: $TOOL_NAME triggered >> debug.log"
   }
   ```

2. **Check Claude's understanding**:
   ```
   What skills and commands are available in this project?
   ```

3. **Test in isolation**:
   - Test one skill at a time
   - Test with simple inputs first

4. **Read Claude's reasoning**:
   - Ask Claude to explain what it's doing
   - Check if it mentions using your skill/command

---

## Contributing Guidelines

### Code Style

1. **Markdown Formatting**:
   - Use ATX headers (`#`, `##`, etc.)
   - Use fenced code blocks with language tags
   - Use tables for structured information

2. **YAML Frontmatter**:
   - Keep it minimal
   - Use lowercase keys
   - Indent with 2 spaces

3. **Naming Conventions**:
   - Skills: `kebab-case` directory names
   - Agents: `kebab-case.md` filenames
   - Commands: `kebab-case.md` filenames

### Before Submitting Changes

1. **Test your changes** (see Testing section)
2. **Update documentation**:
   - Update `CLAUDE.md`
   - Update relevant docs files
3. **Follow existing patterns**:
   - Look at existing files for format guidance
   - Maintain consistency

### File Checklist for New Features

- [ ] Main file created (SKILL.md, agent.md, or command.md)
- [ ] Description field is specific and helpful
- [ ] Examples included where helpful
- [ ] Output format specified
- [ ] CLAUDE.md updated
- [ ] User-facing documentation updated (if applicable)
- [ ] Tested in Claude Code

---

## Quick Reference

### File Locations

| Component | Location |
|-----------|----------|
| Skills | `.claude/skills/{name}/SKILL.md` |
| Agents | `.claude/agents/{name}.md` |
| Commands | `.claude/commands/{name}.md` |
| Hooks | `.claude/settings.json` |
| Project Context | `CLAUDE.md` |

### Required Fields

| Component | Required Fields |
|-----------|-----------------|
| Skill | `name`, `description` |
| Agent | `name`, `description`, `tools` |
| Command | Title, Usage, Instructions |
| Hook | `type`, `command` or `prompt` |

### Tools Available to Agents

```
Read, Write, Edit, Bash, Grep, Glob,
WebFetch, WebSearch, Task, TodoWrite
```

### Hook Events

```
PreToolUse, PostToolUse, Notification, Stop
```

---

## Getting Help

1. **Check the troubleshooting section** in this guide
2. **Read the example files** in this project
3. **Check Claude Code documentation** at https://docs.anthropic.com/claude-code
4. **Ask Claude** - it knows how its own extension system works!
