# PACER Learning System - Claude Code Project

## Project Overview

This is a **Claude Code extension system** implementing Dr. Justin Sung's PACER learning methodology. It helps users learn more efficiently by classifying information types and applying appropriate encoding strategies.

**Key Insight**: Most people over-rely on flashcards and retrieval practice. This system promotes proper encoding FIRST, which makes retention much easier.

## What This Project Does

1. **Classifies information** into 5 types (PACER):
   - **P**rocedural - Skills to practice
   - **A**nalogous - Comparisons to critique
   - **C**onceptual - Ideas to understand
   - **E**vidence - Data supporting concepts
   - **R**eference - Arbitrary facts (minimize!)

2. **Guides digestion** with type-specific protocols
3. **Creates GRINDE mind maps** for deep encoding
4. **Tracks learning balance** between consumption and digestion
5. **Prevents common mistakes** like premature flashcard creation

## Project Structure

```
.claude/
├── skills/           # Auto-triggered learning strategies
│   ├── pacer-classifier/
│   ├── grinde-mapper/
│   ├── layer-learning/
│   └── encoding-first/
├── agents/           # Specialized subagents
│   ├── learning-analyzer.md
│   ├── digestion-coach.md
│   └── learner-diagnostic.md
├── commands/         # User-invoked slash commands
│   ├── pacer.md
│   ├── grinde.md
│   ├── digest.md
│   ├── balance-check.md
│   ├── layer-check.md
│   └── flashcards.md
├── settings.json     # Hooks configuration
└── settings.local.json  # Local permissions

docs/
├── PACER_RESEARCH_COMPREHENSIVE.md    # Full methodology research
├── IMPLEMENTATION_ARCHITECTURE.md      # Technical architecture
└── CLAUDE_CODE_EXTENSION_ARCHITECTURE.md  # Educational guide
```

## Key Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `/pacer` | Classify content | "Classify this article" |
| `/grinde` | Create mind map | "Map photosynthesis" |
| `/digest` | Process content | "Practice this procedure" |
| `/balance-check` | Check learning balance | After reading session |
| `/layer-check` | Verify understanding layers | "Check my physics knowledge" |
| `/flashcards` | Generate R-type cards | For truly arbitrary facts |

## When Working on This Project

### Adding New Features
1. Determine the appropriate mechanism (Skill, Agent, Command, Hook)
2. Follow existing file patterns in `.claude/` directories
3. Update this CLAUDE.md with new capabilities
4. Test with real learning content

### Modifying Existing Components
- Skills: Edit SKILL.md files, keep `description` field accurate for auto-triggering
- Commands: Follow the markdown template format
- Agents: Maintain the YAML frontmatter structure

### Key Principles to Maintain
1. **Encoding before retrieval** - Never suggest flashcards before understanding
2. **Minimize R-type** - Challenge any Reference classification
3. **Layer sequence** - Logic → Concepts → Details → Arbitrary
4. **Balance awareness** - Track consumption vs digestion

## Testing

Test each component by:
1. **Skills**: Discuss learning topics - should auto-activate
2. **Commands**: Type `/command-name` with sample content
3. **Agents**: Request "Use learning-analyzer to..."
4. **Hooks**: Read files, check if balance.log updates

## Dependencies

- Claude Code CLI (latest version)
- No external packages required
- Works on Windows, macOS, Linux

## Documentation

- `docs/USER_GUIDE.md` - Complete user documentation
- `docs/DEVELOPER_GUIDE.md` - Technical developer guide
- `docs/QUICK_START.md` - 10 use case tutorials
- `docs/TROUBLESHOOTING.md` - Common issues and solutions

## Important Notes

- Skills auto-trigger based on conversation context
- Commands require explicit `/command` invocation
- Hooks run automatically on tool events
- The system is designed to PREVENT over-reliance on memorization
