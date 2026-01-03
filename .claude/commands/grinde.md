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
| **G** | Grouped | Chunk related information into visual boxes |
| **R** | Reflective | Add "Why?" annotations and personal understanding |
| **I** | Interconnected | Show relationships with arrows and lines |
| **N** | Non-verbal | Use symbols, emojis, visual elements |
| **D** | Directional | Show flow, hierarchy, cause-effect |
| **E** | Emphasized | Mark importance levels (★★★, ★★, ★) |

### Output Format

```markdown
## GRINDE Map: [Topic]

### The Backbone
[1-2 sentence core insight that holds everything together]

### Map

═══════════════════════════════════════════════════════════════
                    ★★★ [MAIN TOPIC] ★★★
═══════════════════════════════════════════════════════════════

┌─────────────────────────────────────┐
│  ★★ [Major Chunk 1]                 │
│                                     │
│  • Key point                        │
│  • Key point                        │
│                                     │
│  Why: [explanation]                 │
└────────────────┬────────────────────┘
                 │
                 │ [relationship]
                 ▼
┌─────────────────────────────────────┐
│  ★★ [Major Chunk 2]                 │
│                                     │
│  • Key point                        │
│  • Key point                        │
│                                     │
│  Why: [explanation]                 │
└─────────────────────────────────────┘

═══════════════════════════════════════════════════════════════
★★★ BACKBONE: [Core insight summary] ★★★
═══════════════════════════════════════════════════════════════

### Connections
• [Chunk 1] → [relationship] → [Chunk 2]
• [Link to prior knowledge]

### Understanding Check
- Q: [Question testing deep understanding]
- Q: [Application question]
```

### Map Construction Steps

1. **Identify the Backbone** (most important first)
   - What's the ONE core insight?
   - What holds everything together?

2. **Chunk into Major Groups** (G)
   - What are the 3-5 main components?
   - Group related details together

3. **Add Reflections** (R)
   - Why does each chunk matter?
   - How does it connect to the backbone?

4. **Draw Connections** (I)
   - What flows into what?
   - What causes what?

5. **Add Visual Elements** (N)
   - Emojis for quick recognition
   - Box styles for different types

6. **Show Direction** (D)
   - Arrows for causation
   - Hierarchy for importance

7. **Mark Importance** (E)
   - ★★★ = Critical
   - ★★ = Important
   - ★ = Supporting

### Visual Elements Library

```
Boxes:
┌───────┐  ╔═══════╗  ┏━━━━━━━┓
│ basic │  ║ double ║  ┃ heavy ┃
└───────┘  ╚═══════╝  ┗━━━━━━━┛

Arrows:
→ ← ↑ ↓ ↔ ↕
▶ ◀ ▲ ▼
└──► ──┘ ┌── ──┐

Connectors:
├── ──┤ ┬ ┴ ┼
╠══ ══╣ ╦ ╩ ╬

Emphasis:
★★★ ★★ ★
⚡ 💡 ⚠️ ✅ ❌
```

## Example

```
/grinde supply and demand
```

Output:
```markdown
## GRINDE Map: Supply and Demand

### The Backbone
Opposing forces (buyers want low prices, sellers want high) create equilibrium; deviations self-correct through market pressure.

### Map

═══════════════════════════════════════════════════════════════
                    ★★★ SUPPLY & DEMAND ★★★
                   (Market Price Discovery)
═══════════════════════════════════════════════════════════════

┌─────────────────────────┐         ┌─────────────────────────┐
│  ★★ DEMAND (Buyers)     │         │  ★★ SUPPLY (Sellers)    │
│                         │         │                         │
│  📉 Downward slope      │         │  📈 Upward slope        │
│  • Price ↑ → Qty ↓      │         │  • Price ↑ → Qty ↑      │
│  • Price ↓ → Qty ↑      │         │  • Price ↓ → Qty ↓      │
│                         │         │                         │
│  Why: Buyers want deals │         │  Why: Profit motive     │
└────────────┬────────────┘         └────────────┬────────────┘
             │                                   │
             │          INTERSECT AT             │
             └──────────────┬────────────────────┘
                            │
                            ▼
             ┌──────────────────────────────┐
             │  ★★★ EQUILIBRIUM             │
             │  ⚖️ Where curves cross       │
             │                              │
             │  • Quantity supplied = Qd    │
             │  • Market clears             │
             │                              │
             │  Why: Stable point - no      │
             │       pressure to change     │
             └──────────────┬───────────────┘
                            │
          ┌─────────────────┼─────────────────┐
          ▼                                   ▼
┌──────────────────┐               ┌──────────────────┐
│ ★ SHORTAGE       │               │ ★ SURPLUS        │
│                  │               │                  │
│ Price < Equil    │               │ Price > Equil    │
│ Qd > Qs ⚡       │               │ Qs > Qd         │
│ → Price rises ↑  │               │ → Price falls ↓  │
│                  │               │                  │
│ Why: Competition │               │ Why: Sellers     │
│ among buyers     │               │ compete for sales│
└────────┬─────────┘               └─────────┬────────┘
         │                                   │
         └──────────► returns to ◄───────────┘
                    equilibrium

═══════════════════════════════════════════════════════════════
★★★ BACKBONE: Market forces naturally push prices toward
    equilibrium where supply meets demand ★★★
═══════════════════════════════════════════════════════════════

### Connections
• Demand curve ↔ Supply curve (opposing slopes create tension)
• Disequilibrium → Market pressure → Return to equilibrium
• Similar to: thermostat (self-correcting system)

### Understanding Check
- Q: Why does a shortage cause prices to rise?
- Q: If the government sets a price below equilibrium, what happens?
- Q: How would a new competitor entering the market affect equilibrium?
```
