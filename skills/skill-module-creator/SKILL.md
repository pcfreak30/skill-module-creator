---
name: skill-module-creator
description: Design and create Agent Skills using natural English patterns. Use when building new skills, planning skill architecture, or writing skill content.
---

# Skill Module Creator

Create effective Agent Skills using natural English patterns that LLMs naturally understand from training data.

## When to Use

Use this skill when:

- You need to create a new Agent Skill
- Planning skill architecture or structure
- Writing skill content or instructions
- Refactoring existing skills for clarity
- Building domain-specific capabilities

Do not use when:

- Simply activating an existing skill
- Running tests or building code
- Making simple file edits without skill creation

## Core Principle

Leverage natural English patterns that LLMs recognize from training data (documentation, rules, policies, procedures). No custom syntax. No interpreter. Just structured patterns.

### Recognized Patterns

LLMs are trained on these natural patterns:

| Pattern | Example | Training Source |
|---------|---------|-----------------|
| Imperative | "Do X", "Require Y" | Documentation, instructions |
| Conditional | "If X, then Y" | Rules, policies, procedures |
| Prohibition | "Never X", "Block Y" | Security policies, warnings |
| Requirement | "Must X", "X is required" | Compliance, regulations |
| State declaration | "In mode X", "State Y" | Documentation, manuals |
| Ordered list | "1. X, 2. Y" | Procedures, tutorials |

## Skill Location

Skills can be created in two locations:

- **Global skills** (`~/.aider-desk/skills/X`) - Available across all projects
- **Project skills** (`PROJECTDIR/.aider-desk/skills/X`) - Available only for the current project

Use project skills when the functionality is specific to a single project or codebase. Use global skills for reusable, domain-agnostic capabilities.

## Progressive Disclosure

Skills load in 3 levels:

1. **Metadata** (~27 tokens) - YAML frontmatter for triggering
2. **Instructions** (<680 tokens) - SKILL.md body with core patterns
3. **Resources** (unlimited) - references/, scripts/, assets/ loaded on demand

**Key**: Keep Levels 1 & 2 lean. Move details to Level 3.

## Skill Structure

### Section 1: Identity

```markdown
---
name: skill-name
description: What this skill does
mode: planning | implementation | verification
---

# Skill Name

One-sentence purpose.
```

**Why:** Frontmatter is standard metadata. Headers are standard document structure.

### Section 2: When to Use

```markdown
## When to Use

Use this skill when:

- [condition 1]
- [condition 2]
- [condition 3]

Do not use when:

- [condition 4]
- [condition 5]
```

**Why:** "When to use" and "Do not use" are natural patterns LLMs recognize.

### Section 3: Rules (Logical Statements)

```markdown
## Rules

### Rule: Rule Name

**When:** [condition]

**Then:** [action]

**Example:**
```
User says: "X"
Agent does: "Y"
```

### Rule: Another Rule

**If:** [condition]

**Then:** [action]

**Never:** [forbidden action]
```

**Why:** "When/Then" and "If/Then" are natural conditional patterns. "Never" is a natural prohibition pattern.

### Rule Priority

**Rule ordering matters.** Rules are evaluated top-to-bottom. First matching rule wins.

**When:** Evaluating rules

**Then:** Check conditions in order, stop at first match

**Never:** Continue evaluating after a match

**Why:** Makes skill behavior predictable and deterministic

**Example:**
```markdown
## Rules

### Rule: Handle specific case first

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute implementation

### Rule: Handle general case

**When:** User says "proceed"

**Then:** Ask what to implement
```

In this example, if tasks.md exists, the specific rule matches first. The general rule is never evaluated.

### Section 4: Mode Definition (if applicable)

```markdown
## Mode: [mode_name]

**In this mode:**

- Can: [action 1], [action 2], [action 3]
- Cannot: [action 4], [action 5]
- Must: [requirement 1], [requirement 2]
- Must not: [prohibition 1], [prohibition 2]

**Transition to:** [next_mode]
**When:** [condition]
```

