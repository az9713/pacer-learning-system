# PACER Classification Examples

Real-world examples for each PACER category to guide accurate classification.

---

## P - Procedural Examples

### Example 1: Programming Tutorial
```
"To create a React component, first import React, then define a function
that returns JSX, and finally export the component."
```
**Classification**: P - Procedural
**Reasoning**: Step-by-step instructions for executing a coding task
**Protocol**: Practice by immediately creating a React component

### Example 2: Clinical Examination
```
"When performing a cardiovascular exam: 1) Inspect for jugular venous
distension, 2) Palpate the precordium, 3) Auscultate in the four cardiac areas"
```
**Classification**: P - Procedural
**Reasoning**: Instructions for performing a physical examination
**Protocol**: Practice on simulation or with supervision immediately

### Example 3: Recipe
```
"To make roux: melt butter over medium heat, add equal parts flour,
whisk constantly for 2-3 minutes until golden brown"
```
**Classification**: P - Procedural
**Reasoning**: Step-by-step cooking technique
**Protocol**: Go to kitchen and make roux now

---

## A - Analogous Examples

### Example 1: Mitochondria Analogy
```
"Mitochondria are like the powerhouse of the cell, converting nutrients
into energy just like a power plant converts fuel into electricity."
```
**Classification**: A - Analogous
**Reasoning**: Comparison to something familiar (power plant)
**Critique Questions**:
- How accurate? Both convert input to energy output - fairly accurate
- Where does it break down? Cells have many mitochondria; cities have few power plants. Scale is different.

### Example 2: Computer Memory Analogy
```
"RAM is like a desk where you do your work - it's fast to access but
limited in space. Storage is like a filing cabinet - more space but
slower to retrieve."
```
**Classification**: A - Analogous
**Reasoning**: Familiar objects used to explain technical concepts
**Critique Questions**:
- How accurate? Speed/accessibility trade-off is captured well
- Where does it break down? Desk doesn't lose contents when you leave; RAM does (volatile)

### Example 3: Nested Analogy in Procedural Content
```
"When debugging, think of it like being a detective - follow the clues
(error messages), interview witnesses (log files), and reconstruct the crime
(trace execution). Start by reproducing the bug..."
```
**Classification**: P with embedded A
**Reasoning**: Procedural (how to debug) with detective analogy
**Protocol**: Practice debugging, but also critique the detective metaphor

---

## C - Conceptual Examples

### Example 1: Supply and Demand
```
"The law of supply and demand states that when supply exceeds demand,
prices fall; when demand exceeds supply, prices rise. The equilibrium
point is where supply and demand curves intersect."
```
**Classification**: C - Conceptual
**Reasoning**: Core economic principle explaining relationships
**Protocol**: Create mind map showing supply/demand curves, factors affecting each, equilibrium dynamics

### Example 2: Natural Selection
```
"Natural selection operates on three principles: variation exists within
populations, some variations improve survival/reproduction, and these
variations are heritable. Over generations, beneficial traits become
more common."
```
**Classification**: C - Conceptual
**Reasoning**: Foundational theory explaining biological mechanisms
**Protocol**: Map the relationships between variation, selection pressure, heritability, and population change

### Example 3: Object-Oriented Programming
```
"Object-oriented programming is based on four pillars: encapsulation
(bundling data and methods), inheritance (deriving new classes from
existing ones), polymorphism (same interface, different implementations),
and abstraction (hiding complexity behind simple interfaces)."
```
**Classification**: C - Conceptual
**Reasoning**: Abstract principles underlying a programming paradigm
**Protocol**: Create GRINDE map connecting the four pillars and how they interact

---

## E - Evidence Examples

### Example 1: Research Statistic
```
"A 2023 meta-analysis found that spaced repetition improved long-term
retention by 47% compared to massed practice (p < 0.001, n = 12,847)."
```
**Classification**: E - Evidence
**Reasoning**: Statistical data supporting the concept of spaced repetition
**Protocol**: Store in notes, create practice problem: "If baseline retention is X%, what would spaced repetition achieve?"

### Example 2: Case Study
```
"Toyota's implementation of lean manufacturing in the 1970s reduced
production defects by 60% and inventory costs by 75%, demonstrating
the practical value of just-in-time production."
```
**Classification**: E - Evidence
**Reasoning**: Real-world case supporting lean manufacturing concepts
**Protocol**: Store in second-brain, link to concepts of JIT and lean methodology

### Example 3: Clinical Trial Results
```
"The RECOVERY trial showed that dexamethasone reduced 28-day mortality
in COVID-19 patients on ventilators by 35% (rate ratio 0.65, 95% CI 0.51-0.82)."
```
**Classification**: E - Evidence
**Reasoning**: Clinical evidence supporting treatment efficacy
**Protocol**: Store for reference, create application scenario: "When should dexamethasone be considered?"

---

## R - Reference Examples

### Example 1: Historical Date
```
"World War I began on July 28, 1914, when Austria-Hungary declared war on Serbia."
```
**Classification**: R - Reference
**Reasoning**: Specific date with low conceptual value on its own
**Protocol**: Create flashcard only if you must recall this date from memory

### Example 2: Physical Constant
```
"The speed of light in a vacuum is exactly 299,792,458 meters per second."
```
**Classification**: R - Reference
**Reasoning**: Precise numerical value to look up when needed
**Protocol**: Don't memorize; know it's ~3×10^8 m/s for estimation, look up exact value when needed

### Example 3: Medical Dosage
```
"The standard adult dose of amoxicillin for respiratory infections
is 500mg every 8 hours or 875mg every 12 hours."
```
**Classification**: R - Reference
**Reasoning**: Specific values that should be verified from authoritative sources
**Protocol**: Reference in clinical resources; don't rely on memory for dosing

---

## Mixed Content Example

Consider this paragraph about muscle physiology:

```
"Skeletal muscle contraction occurs through the sliding filament theory (C).
When calcium ions are released from the sarcoplasmic reticulum, they bind
to troponin, causing tropomyosin to shift and expose binding sites on actin (C).
This is similar to a key opening a lock (A). ATP then powers the myosin heads
to pull the actin filaments inward (C). To perform a bicep curl correctly,
keep your elbow stationary and curl the weight toward your shoulder (P).
Studies show that eccentric contractions cause 40% more muscle damage than
concentric ones (E). The sarcomere, the basic unit of muscle contraction,
is approximately 2.5 micrometers long at rest (R)."
```

**Breakdown**:
| Content | Category | Protocol |
|---------|----------|----------|
| Sliding filament theory mechanism | C | Map the process |
| Calcium-troponin-tropomyosin cascade | C | Map relationships |
| "Like a key opening a lock" | A | Critique: where does it break? |
| Bicep curl technique | P | Practice the movement |
| 40% more muscle damage statistic | E | Store, create application scenario |
| 2.5 micrometer sarcomere length | R | Flashcard if exam requires it |
