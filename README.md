# PACER Learning System

A Claude Code extension implementing Dr. Justin Sung's PACER methodology for efficient learning.

## What is This?

This project helps you **learn more efficiently** by:

1. **Classifying information** into 5 types (P/A/C/E/R)
2. **Applying the right strategy** for each type
3. **Creating mind maps** for deep understanding
4. **Preventing common mistakes** like over-flashcarding

### The Core Insight

> "Lots of retrieval without proper encoding is like filling a leaky bucket faster."

Most people try to memorize everything with flashcards. But proper **encoding** (understanding) makes retention easy. This system teaches you when to understand vs. when to memorize.

## Quick Start

### 1. Install Claude Code

If you haven't already, install Claude Code from https://claude.ai/code

### 2. Navigate to This Project

```bash
cd path/to/pacer_bestpartnerstv
```

### 3. Start Claude

```bash
claude
```

### 4. Try It Out

Ask Claude to classify some learning content:

```
Classify this for learning:

"Photosynthesis converts light energy to chemical energy using
chloroplasts in plant cells."
```

Claude will identify this as **Conceptual** content and recommend creating a mind map rather than flashcards.

## The PACER Types

| Type | What It Is | What To Do |
|------|------------|------------|
| **P**rocedural | Skills, techniques | Practice it |
| **A**nalogous | Comparisons, metaphors | Critique it |
| **C**onceptual | Ideas, theories | Understand it |
| **E**vidence | Data, examples | Connect it |
| **R**eference | Arbitrary facts | Memorize (last resort!) |

## Available Commands

| Command | Purpose |
|---------|---------|
| Ask to classify | Break content into P/A/C/E/R |
| Ask for GRINDE map | Create visual concept map |
| Ask to digest | Process by type |
| Ask for balance check | Check consumption vs digestion |
| Ask for layer check | Verify understanding depth |
| Ask for flashcards | Generate R-type cards only |

## Documentation

| Document | Description | Who It's For |
|----------|-------------|--------------|
| [Quick Start Guide](docs/QUICK_START.md) | 10 hands-on tutorials | Everyone (start here!) |
| [User Guide](docs/USER_GUIDE.md) | Complete usage guide | All users |
| [Developer Guide](docs/DEVELOPER_GUIDE.md) | Technical deep dive | Developers |
| [Troubleshooting](docs/TROUBLESHOOTING.md) | Common issues & fixes | Anyone stuck |

## Project Structure

```
pacer_bestpartnerstv/
├── .claude/
│   ├── skills/           # Auto-triggered learning strategies
│   │   ├── pacer-classifier/
│   │   ├── grinde-mapper/
│   │   ├── layer-learning/
│   │   └── encoding-first/
│   ├── agents/           # Specialized subagents
│   ├── commands/         # User-invoked commands
│   └── settings.json     # Hooks configuration
├── docs/                 # Documentation
├── CLAUDE.md             # Project context for Claude
└── README.md             # You are here
```

## Why This Works

Traditional study approaches focus on **retrieval** (testing, flashcards). But without proper **encoding** first, you're fighting a steep forgetting curve.

This system ensures you:
1. **Understand** before memorizing
2. **Practice** procedures instead of flashcarding them
3. **Critique** analogies instead of accepting blindly
4. **Minimize** true memorization to what's necessary

The result: Less time studying, better retention.

## Getting Help

1. **Quick questions**: Ask Claude - it knows this system
2. **Step-by-step help**: See [Quick Start Guide](docs/QUICK_START.md)
3. **Detailed reference**: See [User Guide](docs/USER_GUIDE.md)
4. **Something broken?**: See [Troubleshooting](docs/TROUBLESHOOTING.md)
5. **Want to contribute?**: See [Developer Guide](docs/DEVELOPER_GUIDE.md)

## Credits

Based on the learning methodology of **Dr. Justin Sung**:
- PACER classification system
- GRINDE mind mapping
- 4 Layers of Learning
- Encoding-first philosophy

## License

This project is for educational purposes.

---

**Ready to learn efficiently?** Start with the [Quick Start Guide](docs/QUICK_START.md)!
