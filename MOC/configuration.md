<!-- Assisted by: Claude Sonnet 4.5 -->
# Configuration

<rule type="always" severity="high">
- DO make config types explicit in content (type/kind field), not inferred from file paths
- DON'T infer config type from file paths (breaks when files move)
</rule>

<rule type="always" severity="high">
- DO read config at call time not import time to enable testing and runtime reconfiguration
- DON'T read config at module import time; makes testing impossible and prevents runtime reconfiguration
- DO allow env var overrides for config (critical for containers/CI)
- DON'T skip env var support for config; breaks containerization and CI/CD
</rule>

<rule type="if-then" condition="tool respects user context" severity="medium">
- IF tool respects user context, THEN use fallback: explicit override > env vars > config files > documented default
- IF tool respects user context, DON'T ignore it forcing arbitrary defaults (e.g., always "default" namespace when user selected different)
</rule>
