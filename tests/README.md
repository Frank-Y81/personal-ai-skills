# Tests

This directory will contain tests for skills. Currently, only testing guidelines are defined.

## What Should Be Tested

- **Skill behavior**: Does the skill produce the expected type of output for a given input?
- **Decision logic**: Does the skill follow its own decision rules? (e.g., Shopping must allow "DON'T BUY")
- **Output structure**: Does the output contain the required sections/fields defined in the skill?
- **Constraint adherence**: Does the skill respect its stated constraints?

## Testing Principles

- **Test behavior, not wording**: Different agents using the same skill may phrase outputs differently. Tests should verify behavior and structure, not exact wording.
- **Agent-agnostic**: Tests must be designed so that both Claude and Hermes (and future agents) can run the same test cases.
- **No agent-specific assumptions**: Tests should not rely on agent-specific features, tools, or capabilities.

## Workflow

1. **Modify skill** → 2. **Run local tests** → 3. **Verify all pass** → 4. **Commit and push to GitHub**

## Future Plans

- Standardized test case format (input + expected behavior description)
- Automated test runner for different agents
- Regression test suite for each skill version
