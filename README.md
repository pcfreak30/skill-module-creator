# Skill Module Creator

Create Agent Skills using natural English patterns that LLMs naturally understand.

## Overview

This project provides a skill for designing and creating Agent Skills. The skill uses natural English patterns (When/Then, If/Then, Never) that LLMs recognize from training data, eliminating the need for custom syntax or interpreters.

## Key Concepts

### Natural English Patterns

Skills use patterns LLMs recognize from documentation, rules, policies, and procedures:

| Pattern | Example | Training Source |
|---------|---------|-----------------|
| Imperative | "Do X", "Require Y" | Documentation, instructions |
| Conditional | "If X, then Y" | Rules, policies, procedures |
| Prohibition | "Never X", "Block Y" | Security policies, warnings |
| Requirement | "Must X", "X is required" | Compliance, regulations |

### Progressive Disclosure

Skills load in 3 levels:

1. **Metadata** (~27 tokens) - YAML frontmatter for triggering
2. **Instructions** (<680 tokens) - SKILL.md body with core patterns
3. **Resources** (unlimited) - references/, scripts/, assets/ loaded on demand

Keep Levels 1 & 2 lean. Move details to Level 3.

### Rule Priority

Rules evaluate top-to-bottom. First matching rule wins.

**Order rules by specificity:**
- Most specific rules first
- General rules last
- Edge cases before common cases

**Example:**
```markdown
## Rules

### Rule: Specific case

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks

### Rule: General case

**When:** User says "proceed"

**Then:** Ask what to implement
```

If tasks.md exists, only the specific rule matches. The general rule is never evaluated.

## Skill Structure

```
skill-name/
├── SKILL.md       # Core instructions + metadata
├── references/    # Detailed docs (loaded as needed)
├── scripts/       # Executable operations
└── assets/        # Templates, images, files
```

### SKILL.md Sections

1. **Frontmatter** - name, description, mode
2. **When to Use** - Trigger conditions and exclusions
3. **Rules** - Logical statements with When/Then patterns
4. **Process** - Numbered workflow steps
5. **Preconditions** - What must be true first
6. **Postconditions** - What should be true after
7. **Common Situations** - Edge cases and patterns

## Installation

This skill is located in the project's `skills/` directory:

```
skills/skill-module-creator/
```

## Usage

Activate the skill when you need to create a new Agent Skill:

```
Activate skill: skill-module-creator
```

Then use the skill to:

1. Identify skill purpose and scope
2. Choose location (global vs project)
3. Create skill directory structure
4. Write SKILL.md with metadata and instructions
5. Add references/ for detailed documentation
6. Verify structure follows guidelines

## Documentation

### Quick Start

See [references/quick-start.md](skills/skill-module-creator/references/quick-start.md) for creating your first skill.

### Writing Guide

See [references/writing-guide.md](skills/skill-module-creator/references/writing-guide.md) for comprehensive patterns and guidelines.

### Examples

See [references/skill-examples.md](skills/skill-module-creator/references/skill-examples.md) for complete skill examples.

### Development Process

See [references/development-process.md](skills/skill-module-creator/references/development-process.md) for step-by-step workflow.

## What Not to Do

### ❌ Custom Syntax

```
❌ IF X THEN Y
❌ FOR item IN list
❌ GOTO label
```

### ❌ Programming Keywords

```
❌ FUNCTION, RETURN, WHILE, BREAK
❌ END IF, END FOR
```

### ❌ Conversational Prose

```
❌ First you need to check if there's a PRD, and if there isn't one,
   you should create it using skill-name.
```

### ✅ Natural Patterns

```
✅ When X happens, do Y
✅ If X is true, then do Y
✅ Never do X
✅ Must do X
```

## Why This Works

LLMs are trained on:

1. **Documentation** with "When to use" sections
2. **Rules and policies** with "If/then" statements
3. **Procedures** with numbered steps
4. **Permissions** with "Can/cannot" lists
5. **Requirements** with "Must/must not" statements

No interpreter needed. The skill file itself is the specification, written in natural patterns LLMs already understand.

## License

See [LICENSE](LICENSE) for details.

## Attribution

Includes modified code from [anthropics/skills](https://github.com/anthropics/skills) [skills/skill-creator/SKILL.md](https://github.com/anthropics/skills/blob/ef740771ac901e03fbca3ce4e1c453a96010f30a/skills/skill-creator/SKILL.md) under [Apache License 2.0](A2-LICENSE).


