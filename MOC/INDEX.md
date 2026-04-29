<!-- Assisted by: Claude Sonnet 4.5 -->
# MOC Guidelines Index

## By Concern
- `validation.md` - Input validation, user input sanitization
- `configuration.md` - Config loading, env vars, user context
- `code-quality.md` - Constants, code reuse, imports, data structures, cleanup
- `testing.md` - Test coverage, CI/CD
- `security.md` - Permissions, temp files, format construction, file operations
- `resources.md` - Resource labeling, availability verification, system components
- `errors.md` - Exception handling, CLI error messages, exit codes

## By Severity
- **High**: validation.md, configuration.md (config loading), code-quality.md (code reuse), testing.md, security.md, resources.md, errors.md
- **Medium**: configuration.md (user context), code-quality.md (constants, defaults, consistency)
- **Low**: code-quality.md (imports, data structures, cleanup)

## By Rule Type
- **Always**: All files contain always-apply rules
- **If/Then**: validation.md, configuration.md, security.md, resources.md, errors.md
