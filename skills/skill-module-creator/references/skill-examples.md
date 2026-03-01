# Skill Examples

This document provides complete examples of skills demonstrating the natural English pattern approach.

## Example 1: Simple Implementation Skill

```markdown
---
name: implement-feature
description: Execute feature implementation with verification
mode: implementation
---

# Implement Feature

Execute feature implementation with verification before completion.

## When to Use

Use this skill when:

- User says "proceed", "continue", "start"
- User indicates task continuation
- Implementation plan exists

Do not use when:

- No implementation plan exists
- User asks about requirements
- Planning phase not complete

## Rules

### Rule: Verify before completion

**When:** Marking task complete

**Then:** Require verification evidence

**Never:** Mark complete without evidence

### Rule: Fix before proceeding

**If:** Verification fails

**Then:** Fix issues and re-verify

**Until:** Verification passes

**Note:** Rules are evaluated in order. First matching rule wins.

## Process

1. Read task from implementation plan
2. Check requirements for specifications
3. Implement code changes
4. Run verification tests
5. If tests pass, mark task complete
6. If tests fail, fix and re-verify
7. Repeat until all tasks complete

**Between steps 3 and 4:**

- If writing new code, consider test-driven development
- If fixing bugs, write failing test first

## Preconditions

Before using this skill, verify:

- Requirements document exists
- Implementation plan exists
- User intent is implementation

If any precondition fails:

- Do not implement
- Ask user to complete planning first

## Postconditions

After completing this skill, verify:

- All tasks marked complete
- Verification evidence provided
- Tests pass (0 failures)
- Code ready for review

**Success metrics:**

- All tasks complete with evidence
- Zero verification failures
- Code committed to branch

## Common Situations

**Situation:** User says "proceed" after planning

**Pattern:**
- Check: Implementation plan exists
- If true: Execute all tasks
- If false: Ask what to implement

**Situation:** Verification fails

**Pattern:**
- When: verification_fails
- Then: fix_and_reverify
- Until: verification_passes
```

## Example 2: Planning Skill

```markdown
---
name: plan-work
description: Break down work into actionable tasks
mode: planning
---

# Plan Work

Break down work into actionable tasks with clear specifications.

## When to Use

Use this skill when:

- User provides requirements or feature description
- User asks "how should I do this"
- Starting new feature or project

Do not use when:

- Implementation already started
- User just wants code without planning
- Task is trivial and well-understood

## Rules

### Rule: Require clear requirements

**When:** Starting planning

**Then:** Verify requirements are clear and complete

**If missing:** Ask clarifying questions

### Rule: Create actionable tasks

**When:** Breaking down work

**Then:** Each task must be specific and testable

**Never:** Create vague or oversized tasks

### Rule: Define verification criteria

**When:** Creating tasks

**Then:** Include how to verify completion

**Never:** Leave verification undefined

## Process

1. Gather requirements from user
2. Clarify ambiguous points
3. Identify all affected components
4. Break down into specific tasks
5. Define verification for each task
6. Order tasks by dependencies
7. Create implementation plan document

**Between steps 4 and 5:**

- If task is too large, break it down further
- If task is too small, combine with related tasks

## Preconditions

Before using this skill, verify:

- User has provided initial requirements
- Work scope is understood
- Planning phase is appropriate

If any precondition fails:

- Ask for requirements or clarification
- Confirm planning is needed

## Postconditions

After completing this skill, verify:

- Implementation plan document created
- All tasks are specific and testable
- Verification criteria defined for each task
- Dependencies between tasks identified

**Success metrics:**

- Complete implementation plan exists
- Tasks are actionable and clear
- User approves the plan

## Common Situations

**Situation:** Requirements are unclear

**Pattern:**
- When: requirements_unclear
- Then: ask_clarifying_questions
- Until: requirements_clear

**Situation:** Task is too large

**Pattern:**
- Check: Can complete in one session?
- If false: Break into smaller tasks
- If true: Keep as single task

**Situation:** Too many small tasks

**Pattern:**
- When: tasks_too_fine_grained
- Then: group_related_tasks
- Until: reasonable_task_count
```

## Example 3: Verification Skill

