# Development Process

This guide explains the step-by-step process for developing skills.

## Overview

Skill development follows a systematic process from idea to deployment.

## Step 1: Identify Need

Determine if you need a skill:

**Create a skill when:**

- You notice repeating context across conversations
- Domain expertise is needed repeatedly
- Project-specific knowledge should be automatic
- Complex logic benefits from structured patterns

**Do not create a skill when:**

- Task is simple and one-time
- No pattern repetition exists
- Quick fix is sufficient

## Step 2: Define Scope

Define what the skill should do:

1. **Purpose** - One-sentence description
2. **Trigger conditions** - When to activate
3. **Scope** - What's in scope, what's out
4. **Mode** - planning, implementation, or verification

**Example:**
```
Purpose: Execute feature implementation with verification
Triggers: User says "proceed", "continue", "start"
Scope: Implementation only, not planning
Mode: implementation
```

## Step 3: Choose Location

Decide where to create the skill:

**Global skill**:
- Use for: Reusable, domain-agnostic capabilities
- Location: Agent's global skills directory
- Examples: Code review patterns, testing strategies
- Available: Across all projects

**Project skill**:
- Use for: Project-specific functionality
- Location: Project's skills directory
- Examples: Project conventions, specific workflows
- Available: Only for current project

Check your agent's documentation for the exact paths for global vs project skills.

## Step 4: Create Structure

Create the directory structure:

```bash
mkdir -p skill-name/references
```

**Required:**
- `SKILL.md` - Core instructions

**Optional:**
- `references/` - Detailed documentation
- `scripts/` - Executable operations
- `assets/` - Templates, images

## Step 5: Write Frontmatter

Create the YAML frontmatter:

```markdown
---
name: skill-name
description: What this skill does
mode: planning | implementation | verification
---
```

**Keep it lean** (~27 tokens for metadata)

## Step 6: Write Core Instructions

Write SKILL.md with these sections:

1. **When to Use** - Trigger conditions and exclusions
2. **Rules** - Logical statements with When/Then patterns
3. **Process** - Numbered workflow steps
4. **Preconditions** - What must be true first
5. **Postconditions** - What should be true after

**Keep it concise** (<680 tokens for instructions body)

## Step 7: Add Natural Patterns

Use natural English patterns:

**Conditionals:**
- When X happens, do Y
- If X is true, then do Y

**Prohibitions:**
- Never do X
- Block X action

**Requirements:**
- Must do X
- X is required

**Actions:**
- Do X
- Execute X

## Step 7.5: Order Rules by Priority

Rules evaluate top-to-bottom. First matching rule wins.

**Order rules by specificity:**

1. Most specific rules first
2. General rules last
3. Edge cases before common cases

**Example:**
```markdown
## Rules

### Rule: Handle specific case

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute implementation

### Rule: Handle general case

**When:** User says "proceed"

**Then:** Ask what to implement
```

If tasks.md exists, only the specific rule matches. The general rule is never evaluated.

## Step 8: Move Complexity to Level 3

If SKILL.md becomes too long:

1. Move detailed content to `references/`
2. Keep core patterns in SKILL.md
3. Reference detailed docs from SKILL.md

**Example:**
```markdown
See references/detailed-guide.md for complete specification
```

## Step 9: Add Examples

Document common situations:

```markdown
## Common Situations

**Situation:** User says "proceed"

**Pattern:**
- Check: tasks.md exists
- If true: Execute tasks
- If false: Ask what to implement
```

## Step 10: Test Thoroughly

Verify the skill works:

1. Activate the skill
2. Test with various inputs
3. Verify it triggers correctly
4. Check instructions are followed
5. Ensure edge cases are handled

## Step 11: Iterate and Refine

Improve based on testing:

- Adjust trigger conditions if needed
- Clarify ambiguous instructions
- Add missing edge cases
- Simplify complex logic
- Move more details to references/

## Step 12: Document for Others

Add documentation for skill users:

1. **Quick Start** - Get started fast
2. **Writing Guide** - Pattern reference
3. **Examples** - Complete skill examples

## Checklist

Before deploying your skill:

**Structure:**
- [ ] Directory structure created
- [ ] SKILL.md exists with frontmatter
- [ ] references/ directory for details

**Content:**
- [ ] Frontmatter is concise (~27 tokens)
- [ ] Instructions are concise (<680 tokens)
- [ ] When to Use section complete
- [ ] Rules section with clear patterns
- [ ] Process section with numbered steps
- [ ] Preconditions and postconditions defined
- [ ] Common situations documented

**Quality:**
- [ ] No custom syntax
- [ ] No programming keywords
- [ ] Natural English patterns used
- [ ] Clear and direct language
- [ ] Standard markdown formatting

**Testing:**
- [ ] Skill activates correctly
- [ ] Instructions are followed
- [ ] Edge cases handled
- [ ] No unintended behaviors
- [ ] Rule ordering produces expected behavior
- [ ] First matching rule wins as designed

## Common Pitfalls

### Pitfall 1: Wrong Rule Order

**Problem:** General rules come before specific rules, causing specific cases to never match

**Solution:** Order rules by specificity - most specific first, most general last

**Example:**
```markdown
# Wrong:
## Rules
### Rule: General case
**When:** User says "proceed"
**Then:** Ask what to implement

### Rule: Specific case (never matches!)
**When:** User says "proceed" AND tasks.md exists
**Then:** Execute tasks

# Correct:
## Rules
### Rule: Specific case
**When:** User says "proceed" AND tasks.md exists
**Then:** Execute tasks

### Rule: General case
**When:** User says "proceed"
**Then:** Ask what to implement
```

### Pitfall 2: Too Much in SKILL.md

**Problem:** SKILL.md exceeds 680 tokens

**Solution:** Move details to references/ directory

### Pitfall 3: Conversational Prose

**Problem:** Instructions read like conversation

**Solution:** Use direct, imperative statements

### Pitfall 4: Custom Syntax

**Problem:** Using code-like syntax

**Solution:** Use natural English patterns only

### Pitfall 5: Missing Edge Cases

**Problem:** Skill fails on unexpected inputs

**Solution:** Add Common Situations section

### Pitfall 6: No Testing

**Problem:** Skill deployed without verification

**Solution:** Test thoroughly before use

## Example Workflow

Here's a complete example workflow:

**1. Identify Need:**
- Notice: "I keep explaining how to verify code"
- Decision: Create verification skill

**2. Define Scope:**
- Purpose: Verify code meets standards
- Triggers: User requests verification
- Mode: verification

**3. Choose Location:**
- Decision: Global skill (reusable across projects)

**4. Create Structure:**
```bash
mkdir -p ~/.aider-desk/skills/code-verification/references
```

**5. Write SKILL.md:**
- Add frontmatter
- Write When to Use section
- Define Rules
- Create Process steps
- Add Preconditions/Postconditions

**6. Test:**
- Activate skill
- Request verification
- Verify behavior matches expectations

**7. Refine:**
- Adjust trigger conditions
- Add missing patterns
- Move details to references/

**8. Document:**
- Add quick-start guide
- Create examples

## Next Steps

- Read [quick-start.md](quick-start.md) for first-time skill creation
- Study [skill-examples.md](skill-examples.md) for complete examples
- Review [writing-guide.md](writing-guide.md) for pattern reference

## Summary

1. Identify need and define scope
2. Choose location and create structure
3. Write frontmatter and core instructions
4. Use natural English patterns
5. Move complexity to Level 3
6. Add examples and edge cases
7. Test thoroughly
8. Iterate and refine
9. Document for others

Follow this process to create effective skills that leverage natural English patterns LLMs understand.
