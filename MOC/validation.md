<!-- Assisted by: Claude Sonnet 4.5 -->
# Validation

<rule type="always" severity="high">
- DO use validation frameworks (Pydantic, marshmallow) at config boundaries to fail fast with clear errors
- DON'T use raw dict.get() with silent defaults for config; fails late with cryptic errors instead of clear boundary validation errors
- DON'T skip validation at data entry points; errors propagate deep causing confusing failures
</rule>

<rule type="if-then" condition="using user input in identifiers/names/commands" severity="high">
- IF using user input in identifiers/names/commands, THEN sanitize and validate against target system rules
- IF using user input in identifiers/names/formats, DON'T use it directly without validation; creates SQL/command injection, malformed output
</rule>