**Why:** "Can/Cannot" and "Must/Must not" are natural patterns LLMs recognize from documentation about permissions and requirements.

### Section 5: Workflow/Process

```markdown
## Process

1. [Step 1]
2. [Step 2]
3. [Step 3]

**Between step 2 and 3:**

- If [condition], do [action]
- If [other condition], do [other action]
```

**Why:** Numbered lists are natural for procedures. "If/then" between steps is natural for conditional logic.

### Section 6: Preconditions

```markdown
## Preconditions

Before using this skill, verify:

- [condition 1]
- [condition 2]
- [condition 3]

If any precondition fails:

- Do not proceed
- Handle by: [action]
```

**Why:** "Preconditions" and "before/after" are natural patterns from procedure documentation.

### Section 7: Postconditions

```markdown
## Postconditions

After completing this skill, verify:

- [condition 1]
- [condition 2]
- [condition 3]

**Success metrics:**

- [metric 1]
- [metric 2]
```

### Section 8: Common Patterns

```markdown
## Common Situations

**Situation:** [description]

**Pattern:**
- Check: [condition 1]
- If true: [action 1]
- If false: [action 2]

**Situation:** [other description]

**Pattern:**
- When: [condition]
- Then: [action]
```

## Natural Language Patterns to Use

### Conditionals

Use these natural forms:

```
✅ When X happens, do Y
✅ If X is true, then do Y
✅ In case of X, do Y
✅ On X, do Y

❌ IF X THEN Y (too code-like)
```

### Prohibitions

```
✅ Never do X
✅ Block X action
✅ Forbid X
✅ X is not allowed

❌ FORBID X (too formal/code-like)
```

### Requirements

```
✅ Must do X
✅ Require X
✅ X is mandatory
✅ X is required

❌ REQUIRE X (too code-like)
```

### Actions

```
✅ Do X
✅ Execute X
✅ Perform X
✅ Complete X

❌ EXECUTE X (too code-like)
```

## Structural Guidelines

### Guideline 1: Use Headers for Organization

```markdown
## Section Name

Content here.

### Subsection

Sub-content.
```

LLMs recognize headers as structural elements.

### Guideline 2: Use Lists for Multiple Items

```markdown
- Item 1
- Item 2
- Item 3

1. Step 1
2. Step 2
3. Step 3
```

LLMs recognize bullets and numbers as lists.

### Guideline 3: Use Code Blocks for Examples

```markdown
**Example:**
```
User says: "X"
Agent does: "Y"
```
```

LLMs recognize code blocks as examples.

### Guideline 4: Use Bold for Emphasis

```markdown
**Required:** This is critical
**Optional:** This is optional
**Never:** Do not do this
```

LLMs recognize bold text as emphasis.

## What Not to Do

### ❌ Wrong Rule Order

```
❌ General rule before specific rule
❌ Overlapping conditions without clear priority
❌ Rules that can never match due to ordering
```

**Correct:**
```markdown
## Rules

### Rule: Specific case

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks

### Rule: General case

**When:** User says "proceed"

**Then:** Ask what to implement
```

**Wrong:**
```markdown
## Rules

### Rule: General case (WRONG - comes first!)

**When:** User says "proceed"

**Then:** Ask what to implement

### Rule: Specific case (NEVER MATCHES!)

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks
```

### ❌ Custom Syntax

```
❌ SET x = value
❌ FOR item IN list
❌ GOTO label
❌ CALL tool "name"
```

These are not natural English patterns.

### ❌ Nested Structures

```
❌ IF condition THEN
     IF other condition THEN
         action
     END IF
   END IF
```

LLMs don't recognize this naturally from training.

### ❌ Programming Keywords

```
❌ FUNCTION, RETURN, WHILE, BREAK
❌ END IF, END FOR, END WHILE
❌ DECLARE, EXECUTE, INVOKE (as keywords)
```

These are programming language keywords, not natural English.

### ❌ Conversational Prose