```markdown
---
name: verify-work
description: Verify work meets requirements and quality standards
mode: verification
---

# Verify Work

Verify work meets requirements and quality standards before completion.

## When to Use

Use this skill when:

- User requests verification
- Before marking work complete
- After implementing changes
- During code review

Do not use when:

- Work is not yet complete
- User explicitly skips verification
- Just viewing or reading code

## Rules

### Rule: Verify against requirements

**When:** Verifying work

**Then:** Check against original requirements

**Never:** Assume implementation matches requirements

### Rule: Run automated tests

**If:** Tests exist for the work

**Then:** Run all tests

**If any fail:** Fix failures before proceeding

### Rule: Check code quality

**When:** Verifying implementation

**Then:** Run linter and type checker

**Never:** Accept code with errors or warnings

## Process

1. Identify verification requirements
2. Check implementation against requirements
3. Run automated tests if available
4. Run linter and type checker
5. Manual code review if needed
6. Document verification results
7. Report findings to user

**Between steps 3 and 4:**

- If tests fail, fix and re-run
- If linter fails, fix issues and re-check

## Preconditions

Before using this skill, verify:

- Work is complete and ready for verification
- Requirements are available for comparison
- Testing tools are configured

If any precondition fails:

- Do not verify incomplete work
- Ask user to complete work first

## Postconditions

After completing this skill, verify:

- All verification checks complete
- Results documented
- User informed of findings
- Issues identified and reported

**Success metrics:**

- All verification checks pass
- Zero test failures
- Zero linter errors
- Documentation complete

## Common Situations

**Situation:** Tests fail

**Pattern:**
- When: tests_fail
- Then: identify_failure_cause
- Then: fix_issue
- Then: retest
- Until: tests_pass

**Situation:** Linter errors

**Pattern:**
- Check: Are errors critical?
- If true: Fix before proceeding
- If false: Note and continue

**Situation:** Requirements unclear

**Pattern:**
- When: requirements_ambiguous
- Then: ask_user_for_clarification
- Until: requirements_clear
```

## Example 4: Debugging Skill

```markdown
---
name: debug-issue
description: Diagnose and fix issues systematically
mode: implementation
---

# Debug Issue

Diagnose and fix issues using systematic approach.

## When to Use

Use this skill when:

- User reports a bug or error
- Tests fail unexpectedly
- Behavior does not match expectations
- Performance issues detected

Do not use when:

- No issue to debug
- User just wants new features
- Issue is already resolved

## Rules

### Rule: Reproduce the issue first

**When:** Starting debugging

**Then:** Reproduce the issue reliably

**Never:** Attempt fix without reproduction

### Rule: Identify root cause

**When:** Issue is reproduced

**Then:** Investigate and identify root cause

**If cause unclear:** Add more logging or debugging

### Rule: Fix at root cause

**When:** Root cause identified

**Then:** Fix at the root cause

**Never:** Apply superficial patches

## Process

1. Gather information about the issue
2. Attempt to reproduce the issue
3. Add logging if needed
4. Identify root cause
5. Create fix for root cause
6. Verify fix resolves issue
7. Add test to prevent regression
8. Document the issue and fix

**Between steps 4 and 5:**

- If root cause unclear, gather more data
- If multiple causes, prioritize and address each

## Preconditions

Before using this skill, verify:

- Issue description is available
- Access to relevant code and logs
- Ability to reproduce the issue

If any precondition fails:

- Ask user for more information
- Request access to resources

## Postconditions

After completing this skill, verify:

- Issue is resolved
- Fix does not break existing functionality
- Test added to prevent regression
- Issue documented

**Success metrics:**

- Issue reproduced and fixed
- Zero regressions introduced
- Test coverage improved

## Common Situations

**Situation:** Cannot reproduce issue

**Pattern:**
- When: cannot_reproduce
- Then: gather_more_information
- Ask: Steps to reproduce, environment details
- Until: issue_reproducible

**Situation:** Multiple potential causes

**Pattern:**
- Check: Can test each hypothesis?
- If true: Test systematically
- If false: Add logging to narrow down

**Situation:** Fix breaks other things

**Pattern:**
- When: regressions_found
- Then: identify_affected_areas
- Then: adjust_fix
- Until: no_regressions
```

## Key Patterns Demonstrated

### Rule Priority
Rules evaluate top-to-bottom, first match wins:

```markdown
## Rules

### Rule: Specific case first

**When:** User says "proceed" AND tasks.md exists

**Then:** Execute tasks

### Rule: General case

**When:** User says "proceed"

**Then:** Ask what to implement
```

If tasks.md exists, only the specific rule matches. General rule is never evaluated.

### Conditional Logic
- When/Then patterns for trigger-response
- If/Then patterns for conditionals
- Never patterns for prohibitions

### Structure
- When to Use sections
- Rules with clear conditions
- Process with numbered steps
- Preconditions and postconditions
- Common situations with patterns

### Natural Language
- No custom syntax
- No programming keywords
- Clear and direct statements
- Standard markdown formatting

## Tips for Your Skills

1. **Keep it focused** - One clear purpose per skill
2. **Use natural patterns** - When/Then, If/Then, Never
3. **Be specific** - Clear conditions and actions
4. **Organize well** - Standard sections for consistency
5. **Document edge cases** - Common situations section
6. **Test thoroughly** - Verify skill works as intended

See [writing-guide.md](writing-guide.md) for detailed patterns and guidelines.
