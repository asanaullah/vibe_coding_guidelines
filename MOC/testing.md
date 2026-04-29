<!-- Assisted by: Claude Sonnet 4.5 -->
# Testing

<rule type="always" severity="high">
- DO write comprehensive fast independent tests using mocks for external dependencies; focus on security and resource management
- DO test pure functions thoroughly (structure, required fields, value mapping, edge cases)
- DON'T ship with zero/minimal test coverage; untested code breaks on modification
- DON'T skip testing security/resource-management code; highest consequence failures
- DON'T write tests requiring full infrastructure; slow tests discourage running them
</rule>

<rule type="always" severity="medium">
- DO use pre-commit hooks and CI for linting, formatting, type checking, tests, security scans
- DON'T skip CI/CD automation; manual enforcement fails, quality degrades
</rule>