```
❌ First you need to check if there's a PRD, and if there isn't one,
   you should create it using skill-name. After that's done, you can
   move on to creating a plan.
```

This is conversational, not logical structure.

## Rules

### Rule: Keep metadata concise

**When:** Creating frontmatter

**Then:** Keep under 27 tokens for name, description, mode

**Why:** Metadata loads first, must be lean

### Rule: Order rules by priority

**When:** Writing rules

**Then:** Most specific rules first, general rules last

**Never:** Put general rules before specific ones

**Why:** First matching rule wins, ordering determines behavior

### Rule: Keep instructions under 680 tokens

**When:** Writing SKILL.md body

**Then:** Keep core instructions under 680 tokens

**Why:** Instructions load second, must remain concise

### Rule: Move details to Level 3 resources

**When:** Content exceeds token limits or becomes complex

**Then:** Move to references/, scripts/, or assets/

**Never:** Bloat Level 1 or 2

### Rule: Use natural patterns only

**When:** Writing skill logic

**Then:** Use natural English patterns from training data

**Never:** Use custom syntax or programming keywords

### Rule: Organize with sections

**When:** Structuring skill content

**Then:** Use standard sections: When to Use, Rules, Process, Preconditions

**Never:** Mix sections or skip required structure

## Process

1. Identify skill purpose and scope
2. Choose location (global vs project)
3. Create skill directory structure
4. Write SKILL.md with metadata and instructions
5. Add references/ for detailed documentation
6. Add scripts/ for executable operations if needed
7. Add assets/ for templates if needed
8. Verify structure follows guidelines

**Between steps 4 and 5:**

- If SKILL.md exceeds 680 tokens, move content to references/
- If logic is complex, break into multiple reference files

## Preconditions

Before using this skill, verify:

- You understand progressive disclosure principle
- You can identify natural English patterns
- You have a clear skill purpose in mind

If any precondition fails:

- Review references/quick-start.md
- Study the complete example in references/skill-examples.md

## Postconditions

After completing this skill, verify:

- Skill directory follows standard structure
- SKILL.md has proper frontmatter and sections
- Instructions are under 680 tokens
- Resources are in Level 3 directories
- No custom syntax or programming keywords used

**Success metrics:**

- Skill loads correctly without errors
- Metadata triggers skill appropriately
- Instructions are clear and concise
- Resources are well-organized

## Common Situations

**Situation:** Creating first skill

**Pattern:**
- Check: references/quick-start.md
- Follow: Step-by-step guide
- Use: Complete example as template

**Situation:** Skill becomes too large

**Pattern:**
- When: SKILL.md exceeds 680 tokens
- Then: Move content to references/
- Until: Instructions fit within limit

**Situation:** Complex conditional logic

**Pattern:**
- Check: Can express as natural patterns?
- If yes: Use "When/Then" or "If/Then"
- If no: Break into simpler rules or create reference doc

## Why This Works

### LLM Training Data Includes:

1. **Documentation** with "When to use" sections
2. **Rules and policies** with "If/then" statements
3. **Procedures** with numbered steps
4. **Permissions** with "Can/cannot" lists
5. **Requirements** with "Must/must not" statements

### LLMs Recognize:

- Headers as structure
- Lists as collections
- Bold as emphasis
- Code blocks as examples
- These patterns from training data

### No Interpreter Needed:

The LLM understands these patterns natively. It doesn't need a "VM" or interpreter. The skill file itself is the specification, written in natural patterns the LLM already knows.

## Key Principles

1. **Use natural English patterns** LLMs recognize from training
2. **Leverage standard markdown structure** (headers, lists, bold)
3. **Avoid custom syntax** (no programming keywords)
4. **Be explicit and direct** (one logical statement per line)
5. **Use conditionals naturally** (When/Then, If/Then)
6. **Organize with sections** (When to use, Rules, Process, Preconditions)
7. **Apply progressive disclosure** (keep levels 1 & 2 lean, details in level 3)

**The skill file IS the logic.** No interpreter. No VM. Just natural patterns LLMs understand.
