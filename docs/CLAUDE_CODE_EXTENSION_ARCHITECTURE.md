# Claude Code Extension Architecture Guide

## A Comprehensive Framework for Choosing Between Skills, Subagents, Slash Commands, and Hooks

---

## Table of Contents

1. [Introduction](#introduction)
2. [The Four Extension Mechanisms](#the-four-extension-mechanisms)
3. [Decision Framework](#decision-framework)
4. [Deep Dive: Skills](#deep-dive-skills)
5. [Deep Dive: Subagents](#deep-dive-subagents)
6. [Deep Dive: Slash Commands](#deep-dive-slash-commands)
7. [Deep Dive: Hooks](#deep-dive-hooks)
8. [Comparison Matrix](#comparison-matrix)
9. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)
10. [Case Study: PACER Learning System](#case-study-pacer-learning-system)
11. [Advanced Patterns](#advanced-patterns)
12. [Quick Reference](#quick-reference)

---

## Introduction

Claude Code provides four primary extension mechanisms, each designed for different use cases. Choosing the wrong mechanism leads to:
- Poor user experience (having to explicitly invoke something that should be automatic)
- Wasted context (loading knowledge that isn't needed)
- Missed opportunities (Claude not applying relevant expertise)
- Maintenance burden (complex implementations where simple ones suffice)

This guide provides a systematic framework for making the right choice.

### The Core Question

When extending Claude Code, always ask:

> **"Who or what should decide when this capability is used?"**

| Answer | Mechanism |
|--------|-----------|
| Claude should decide automatically | **Skill** |
| Claude should delegate to a specialist | **Subagent** |
| The user should explicitly request it | **Slash Command** |
| The system should trigger on events | **Hook** |

---

## The Four Extension Mechanisms

### Overview Table

| Mechanism | Trigger Type | Context | Primary Purpose | File Location |
|-----------|-------------|---------|-----------------|---------------|
| **Skills** | Model-invoked (automatic) | Shared with conversation | Add knowledge/expertise | `~/.claude/skills/` or `.claude/skills/` |
| **Subagents** | Delegated or explicit | Separate context window | Specialized task execution | `~/.claude/agents/` or `.claude/agents/` |
| **Slash Commands** | User-invoked (`/command`) | Injected into conversation | Reusable prompts/actions | `~/.claude/commands/` or `.claude/commands/` |
| **Hooks** | Event-driven (automatic) | Background execution | Automation/validation | `settings.json` |

### Visual Decision Tree

```
                    ┌─────────────────────────────────┐
                    │  I want to extend Claude Code   │
                    └─────────────────┬───────────────┘
                                      │
                    ┌─────────────────▼───────────────┐
                    │  Should it run automatically?   │
                    └─────────────────┬───────────────┘
                                      │
                 ┌────────────────────┼────────────────────┐
                 │ YES                │                    │ NO
                 ▼                    │                    ▼
    ┌────────────────────┐           │       ┌────────────────────┐
    │ Based on CONTENT   │           │       │ User types command │
    │ of conversation?   │           │       │ to invoke it?      │
    └─────────┬──────────┘           │       └─────────┬──────────┘
              │                      │                 │
      ┌───────┴───────┐              │         ┌───────┴───────┐
      │ YES           │ NO           │         │ YES           │ NO
      ▼               ▼              │         ▼               ▼
 ┌─────────┐   ┌───────────┐        │    ┌─────────┐    ┌─────────┐
 │  SKILL  │   │   HOOK    │        │    │ SLASH   │    │ Consider│
 │         │   │ (event-   │        │    │ COMMAND │    │ MCP or  │
 │         │   │  based)   │        │    │         │    │ other   │
 └─────────┘   └───────────┘        │    └─────────┘    └─────────┘
      │                             │
      ▼                             │
 ┌─────────────────────┐            │
 │ Needs separate      │            │
 │ context/isolation?  │            │
 └─────────┬───────────┘            │
           │                        │
   ┌───────┴───────┐                │
   │ YES           │ NO             │
   ▼               ▼                │
┌──────────┐  ┌─────────┐           │
│ SUBAGENT │  │  SKILL  │           │
│          │  │ (stays) │           │
└──────────┘  └─────────┘           │
```

---

## Decision Framework

### The Five Key Questions

When deciding which mechanism to use, ask these questions in order:

#### Question 1: Is this knowledge or action?

| Type | Description | Likely Mechanism |
|------|-------------|------------------|
| **Knowledge** | Information, guidelines, best practices | Skill |
| **Action** | Doing something specific | Slash Command or Subagent |
| **Reaction** | Responding to events | Hook |

#### Question 2: Who decides when to use it?

| Decision Maker | Mechanism | Example |
|----------------|-----------|---------|
| **Claude** (based on context) | Skill | "Apply our code review standards" |
| **Claude** (delegation) | Subagent | "Run a deep security analysis" |
| **User** (explicit request) | Slash Command | `/deploy staging` |
| **System** (event trigger) | Hook | "Lint after every file write" |

#### Question 3: Does it need isolated context?

| Context Need | Mechanism | Rationale |
|--------------|-----------|-----------|
| **Shared context** | Skill | Knowledge enhances the current conversation |
| **Isolated context** | Subagent | Task benefits from fresh, focused context |
| **Injected context** | Slash Command | Adds specific prompt to conversation |
| **No context** | Hook | Runs in background, doesn't see conversation |

#### Question 4: How complex is it?

| Complexity | Mechanism | Why |
|------------|-----------|-----|
| **Simple guidance** | Skill (single file) | Just needs SKILL.md |
| **Reference + examples** | Skill (multi-file) | SKILL.md + supporting files |
| **Complex workflow** | Subagent | Dedicated agent with specific tools |
| **Quick prompt** | Slash Command | Single markdown file |
| **System automation** | Hook | Shell script or prompt evaluation |

#### Question 5: Should it always load into context?

| Loading Behavior | Mechanism | Context Impact |
|------------------|-----------|----------------|
| **Load name/description only, full content on demand** | Skill | Efficient - only loads when relevant |
| **Never in main context** | Subagent | Runs separately |
| **Only when explicitly called** | Slash Command | User controls |
| **Never in context** | Hook | Background only |

---

## Deep Dive: Skills

### What Are Skills?

Skills are **markdown files that teach Claude how to do something specific**. They are **model-invoked** - Claude automatically applies them when your request matches their description.

### When to Use Skills

✅ **Use Skills when:**
- Claude should automatically recognize when to apply this knowledge
- The expertise enhances (not replaces) the current conversation
- You want consistent application of standards/practices
- The guidance applies across multiple scenarios
- You need progressive disclosure (main content + reference files)

❌ **Don't use Skills when:**
- The user should explicitly choose when to invoke it
- The task needs a completely fresh context
- It's a one-off prompt you run occasionally
- It needs to respond to system events (use Hooks)

### Skill Anatomy

```
my-skill/
├── SKILL.md              # Required: Main file with metadata + instructions
├── reference.md          # Optional: Detailed docs loaded on demand
├── examples.md           # Optional: Usage examples
└── scripts/
    └── helper.py         # Optional: Utility scripts (executed, not loaded)
```

**SKILL.md Structure:**
```yaml
---
name: skill-name                    # Required: lowercase, hyphens only
description: When to use this skill # Required: Claude uses this to decide activation
allowed-tools: Tool1, Tool2         # Optional: Restrict tool access
model: claude-sonnet-4-20250514     # Optional: Specific model
---

# Skill Title

## Instructions
Clear, step-by-step guidance for Claude.

## Key Principles
Important rules or standards to follow.

## Additional Resources
- For details, see [reference.md](reference.md)
- For examples, see [examples.md](examples.md)
```

### Skill Best Practices

#### 1. Write Discoverable Descriptions
The `description` field is how Claude decides whether to use your Skill. Be specific:

```yaml
# ❌ Bad: Too vague
description: Helps with documents

# ✅ Good: Specific triggers and capabilities
description: Reviews pull requests for security vulnerabilities, performance issues, and code style. Use when reviewing PRs, checking code changes, or when user mentions "review" or "check my code".
```

#### 2. Use Progressive Disclosure
Keep SKILL.md focused (<500 lines). Put detailed reference material in separate files:

```markdown
# In SKILL.md
## Quick Reference
[Essential info here]

## Detailed Documentation
For complete API details, see [reference.md](reference.md)
```

#### 3. Bundle Utility Scripts
Scripts execute without loading into context - great for validation, formatting, etc.:

```markdown
To validate the configuration, run:
```bash
python scripts/validate.py input.json
```
```

### Skill Activation Flow

```
┌─────────────────────────────────────────────────────────────┐
│                      User sends request                      │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│     Claude checks request against all Skill descriptions    │
│     (Only names and descriptions are loaded at startup)     │
└─────────────────────────────┬───────────────────────────────┘
                              │
                    ┌─────────┴─────────┐
                    │ Match found?      │
                    └─────────┬─────────┘
                              │
              ┌───────────────┼───────────────┐
              │ YES                           │ NO
              ▼                               ▼
┌─────────────────────────┐     ┌─────────────────────────┐
│ Claude asks to use Skill │     │ Normal response         │
│ User sees confirmation   │     │ (no Skill applied)      │
└───────────┬─────────────┘     └─────────────────────────┘
            │
            ▼
┌─────────────────────────┐
│ Full SKILL.md loaded    │
│ Claude follows guidance │
└─────────────────────────┘
```

---

## Deep Dive: Subagents

### What Are Subagents?

Subagents are **specialized AI assistants that operate in their own context window**. Claude can delegate tasks to them, and they work independently before returning results.

### When to Use Subagents

✅ **Use Subagents when:**
- The task benefits from a fresh, focused context
- You need different tool access than the main conversation
- Complex analysis that would pollute the main context
- Specialized expertise that should run independently
- You want resumable, long-running tasks

❌ **Don't use Subagents when:**
- Simple knowledge that should enhance current conversation (use Skill)
- Quick prompts the user runs occasionally (use Slash Command)
- The task doesn't need isolation
- You need to maintain conversational continuity

### Subagent Anatomy

```markdown
# .claude/agents/my-agent.md
---
name: agent-name                    # Required: Unique identifier
description: When to use this agent # Required: Triggers delegation
tools: Tool1, Tool2                 # Optional: Specific tools (inherits all if omitted)
model: sonnet                       # Optional: Model alias or 'inherit'
permissionMode: default             # Optional: Permission handling
skills: skill1, skill2              # Optional: Skills to preload
---

System prompt that defines the agent's role, capabilities,
and approach to problem-solving.

Include specific instructions, best practices, and constraints.
```

### Key Subagent Concepts

#### 1. Context Isolation
Subagents start with a **clean context**. They don't see the main conversation history. This is beneficial for:
- Complex analysis without context pollution
- Focused task execution
- Parallel processing of independent tasks

#### 2. Tool Restriction
You can limit which tools a subagent can use:

```yaml
# Full access (inherits all tools)
# (omit tools field)

# Restricted access
tools: Read, Grep, Glob, Bash
```

#### 3. Automatic vs Explicit Invocation

**Automatic Delegation:**
Claude decides to delegate based on the `description`:
```yaml
description: Expert code reviewer. Use PROACTIVELY after code changes.
```

**Explicit Invocation:**
User requests specific subagent:
```
> Use the security-auditor subagent to check this code
```

#### 4. Resumable Subagents
Subagents can be resumed to continue previous work:
```
> Resume agent abc123 and continue the analysis
```

### Subagent Delegation Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    Main Conversation                         │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ User: "Analyze this code for security issues"       │    │
│  └─────────────────────────────────────────────────────┘    │
│                           │                                  │
│                           ▼                                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Claude: "I'll delegate to security-auditor agent"   │    │
│  └─────────────────────────────────────────────────────┘    │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ Delegation
                            ▼
┌─────────────────────────────────────────────────────────────┐
│               Subagent Context (Isolated)                    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ System: Security auditor prompt                     │    │
│  │ Task: Analyze code for security issues              │    │
│  │ Tools: Read, Grep, Bash (restricted)                │    │
│  └─────────────────────────────────────────────────────┘    │
│                           │                                  │
│                           │ Analysis work...                 │
│                           ▼                                  │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Findings: [Detailed security report]                │    │
│  └─────────────────────────────────────────────────────┘    │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ Results returned
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    Main Conversation                         │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Claude: "Here's the security analysis..."           │    │
│  │ [Summarized findings from subagent]                 │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

### Built-in Subagents

Claude Code includes several built-in subagents:

| Subagent | Model | Tools | Purpose |
|----------|-------|-------|---------|
| **Explore** | Haiku | Read, Grep, Glob, Bash (read-only) | Fast codebase exploration |
| **Plan** | Sonnet | Read, Grep, Glob, Bash | Research during plan mode |
| **General-purpose** | Sonnet | All tools | Complex multi-step tasks |

---

## Deep Dive: Slash Commands

### What Are Slash Commands?

Slash commands are **reusable prompts defined as markdown files** that users invoke explicitly by typing `/command-name`.

### When to Use Slash Commands

✅ **Use Slash Commands when:**
- Users should explicitly choose when to run this
- It's a frequently used prompt/workflow
- The action is simple and self-contained
- You want to pass arguments
- It's a quick operation, not ongoing guidance

❌ **Don't use Slash Commands when:**
- Claude should decide when to apply it (use Skill)
- It needs isolated context (use Subagent)
- It should respond to events (use Hook)
- It's complex guidance spanning multiple scenarios (use Skill)

### Slash Command Anatomy

```markdown
# .claude/commands/my-command.md
---
description: Brief description of the command    # Shows in /help
argument-hint: [required-arg] [optional-arg]     # Usage hint
allowed-tools: Tool1, Tool2                      # Optional: Restrict tools
model: claude-3-5-haiku-20241022                 # Optional: Specific model
---

The prompt content that will be executed.

Use $ARGUMENTS for all arguments, or $1, $2 for positional.

Reference files with @path/to/file
Execute bash with !`command`
```

### Slash Command Features

#### 1. Arguments

**All arguments:**
```markdown
Fix issue #$ARGUMENTS following our standards
# /fix-issue 123 high-priority
# $ARGUMENTS = "123 high-priority"
```

**Positional arguments:**
```markdown
Review PR #$1 with priority $2
# /review-pr 456 high
# $1 = "456", $2 = "high"
```

#### 2. File References
```markdown
Compare @src/old.js with @src/new.js
```

#### 3. Bash Execution
```markdown
---
allowed-tools: Bash(git:*)
---

Current branch: !`git branch --show-current`
Recent commits: !`git log --oneline -5`

Based on these, create a commit message.
```

#### 4. Frontmatter Options

| Field | Purpose | Default |
|-------|---------|---------|
| `description` | Shown in `/help` | First line of prompt |
| `argument-hint` | Usage hint for autocomplete | None |
| `allowed-tools` | Restrict tool access | Inherits from conversation |
| `model` | Specific model to use | Inherits from conversation |
| `disable-model-invocation` | Prevent SlashCommand tool from calling | false |

### Slash Command Locations

| Location | Scope | Priority |
|----------|-------|----------|
| `.claude/commands/` | Project (team) | Highest |
| `~/.claude/commands/` | Personal (all projects) | Lower |
| Plugin commands | Plugin users | Lowest |

**Namespacing with subdirectories:**
- `.claude/commands/frontend/test.md` → `/test` (project:frontend)
- `.claude/commands/backend/test.md` → `/test` (project:backend)

### Skills vs Slash Commands

This is a common source of confusion. Here's the key distinction:

| Aspect | Skills | Slash Commands |
|--------|--------|----------------|
| **Invocation** | Claude decides | User types `/command` |
| **Purpose** | Ongoing expertise | One-off actions |
| **Structure** | Can span multiple files | Single file |
| **Complexity** | Can be elaborate | Should be simple |
| **Discovery** | Automatic | Explicit |

**Rule of thumb:**
- If you'd say "Claude should always know this" → **Skill**
- If you'd say "I want to run this when I choose" → **Slash Command**

---

## Deep Dive: Hooks

### What Are Hooks?

Hooks are **shell commands or prompts that execute automatically in response to events**. They run in the background, outside the conversation context.

### When to Use Hooks

✅ **Use Hooks when:**
- You need automation triggered by specific events
- Validation/linting after file changes
- Notifications when certain actions occur
- Session setup/teardown
- Blocking or modifying tool execution

❌ **Don't use Hooks when:**
- The automation should be conversational (use Skill or Subagent)
- Users should explicitly trigger it (use Slash Command)
- It needs access to conversation context (use Skill)
- Simple guidance or knowledge (use Skill)

### Hook Events

| Event | Trigger | Common Use Cases |
|-------|---------|------------------|
| **PreToolUse** | Before tool executes | Validation, modification, blocking |
| **PostToolUse** | After tool completes | Linting, notifications, logging |
| **PermissionRequest** | Permission dialog shown | Auto-approve/deny |
| **UserPromptSubmit** | User sends message | Validation, context injection |
| **Stop** | Claude finishes responding | Continuation logic, reminders |
| **SubagentStop** | Subagent finishes | Task completion checks |
| **Notification** | System notification | Custom alerts |
| **SessionStart** | Session begins | Setup, context loading |
| **SessionEnd** | Session ends | Cleanup, logging |
| **PreCompact** | Before context compaction | Custom compaction logic |

### Hook Configuration

```json
// settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",  // Regex pattern for tool names
        "hooks": [
          {
            "type": "command",
            "command": "/path/to/script.sh",
            "timeout": 30
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "prompt",
            "prompt": "Check if all tasks are complete: $ARGUMENTS"
          }
        ]
      }
    ]
  }
}
```

### Hook Types

#### 1. Command Hooks
Execute shell commands:
```json
{
  "type": "command",
  "command": "npm run lint -- $FILE_PATH",
  "timeout": 60
}
```

#### 2. Prompt Hooks
Use LLM to evaluate:
```json
{
  "type": "prompt",
  "prompt": "Evaluate if this action is safe: $ARGUMENTS"
}
```

### Hook Input/Output

**Hooks receive JSON via stdin:**
```json
{
  "session_id": "abc123",
  "hook_event_name": "PostToolUse",
  "tool_name": "Write",
  "tool_input": { "file_path": "/path/to/file.txt" },
  "tool_response": { "success": true }
}
```

**Hooks communicate via exit codes and stdout:**
| Exit Code | Meaning | Behavior |
|-----------|---------|----------|
| 0 | Success | Continue normally |
| 2 | Blocking error | Block action, show stderr to Claude |
| Other | Non-blocking error | Log warning, continue |

### Hook Execution Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    Tool Execution                            │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│              PreToolUse Hooks (if configured)               │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Validate parameters                               │    │
│  │ • Modify inputs                                     │    │
│  │ • Block execution (exit 2)                          │    │
│  │ • Allow/Ask for permission                          │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Tool Executes                             │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│              PostToolUse Hooks (if configured)              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ • Run linters/formatters                            │    │
│  │ • Send notifications                                │    │
│  │ • Log activity                                      │    │
│  │ • Provide feedback to Claude                        │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
```

---

## Comparison Matrix

### Feature Comparison

| Feature | Skills | Subagents | Slash Commands | Hooks |
|---------|--------|-----------|----------------|-------|
| **Trigger** | Automatic (Claude) | Delegated/Explicit | Explicit (`/cmd`) | Event-based |
| **Context** | Shared | Isolated | Injected | None |
| **Conversation aware** | ✅ Yes | ❌ Fresh start | ✅ Yes | ❌ No |
| **Can modify files** | ✅ Yes | ✅ Yes | ✅ Yes | ⚠️ Limited |
| **Can restrict tools** | ✅ Yes | ✅ Yes | ✅ Yes | N/A |
| **Supports arguments** | ❌ No | ✅ Yes | ✅ Yes | ✅ Via stdin |
| **Multi-file structure** | ✅ Yes | ❌ Single file | ❌ Single file | ❌ Config only |
| **Progressive disclosure** | ✅ Yes | ❌ No | ❌ No | N/A |
| **Resumable** | ❌ No | ✅ Yes | ❌ No | N/A |
| **Background execution** | ❌ No | ⚠️ Possible | ❌ No | ✅ Yes |

### Use Case Mapping

| Use Case | Best Mechanism | Why |
|----------|---------------|-----|
| Code review standards | **Skill** | Should auto-apply when reviewing |
| Deep security audit | **Subagent** | Needs focused context, specific tools |
| Create git commit | **Slash Command** | User chooses when to commit |
| Lint after file save | **Hook** | Automatic on file write event |
| Project conventions | **Skill** | Always-on guidance |
| Generate documentation | **Slash Command** | On-demand action |
| Complex refactoring | **Subagent** | Benefits from isolation |
| Session setup | **Hook** | Runs at session start |
| PR template | **Slash Command** | User invokes when creating PR |
| Test patterns | **Skill** | Auto-apply when writing tests |

### Context Flow Visualization

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         MAIN CONVERSATION                                │
│                                                                          │
│  User Input ──────► Claude + Skills ──────► Response                    │
│       │                    │                    │                        │
│       │                    │ (delegates)        │                        │
│       │                    ▼                    │                        │
│       │            ┌─────────────┐              │                        │
│       │            │  SUBAGENT   │              │                        │
│       │            │  (isolated) │              │                        │
│       │            └──────┬──────┘              │                        │
│       │                   │ (returns)           │                        │
│       │                   ▼                     │                        │
│       │            Results merged ◄─────────────┘                        │
│       │                                                                  │
│       │   /command ──────► Slash Command Prompt ──────► Response        │
│       │                                                                  │
└───────┼──────────────────────────────────────────────────────────────────┘
        │
        │ (events)
        ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                              HOOKS                                       │
│         (background execution, no conversation context)                  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Anti-Patterns to Avoid

### Anti-Pattern 1: Skill as Slash Command
**Problem:** Creating a Skill that only makes sense when explicitly invoked.

```yaml
# ❌ Bad: Should be a Slash Command
---
name: deploy-staging
description: Deploy to staging environment. Use when user says "deploy".
---
Run deployment pipeline for staging...
```

```markdown
# ✅ Good: As a Slash Command
# .claude/commands/deploy-staging.md
---
description: Deploy to staging environment
---
Run deployment pipeline for staging...
```

**Why:** Deployment is an explicit action, not ongoing knowledge.

### Anti-Pattern 2: Slash Command as Skill
**Problem:** Creating a Slash Command for something Claude should always know.

```markdown
# ❌ Bad: Should be a Skill
# .claude/commands/code-style.md
When writing code, always:
- Use 2-space indentation
- Add JSDoc comments
- Use TypeScript strict mode
```

```yaml
# ✅ Good: As a Skill
---
name: code-style
description: Code style and conventions. Use when writing or reviewing code.
---
When writing code, always:
- Use 2-space indentation...
```

**Why:** Code style should automatically apply without user invoking `/code-style` every time.

### Anti-Pattern 3: Subagent for Simple Knowledge
**Problem:** Using a Subagent when a Skill would suffice.

```yaml
# ❌ Bad: Overkill for simple knowledge
---
name: naming-conventions
description: Subagent for naming conventions
---
You are an expert in naming conventions...
```

```yaml
# ✅ Good: As a Skill
---
name: naming-conventions
description: Naming conventions for this project. Use when naming variables, functions, files.
---
## Naming Rules
- camelCase for variables...
```

**Why:** Naming conventions don't need isolated context; they should enhance the current conversation.

### Anti-Pattern 4: Hook for Conversational Logic
**Problem:** Using Hooks for things that should be conversational.

```json
// ❌ Bad: Hook for something Claude should discuss
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write",
      "hooks": [{
        "command": "echo 'Consider adding tests for this code'"
      }]
    }]
  }
}
```

```yaml
# ✅ Good: As a Skill
---
name: test-reminder
description: Reminds to write tests. Use after writing implementation code.
---
After writing implementation code, always suggest corresponding tests...
```

**Why:** Test reminders should be part of the conversation, not background messages.

### Anti-Pattern 5: Monolithic Skill
**Problem:** Putting everything into one massive Skill.

```yaml
# ❌ Bad: Trying to do everything
---
name: development-guide
description: Complete development guide covering code style, testing, deployment, security, performance, documentation, and architecture.
---
[2000 lines of content]
```

```yaml
# ✅ Good: Focused Skills
# skills/code-style/SKILL.md
# skills/testing/SKILL.md
# skills/security/SKILL.md
# skills/deployment/SKILL.md (or as Slash Command if action-oriented)
```

**Why:** Focused Skills are more discoverable and load only relevant content.

### Anti-Pattern 6: Forgetting About Built-in Subagents
**Problem:** Creating custom subagents for things built-in agents handle.

```yaml
# ❌ Bad: Duplicating built-in Explore agent
---
name: code-explorer
description: Explores codebase to find files and understand structure
tools: Read, Grep, Glob
model: haiku
---
```

**Why:** The built-in Explore subagent already does this optimally.

---

## Case Study: PACER Learning System

This section demonstrates the decision framework by implementing Justin Sung's PACER learning methodology.

### System Components and Their Mechanisms

#### 1. PACER Classification → **Skill**

**Why Skill?**
- Should auto-trigger when any learning content appears
- Core knowledge that enhances all learning conversations
- Doesn't need isolation—classification should inform the current discussion

```yaml
---
name: pacer-classifier
description: Classifies learning content into PACER categories (Procedural, Analogous, Conceptual, Evidence, Reference). Use when studying, learning, reading educational content, or processing information for retention.
---

# PACER Information Classification

When encountering learning content, classify each piece:

## P - Procedural (HOW)
Instructions for executing tasks. Protocol: Practice immediately.

## A - Analogous (LIKE)
Resembles existing knowledge. Protocol: Critique the analogy.

## C - Conceptual (WHAT)
Core theories and principles. Protocol: Create mind map.

## E - Evidence (PROOF)
Data validating concepts. Protocol: Store & apply to problems.

## R - Reference (MINUTIAE)
Arbitrary details. Protocol: Store in flashcards.
```

#### 2. GRINDE Mind Maps → **Skill + Slash Command**

**Why Both?**
- **Skill**: Claude should know GRINDE principles when mapping comes up
- **Slash Command**: User may want to explicitly generate a map

```yaml
# Skill: ~/.claude/skills/grinde-mapper/SKILL.md
---
name: grinde-mapper
description: GRINDE mind mapping methodology for higher-order learning. Use when creating mind maps, organizing concepts, or visualizing knowledge structures.
---
# GRINDE Principles
G - Grouped: Organize into chunks
R - Reflective: Ask "why does this matter?"
I - Interconnected: Draw relationships
N - Non-verbal: Use symbols over words
D - Directional: Show cause-effect
E - Emphasized: Highlight importance
```

```markdown
# Slash Command: ~/.claude/commands/grinde.md
---
description: Generate a GRINDE-style mind map
argument-hint: [topic or content]
---
Create a GRINDE mind map for: $ARGUMENTS
Apply all 6 principles (Grouped, Reflective, Interconnected, Non-verbal, Directional, Emphasized).
```

#### 3. Deep Learning Analysis → **Subagent**

**Why Subagent?**
- Complex analysis benefits from focused context
- Should analyze without polluting main conversation
- Needs dedicated tool access for thorough review

```yaml
# ~/.claude/agents/learning-analyzer.md
---
name: learning-analyzer
description: Deep analysis of learning content using PACER methodology. Use PROACTIVELY when user has substantial learning material to process.
tools: Read, Grep, Glob, WebFetch
model: sonnet
skills: pacer-classifier, layer-learning
---

You are a learning science expert. When analyzing content:

1. **Classify** all information using PACER
2. **Structure** using 4 Layers of Learning (Logic → Concepts → Details)
3. **Recommend** digestion protocols for each section
4. **Identify** encoding vs retrieval balance needs

Output a comprehensive learning plan with time allocation and priorities.
```

#### 4. Digestion Protocols → **Slash Commands**

**Why Slash Commands?**
- User should choose when to execute digestion
- Each protocol is a distinct action
- Arguments specify what to digest

```markdown
# ~/.claude/commands/digest.md
---
description: Execute PACER digestion protocol
argument-hint: [P|A|C|E|R] [content description]
---
Execute digestion protocol for type: $1

Content: $ARGUMENTS

Protocols:
- P (Procedural): Generate practice exercises
- A (Analogous): Create critique questions
- C (Conceptual): Build GRINDE map
- E (Evidence): Format for second-brain + scenarios
- R (Reference): Generate Anki flashcards
```

#### 5. Balance Tracking → **Hook**

**Why Hook?**
- Should track automatically in background
- Responds to Read events (consumption) and Write events (digestion)
- Doesn't need conversational context

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Read|WebFetch",
        "hooks": [{
          "type": "command",
          "command": "echo \"$(date +%s),consumption\" >> ~/.claude/learning-balance.log"
        }]
      },
      {
        "matcher": "Write",
        "hooks": [{
          "type": "command",
          "command": "echo \"$(date +%s),digestion\" >> ~/.claude/learning-balance.log"
        }]
      }
    ],
    "Stop": [
      {
        "hooks": [{
          "type": "prompt",
          "prompt": "Review if this learning session had balanced consumption and digestion. If heavily imbalanced toward consumption, remind user to digest before ending."
        }]
      }
    ]
  }
}
```

### Implementation Summary Table

| PACER Component | Mechanism | Justification |
|----------------|-----------|---------------|
| PACER Classification | **Skill** | Auto-apply knowledge when learning |
| 4 Layers of Learning | **Skill** | Auto-catch improper sequencing |
| Encoding-First Strategy | **Skill** | Auto-intervene when over-retrieval detected |
| GRINDE Map Knowledge | **Skill** | Core mapping methodology |
| Generate GRINDE Map | **Slash Command** | Explicit "make me a map" action |
| Execute Digestion | **Slash Command** | User-initiated protocol execution |
| Check Balance | **Slash Command** | On-demand session review |
| Generate Flashcards | **Slash Command** | User chooses when to make cards |
| Deep Content Analysis | **Subagent** | Complex analysis needing isolation |
| Digestion Coaching | **Subagent** | Interactive guidance session |
| Learner Diagnostic | **Subagent** | Complex multi-dimension assessment |
| Consumption Tracking | **Hook** | Background event logging |
| Digestion Reminder | **Hook** | Auto-prompt on session end |

---

## Advanced Patterns

### Pattern 1: Skill + Slash Command Combo
When you need both automatic knowledge AND explicit invocation:

```
~/.claude/
├── skills/
│   └── code-review/
│       └── SKILL.md          # Auto-triggers during reviews
└── commands/
    └── review.md             # Explicit /review command
```

The Skill provides ongoing knowledge; the command provides on-demand action.

### Pattern 2: Subagent with Preloaded Skills
Subagents can load specific Skills:

```yaml
---
name: security-auditor
skills: secure-coding, owasp-top-10, dependency-check
---
```

This gives the subagent specialized knowledge while maintaining isolated context.

### Pattern 3: Hook Chain
Multiple hooks can respond to the same event:

```json
{
  "PostToolUse": [
    {
      "matcher": "Write",
      "hooks": [
        { "command": "npm run lint" },
        { "command": "npm run format" },
        { "command": "echo 'File written' >> activity.log" }
      ]
    }
  ]
}
```

All hooks run in parallel.

### Pattern 4: Conditional Skill Loading
Use description keywords to control when Skills activate:

```yaml
---
name: react-patterns
description: React component patterns and best practices. Use when working with React, JSX, hooks, or component architecture.
---
```

Claude only loads this when the conversation involves React.

### Pattern 5: Plugin Distribution
Package multiple mechanisms as a plugin:

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── my-skill/
│       └── SKILL.md
├── agents/
│   └── my-agent.md
├── commands/
│   └── my-command.md
└── hooks/
    └── hooks.json
```

---

## Quick Reference

### Decision Checklist

```
□ Should Claude automatically recognize when to apply this?
  → YES: Skill
  → NO: Continue...

□ Should it run in isolated context for complex analysis?
  → YES: Subagent
  → NO: Continue...

□ Should the user explicitly invoke it?
  → YES: Slash Command
  → NO: Continue...

□ Should it respond to system events?
  → YES: Hook
  → NO: Reconsider requirements
```

### File Locations Quick Reference

| Mechanism | Project Location | Personal Location |
|-----------|-----------------|-------------------|
| Skills | `.claude/skills/name/SKILL.md` | `~/.claude/skills/name/SKILL.md` |
| Subagents | `.claude/agents/name.md` | `~/.claude/agents/name.md` |
| Slash Commands | `.claude/commands/name.md` | `~/.claude/commands/name.md` |
| Hooks | `.claude/settings.json` | `~/.claude/settings.json` |

### Trigger Types Summary

| Mechanism | Trigger | User Action Required |
|-----------|---------|---------------------|
| **Skill** | Claude matches context to description | None (automatic) |
| **Subagent** | Claude delegates OR user requests | Optional |
| **Slash Command** | User types `/command` | Always |
| **Hook** | System event fires | None (automatic) |

### When in Doubt

1. **Start with a Skill** - Most guidance/knowledge should be Skills
2. **Graduate to Subagent** - If it needs isolation or gets complex
3. **Use Slash Commands** - For explicit user actions
4. **Add Hooks** - For automation and validation

---

## Conclusion

The key to effective Claude Code extension is matching the **trigger type** to the **use case**:

- **Knowledge that should always apply** → Skill
- **Complex specialized tasks** → Subagent
- **Explicit user actions** → Slash Command
- **Event-based automation** → Hook

By following this framework, you create extensions that feel natural, load only when needed, and provide the right level of automation for each use case.

---

## References

- [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills.md)
- [Claude Code Subagents Documentation](https://code.claude.com/docs/en/sub-agents.md)
- [Claude Code Slash Commands Documentation](https://code.claude.com/docs/en/slash-commands.md)
- [Claude Code Hooks Documentation](https://code.claude.com/docs/en/hooks.md)
- [Claude Code Plugins Documentation](https://code.claude.com/docs/en/plugins.md)
