<!-- Assisted by: Claude Sonnet 4.5 -->
# Code Quality

<rule type="always" severity="medium">
- DO extract hardcoded strings, magic numbers, version strings to named module constants
- DON'T scatter hardcoded strings/magic numbers/versions throughout code; makes refactoring error-prone
</rule>

<rule type="always" severity="high">
- DO extract duplicated logic (client init, tool detection, resource generation) into shared utilities
- DON'T duplicate logic with slight variations; bugs fixed in one place won't fix others
</rule>

<rule type="always" severity="medium">
- DO maintain consistent defaults and categorization; same parameter should have same default across codebase unless documented
- DON'T have inconsistent defaults for same parameter across functions; suggests bugs
</rule>

<rule type="always" severity="low">
- DO follow language import conventions (Python: imports at module top unless circular deps or lazy loading)
- DON'T import inside functions unless breaking circular deps or lazy loading; makes dependencies unclear
</rule>

<rule type="always" severity="low">
- DO use efficient structures: generators not lists where possible, sets for membership, dicts for lookups
- DON'T use inefficient structures: list comprehensions where generators work, linear search where dict/set lookup works
</rule>

<rule type="always" severity="low">
- DO remove unused parameters, dead code, commented-out blocks, unreferenced imports
- DON'T leave unused parameters, dead code, commented-out blocks, unreferenced imports
</rule>

<rule type="always" severity="medium">
- DO ensure similar operations have consistent behavior (e.g., if one function adds labels, all similar functions should)
- DON'T have inconsistent behavior for similar operations; violates least surprise
</rule>
