---
name: code-refactoring
description: >
  Apply Martin Fowler's "Refactoring" methodology to analyze and restructure code. Use this
  skill whenever the user asks to refactor, clean up, restructure, improve, or redesign existing
  code — even if they don't use the word "refactor". Triggers include: "this function is too long",
  "there's a lot of duplication here", "can you clean this up?", "make this more readable",
  "simplify this logic", "break this apart", "this smells bad", "restructure this", or any request
  involving existing code that needs to be improved without changing its behavior. Also use when
  the user asks about code smells, design patterns applied to existing code, or wants guidance on
  where to start improving a codebase.
---
 
# Code Refactoring Skill
 
Refactor code safely and systematically using Martin Fowler's catalog of named refactoring techniques.
 
## Core Rules — Always Follow These
 
1. **Small steps only.** Apply one named refactoring at a time. Compile and test after each step.
2. **Wear the refactoring hat.** Do not add features or fix bugs during a refactoring pass. Restructure only.
3. **Preserve behavior.** Every transformation must leave observable behavior unchanged.
4. **Name the technique.** Always tell the user which named refactoring you're applying (e.g., "Applying *Extract Function* here").
---
 
## Step 1: Diagnose — Identify Code Smells
 
Before touching any code, scan for these smells and call them out explicitly:
 
| Smell | Signs | Primary Fix |
|---|---|---|
| **Mysterious Name** | Variable, function, or field name doesn't reveal intent | Rename Variable / Rename Function |
| **Long Function** | Function does more than one thing; hard to read in one screen | Extract Function |
| **Duplicated Code** | Same logic appears in two or more places | Extract Function, Slide Statements |
| **Long Parameter List** | Function takes many parameters, hard to call correctly | Introduce Parameter Object, Preserve Whole Object |
| **Mutable Data** | Variable updated in many places, hard to track | Encapsulate Variable, Separate Query from Modifier |
| **Feature Envy** | Function accesses another module's data more than its own | Move Function |
| **Data Clumps** | Same group of fields always appear together | Extract Class, Introduce Parameter Object |
| **Switch / Nested Conditionals** | Complex if/switch chains based on type | Decompose Conditional, Replace Conditional with Polymorphism |
| **Divergent Change** | One class changes for many different reasons | Split Phase, Extract Class |
| **Speculative Generality** | Abstractions for hypothetical future use | Inline Function, Inline Class |
 
Report every smell found, grouped by category, before proposing any changes.
 
---
 
## Step 2: Map Smells to Named Refactorings
 
Use only techniques from Fowler's catalog. Reference the right category:
 
### The Basics
- **Extract Function** — Pull code into a new function named after its *intent*, not its *mechanics*. Mechanics: (1) create function named after intent, (2) copy code, (3) identify local variables and pass as parameters, (4) replace original with call.
- **Inline Function** — Remove needless indirection when a function body is as clear as its name.
- **Extract Variable** — Name a complex expression to make it readable.
- **Split Phase** — Separate code that does two sequential things into two distinct phases with a clear handoff.
### Encapsulation
- **Encapsulate Variable** — Route all reads/writes through accessor functions.
- **Encapsulate Record / Collection** — Hide internal data structures behind a class interface.
- **Replace Primitive with Object** — Promote bare strings/numbers to domain objects when they accumulate behavior.
### Moving Features
- **Move Function** — Place function in the module whose data it uses most.
- **Move Field** — Place field where the data it belongs to lives.
- **Split Loop** — Separate a loop doing two things into two loops.
- **Replace Loop with Pipeline** — Convert loops into filter/map/reduce chains for clarity.
### Organizing Data
- **Split Variable** — Give each variable exactly one responsibility; never reuse a variable for two purposes.
- **Replace Derived Variable with Query** — Remove variables that can be computed on demand.
- **Rename Field / Variable** — When the name doesn't reveal intent.
### Simplifying Conditional Logic
- **Decompose Conditional** — Extract condition and each branch into named functions.
- **Replace Nested Conditional with Guard Clauses** — Use early returns to handle exceptional cases first, leaving the happy path clean.
- **Replace Conditional with Polymorphism** — When the same if/switch appears in multiple places based on type, use subclasses or strategy objects instead.
- **Introduce Special Case (Null Object)** — Replace repeated null/special-value checks with a dedicated object.
### Refactoring APIs
- **Parameterize Function** — Merge similar functions that differ only by a literal value.
- **Remove Flag Argument** — Split a function with a boolean parameter into two explicit functions.
- **Preserve Whole Object** — Pass the record, not a list of extracted fields.
- **Separate Query from Modifier** — Never let a function both return a value and cause side effects.
### Inheritance
- **Pull Up Method / Field** — Move shared behavior to the superclass.
- **Extract Superclass** — Create a new parent to share common interface/behavior.
- **Replace Subclass with Delegate** — Swap inheritance for composition when the hierarchy is being abused.
---
 
## Step 3: Present a Refactoring Plan
 
Before writing any code, output a plan in this format:
 
```
REFACTORING PLAN
================
Smells detected:
  1. [Smell name] — [location] — [one-line description]
  2. ...
 
Proposed refactorings (in order):
  Step 1: [Technique name] — [what and why]
  Step 2: [Technique name] — [what and why]
  ...
 
Tests needed before starting:
  - [describe what behavior must be covered]
```
 
Ask the user to confirm before proceeding.
 
---
 
## Step 4: Execute — One Step at a Time
 
For each step in the plan:
 
1. State: *"Applying [Technique Name]."*
2. Show the before code.
3. Show the after code.
4. Explain what changed and why it preserves behavior.
5. Note what test(s) should be run before the next step.
Do not batch multiple refactorings into one code block unless they are mechanically inseparable.
 
---
 
## Step 5: Summarize
 
After all steps, provide:
- A summary list of every named refactoring applied.
- The smells that remain (if any were deferred).
- Suggested next refactoring opportunities if the code warrants a second pass.