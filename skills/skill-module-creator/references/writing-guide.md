# Writing Guide

This guide explains how to write effective skills using natural English patterns.

## Core Principles

### Principle 1: Natural Patterns Only

Use patterns LLMs recognize from training data. No custom syntax.

**Good:**
```
When X happens, do Y
If X is true, then do Y
Never do X
Must do X
```

**Bad:**
```
IF X THEN Y
FORBID X
REQUIRE X
```

### Principle 2: Be Explicit and Direct

One logical statement per line. Clear and unambiguous.

**Good:**
```
When user says "proceed", start implementation
If verification fails, fix and retry
Never mark complete without evidence
```

**Bad:**
```
When the user indicates they want to proceed with the task, you should start the implementation phase
```

### Principle 3: Use Standard Markdown Structure

Headers, lists, bold, code blocks are recognized patterns.

**Good:**
```markdown
## Section Name
- Item 1
- Item 2

**Important:** This is critical
```

### Principle 4: Organize with Sections

Use standard sections for consistency:

- When to Use
- Rules
- Process
- Preconditions
- Postconditions
- Common Situations

## Section Writing Guide

### When to Use

Define when to activate the skill and when not to.

**Pattern:**
```markdown
## When to Use

Use this skill when:

- Condition 1
- Condition 2

Do not use when:

- Condition 3
- Condition 4
```

**Tips:**
- Be specific about trigger conditions
- List clear exclusion criteria
- Use bullet points for readability

### Rules

Express logical statements using natural conditionals.

**Pattern:**
```markdown
## Rules

### Rule: Rule Name

**When:** [condition]
**Then:** [action]

**If:** [alternative condition]
**Then:** [alternative action]

**Never:** [forbidden action]
```

**Tips:**
- Use "When/Then" for trigger-response
- Use "If/Then" for conditionals
- Use "Never" for prohibitions
- Include examples if helpful
- **Order rules by specificity** - Specific rules before general ones
- **First match wins** - Rules stop at first matching condition

### Process

Define workflow with numbered steps.

**Pattern:**
```markdown
## Process

1. Step 1
2. Step 2
3. Step 3

**Between step 2 and 3:**

- If [condition], do [action]
- If [other condition], do [other action]
```

**Tips:**
- Keep steps atomic and clear
- Use conditional logic between steps
- Number steps for clarity

### Preconditions

Define what must be true before using the skill.

**Pattern:**
```markdown
## Preconditions

Before using this skill, verify:

- Condition 1
- Condition 2

If any precondition fails:

- Do not proceed
- Handle by: [action]
```

### Postconditions

Define what should be true after using the skill.

**Pattern:**
```markdown
## Postconditions

After completing this skill, verify:

- Condition 1
- Condition 2

**Success metrics:**

- Metric 1
- Metric 2
```

### Common Situations

Define patterns for common scenarios.

**Pattern:**
```markdown
## Common Situations

**Situation:** [description]

**Pattern:**
- Check: [condition 1]
- If true: [action 1]
- If false: [action 2]
```

## Pattern Reference

### Conditional Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| When/Then | Trigger-response | When user says "proceed", start implementation |
| If/Then | Conditional logic | If test fails, fix and retry |
| In case of | Exception handling | In case of error, log and continue |
| On | Event-driven | On completion, notify user |

**Rule Priority:** Rules evaluate top-to-bottom. First matching rule wins. Order specific rules before general ones.

### Prohibition Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Never | Absolute prohibition | Never modify without backup |
| Block | Action blocking | Block unauthorized access |
| Forbid | Explicit forbidding | Forbid unsafe operations |
| Not allowed | Permission denial | External edits are not allowed |

### Requirement Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Must | Mandatory action | Must verify before completion |
| Require | Necessary condition | Require user confirmation |
| Mandatory | Critical requirement | Backup is mandatory |
| Required | Needed item | Documentation is required |

### Action Patterns

| Pattern | Use When | Example |
|---------|----------|---------|
| Do | Perform action | Do verification |
| Execute | Run operation | Execute tests |
| Perform | Carry out | Perform analysis |
| Complete | Finish task | Complete implementation |

## Common Mistakes

### Mistake 1: Wrong Rule Order

**Bad:**
```markdown
## Rules

### Rule: General case

**When:** User says "proceed"

**Then:** Ask what to implement

### Rule: Specific case

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks
```

**Good:**
```markdown
## Rules

### Rule: Specific case

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks

### Rule: General case

**When:** User says "proceed"

**Then:** Ask what to implement
```

### Mistake 2: Conversational Prose

**Bad:**
```markdown
First you need to check if there's a PRD, and if there isn't one,
you should create it. After that's done, you can move on to planning.
```

**Good:**
```markdown
1. Check if PRD exists
2. If missing, create PRD
3. Create implementation plan
```

### Mistake 3: Custom Syntax

**Bad:**
```markdown
IF PRD_EXISTS THEN
    CREATE_PLAN
END IF
```

**Good:**
```markdown
If PRD exists, create plan
If PRD missing, ask user to create PRD first
```

### Mistake 4: Too Conversational

**Bad:**
```markdown
As you can see, we should probably do this thing before that thing.
```

**Good:**
```markdown
Do X before Y
```

### Mistake 5: Bloating Instructions

**Bad:**
```markdown
## Rules

[50+ rules here]
```

**Good:**
```markdown
## Rules

[5-10 core rules]

See references/detailed-rules.md for complete specification
```

## Writing Checklist

Before finalizing your skill:

- [ ] Frontmatter is concise (name, description, mode)
- [ ] SKILL.md is under 680 tokens
- [ ] All patterns are natural English
- [ ] No custom syntax or programming keywords
- [ ] Sections follow standard structure
- [ ] Rules use When/Then or If/Then
- [ ] Process is numbered steps
- [ ] Preconditions and postconditions defined
- [ ] Common situations documented
- [ ] Complex details moved to references/

## Examples

See [skill-examples.md](skill-examples.md) for complete skill examples demonstrating these patterns.
