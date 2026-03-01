# Quick Start Guide

This guide walks you through creating your first Agent Skill using the natural English patterns approach.

## What is a Skill?

A skill is a reusable capability that helps an agent perform tasks effectively. Skills use natural English patterns that LLMs already understand from training data.

## Step 1: Choose Location

Decide where to create your skill:

**Global skill** (available across all projects):
- Use for: Reusable, domain-agnostic capabilities
- Location: Agent's global skills directory
- Examples: Code review patterns, testing strategies

**Project skill** (available only for this project):
- Use for: Project-specific functionality
- Location: Project's skills directory
- Examples: Project conventions, specific workflows

Check your agent's documentation for the exact paths for global vs project skills.

## Step 2: Create Directory Structure

```bash
mkdir -p my-skill/references
```

Your skill directory should look like:
```
my-skill/
├── SKILL.md       # Core instructions (required)
├── references/    # Detailed docs (optional)
├── scripts/       # Executable operations (optional)
└── assets/        # Templates, images (optional)
```

## Step 3: Write SKILL.md

Create `SKILL.md` with frontmatter and core instructions:

```markdown
---
name: my-skill
description: What this skill does
mode: planning | implementation | verification
---

# My Skill

One-sentence purpose.

## When to Use

Use this skill when:

- Condition 1
- Condition 2

Do not use when:

- Condition 3
- Condition 4

## Rules

### Rule: Rule Name

**When:** [condition]
**Then:** [action]

## Process

1. Step 1
2. Step 2
3. Step 3
```

### Key Guidelines

1. **Keep metadata lean** (~27 tokens): name, description, mode
2. **Keep instructions concise** (<680 tokens): SKILL.md body
3. **Move details to Level 3**: references/, scripts/, assets/

## Step 4: Use Natural Patterns

Use natural English patterns LLMs recognize:

**Rule Priority:** Rules evaluate top-to-bottom, first match wins. Order specific rules before general ones.

### Conditionals

### Conditionals
```
When X happens, do Y
If X is true, then do Y
```

### Prohibitions
```
Never do X
Block X action
```

### Requirements
```
Must do X
X is required
```

## Step 5: Avoid Common Mistakes

❌ Custom syntax: `IF X THEN Y`
❌ Programming keywords: `FUNCTION, RETURN, WHILE`
❌ Conversational prose: "First you need to check..."

✅ Natural patterns: "When X happens, do Y"
✅ Standard markdown: Headers, lists, bold
✅ Explicit logic: One statement per line

## Step 6: Add References if Needed

If SKILL.md becomes too long or complex, move content to `references/`:

```
references/
├── detailed-guide.md
├── examples.md
└── patterns.md
```

These load on demand, keeping SKILL.md lean.

## Complete Example

Here's a complete skill example:

```markdown
---
name: example-skill
description: Example skill for demonstration
mode: implementation
---

# Example Skill

Demonstrates skill structure and patterns.

## When to Use

Use this skill when:

- User needs example
- Learning skill structure
- Testing skill creation

Do not use when:

- Production work
- Complex tasks
- User requests different skill

## Rules

### Rule: Verify before action

**When:** Taking any action
**Then:** Verify it's safe first

**Never:** Act without verification

### Rule: Log important decisions

**If:** Making a significant decision
**Then:** Log the decision and reasoning

## Process

1. Identify task
2. Verify safety
3. Execute action
4. Log decision
5. Report result

## Preconditions

Before using this skill, verify:

- Task is safe to execute
- User has requested action
- You have necessary permissions

## Postconditions

After completing this skill, verify:

- Action completed successfully
- Decision was logged
- User was informed

**Success metrics:**

- Zero errors
- Complete logging
- User satisfied
```

## Testing Your Skill

1. Activate your skill
2. Test with various inputs
3. Verify it triggers correctly
4. Check instructions are followed
5. Ensure edge cases are handled

## Next Steps

- Read [writing-guide.md](writing-guide.md) for detailed patterns
- Study [skill-examples.md](skill-examples.md) for more examples
- Review [development-process.md](development-process.md) for workflow

## Summary

1. Choose location (global or project)
2. Create directory structure
3. Write SKILL.md with frontmatter and sections
4. Use natural English patterns
5. Keep it concise, move details to references/
6. Test thoroughly

That's it! Your skill is ready to use.
