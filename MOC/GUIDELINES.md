# MOC Coding Guidelines

## Validation (Always)
- DO use validation frameworks (Pydantic, marshmallow) at config boundaries to fail fast with clear errors
- DON'T use raw dict.get() with silent defaults for config; fails late with cryptic errors instead of clear boundary validation errors
- DON'T skip validation at data entry points; errors propagate deep causing confusing failures

## Constants (Always)
- DO extract hardcoded strings, magic numbers, version strings to named module constants
- DON'T scatter hardcoded strings/magic numbers/versions throughout code; makes refactoring error-prone

## Configuration Types (Always)
- DO make config types explicit in content (type/kind field), not inferred from file paths
- DON'T infer config type from file paths (breaks when files move)

## Code Reuse (Always)
- DO extract duplicated logic (client init, tool detection, resource generation) into shared utilities
- DON'T duplicate logic with slight variations; bugs fixed in one place won't fix others

## Defaults (Always)
- DO maintain consistent defaults and categorization; same parameter should have same default across codebase unless documented
- DON'T have inconsistent defaults for same parameter across functions; suggests bugs

## Testing (Always)
- DO write comprehensive fast independent tests using mocks for external dependencies; focus on security and resource management
- DO test pure functions thoroughly (structure, required fields, value mapping, edge cases)
- DON'T ship with zero/minimal test coverage; untested code breaks on modification
- DON'T skip testing security/resource-management code; highest consequence failures
- DON'T write tests requiring full infrastructure; slow tests discourage running them

## CI/CD (Always)
- DO use pre-commit hooks and CI for linting, formatting, type checking, tests, security scans
- DON'T skip CI/CD automation; manual enforcement fails, quality degrades

## Permissions (Always)
- DO apply least privilege; role-based access with minimal needed permissions
- DON'T over-permission components; increases blast radius of bugs/compromises

## Resource Labeling (Always)
- DO add consistent metadata/labels to all created resources (app.kubernetes.io/managed-by, version) for querying, bulk ops, tracking
- DON'T create resources without consistent metadata/labels; cannot query what was created, bulk cleanup impossible

## Configuration Loading (Always)
- DO read config at call time not import time to enable testing and runtime reconfiguration
- DON'T read config at module import time; makes testing impossible and prevents runtime reconfiguration
- DO allow env var overrides for config (critical for containers/CI)
- DON'T skip env var support for config; breaks containerization and CI/CD

## Exception Handling (Always)
- DO catch specific exceptions (IOError, PermissionError) not broad Exception/bare except
- DON'T catch broad Exception/bare except in specific operations; masks real errors including KeyboardInterrupt

## Import Conventions (Always)
- DO follow language import conventions (Python: imports at module top unless circular deps or lazy loading)
- DON'T import inside functions unless breaking circular deps or lazy loading; makes dependencies unclear

## Data Structures (Always)
- DO use efficient structures: generators not lists where possible, sets for membership, dicts for lookups
- DON'T use inefficient structures: list comprehensions where generators work, linear search where dict/set lookup works

## Code Cleanup (Always)
- DO remove unused parameters, dead code, commented-out blocks, unreferenced imports
- DON'T leave unused parameters, dead code, commented-out blocks, unreferenced imports

## Behavioral Consistency (Always)
- DO ensure similar operations have consistent behavior (e.g., if one function adds labels, all similar functions should)
- DON'T have inconsistent behavior for similar operations; violates least surprise

## Resource Verification (If/Then)
- IF verifying resource availability, THEN query actual system state not just tracking systems; use max(actual, tracked) to prevent over-allocation
- IF verifying resource availability, DON'T rely solely on tracking systems; reality diverges from tracking causing over-allocation
- IF verifying resource availability, DON'T ignore actual system state for allocation decisions; leads to resource exhaustion

## System Components (If/Then)
- IF configuring system components that inspect/monitor environments, THEN add tolerations/permissions for those environments

## Temporary Files (If/Then)
- IF creating temp files, THEN use tempfile.NamedTemporaryFile() not hardcoded paths like /tmp/file.yaml (prevents race conditions, symlink attacks)
- IF creating temp files, DON'T use hardcoded paths like /tmp/file.yaml; creates race conditions, symlink attacks

## User Input (If/Then)
- IF using user input in identifiers/names/commands, THEN sanitize and validate against target system rules
- IF using user input in identifiers/names/formats, DON'T use it directly without validation; creates SQL/command injection, malformed output

## Structured Formats (If/Then)
- IF constructing JSON/YAML/XML, THEN use structured construction (json.dumps, yaml.safe_dump) not f-strings with user input
- IF constructing JSON/YAML/XML, DON'T build with f-strings/concatenation; user input with special chars breaks format or enables injection

## User Context (If/Then)
- IF tool respects user context, THEN use fallback: explicit override > env vars > config files > documented default
- IF tool respects user context, DON'T ignore it forcing arbitrary defaults (e.g., always "default" namespace when user selected different)

## CLI Tools (If/Then)
- IF building CLI tools, THEN use proper exit codes (sys.exit(1), raise SystemExit(1)); many frameworks ignore return values
- IF building CLI tools, THEN provide clear actionable errors with field names, expected vs actual types
- IF building CLI tools, DON'T ignore exit codes; shell scripts and CI can't detect failures when process exits 0 on error
- IF building CLI tools, DON'T provide generic unhelpful errors like "Error processing config"; need field names, expected vs actual types

## File Operations (If/Then)
- IF writing to files/directories, THEN ensure permissions are set correctly and verify paths exist and are writable before operations
- IF writing to files/directories, DON'T assume permissions are correct; verify output paths exist and are writable
