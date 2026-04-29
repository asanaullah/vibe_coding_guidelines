<!-- Assisted by: Claude Sonnet 4.5 -->
# Error Handling

<rule type="always" severity="high">
- DO catch specific exceptions (IOError, PermissionError) not broad Exception/bare except
- DON'T catch broad Exception/bare except in specific operations; masks real errors including KeyboardInterrupt
</rule>

<rule type="if-then" condition="building CLI tools" severity="high">
- IF building CLI tools, THEN use proper exit codes (sys.exit(1), raise SystemExit(1)); many frameworks ignore return values
- IF building CLI tools, THEN provide clear actionable errors with field names, expected vs actual types
- IF building CLI tools, DON'T ignore exit codes; shell scripts and CI can't detect failures when process exits 0 on error
- IF building CLI tools, DON'T provide generic unhelpful errors like "Error processing config"; need field names, expected vs actual types
</rule>
