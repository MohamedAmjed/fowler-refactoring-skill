# Code Refactoring Skill

A reusable Agent Skill for safe, systematic code refactoring based on Martin Fowler’s named refactoring techniques.

This skill helps an AI coding agent improve existing code structure, readability, and maintainability without changing observable behavior.

## What It Does

`code-refactoring` guides the agent through a disciplined refactoring workflow:

1. Identify code smells before changing code.
2. Map each smell to a named Fowler-style refactoring.
3. Present a refactoring plan before editing.
4. Apply one refactoring at a time.
5. Explain why behavior is preserved.
6. Recommend tests after each step.

The skill is intentionally conservative. It does not add features, rewrite code from scratch, or mix bug fixes with refactoring work.

## When to Use It

Use this skill when working with existing code that needs to be improved without changing behavior.

Typical prompts include:

- “Refactor this function.”
- “Clean this up.”
- “Make this more readable.”
- “Break this long function apart.”
- “There is duplicated logic here.”
- “This code smells bad.”
- “Simplify this conditional logic.”
- “Where should I start improving this codebase?”

It also applies when reviewing code smells, improving module boundaries, or applying design patterns to existing code.

## How the Skill Works

The agent follows a five-step flow.

### 1. Diagnose

Before editing, the agent scans the code for common smells such as:

- Mysterious Name
- Long Function
- Duplicated Code
- Long Parameter List
- Mutable Data
- Feature Envy
- Data Clumps
- Switch Statements or Nested Conditionals
- Divergent Change
- Speculative Generality

### 2. Map

Each smell is mapped to a named refactoring technique, such as:

- Extract Function
- Inline Function
- Extract Variable
- Split Phase
- Encapsulate Variable
- Move Function
- Split Loop
- Replace Loop with Pipeline
- Decompose Conditional
- Replace Nested Conditional with Guard Clauses
- Introduce Parameter Object
- Remove Flag Argument
- Separate Query from Modifier
- Replace Conditional with Polymorphism

### 3. Plan

Before modifying code, the agent produces a refactoring plan:

```text
REFACTORING PLAN
================
Smells detected:
  1. [Smell name] — [location] — [one-line description]

Proposed refactorings, in order:
  Step 1: [Technique name] — [what will change and why]

Tests needed before starting:
  - [behavior that must remain unchanged]
```

### 4. Execute

The agent applies one named refactoring at a time.

For each step, it shows:

- The technique being applied
- Before code
- After code
- What changed
- Why behavior is preserved
- Tests to run before continuing

### 5. Summarize

At the end, the agent summarizes:

- Refactorings applied
- Code smells resolved
- Code smells left for later
- Suggested next refactoring pass

## Installation

### Using the Skills CLI

Install this skill directly from GitHub:

```bash
npx skills add MohamedAmjed/fowler-refactoring-skill --skill code-refactoring
```

To install all skills from this repository:

```bash
npx skills add MohamedAmjed/fowler-refactoring-skill --all
```

Repository:

```text
https://github.com/MohamedAmjed/fowler-refactoring-skill
```

### Manual Installation

Copy the skill folder into your agent’s skills directory.

Recommended structure:

```text
skills/
└── code-refactoring/
    ├── SKILL.md
    └── README.md
```

The required file is `SKILL.md`. This README is for humans browsing the repository.

## Skill File

The core skill lives in `SKILL.md` and includes:

- YAML frontmatter with `name` and `description`
- Activation guidance
- Refactoring rules
- Code smell diagnosis table
- Fowler-style refactoring catalog
- Required response format
- Step-by-step execution protocol

## Example Usage

```text
Refactor this function. Keep the behavior the same and explain each step.
```

```text
This module has too much duplicated validation logic. Can you clean it up safely?
```

```text
Analyze this code for smells first, then suggest a refactoring plan.
```

## Design Principles

This skill follows four strict rules:

1. **Small steps only** — one named refactoring at a time.
2. **Preserve behavior** — no intentional behavior changes.
3. **Separate refactoring from feature work** — no new features during the pass.
4. **Name every technique** — each change must reference the refactoring being applied.

## Repository Structure

A minimal version of this skill only needs:

```text
code-refactoring/
├── SKILL.md
└── README.md
```

Larger versions can add optional references or examples:

```text
code-refactoring/
├── SKILL.md
├── README.md
├── references/
│   ├── code-smells.md
│   └── fowler-refactorings.md
└── examples/
    └── long-function-before-after.md
```

Keep `SKILL.md` focused on the core workflow. Move long examples or reference material into separate files when the skill grows.

## Compatibility

This skill follows the Agent Skills convention: a self-contained folder with a required `SKILL.md` file and optional supporting files such as references, examples, scripts, or assets.

It is suitable for agents and tools that support the Agent Skills format.
