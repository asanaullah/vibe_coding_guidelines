<!-- Assisted by: Claude Sonnet 4.5 -->
# Security

<rule type="always" severity="high">
- DO apply least privilege; role-based access with minimal needed permissions
- DON'T over-permission components; increases blast radius of bugs/compromises
</rule>

<rule type="if-then" condition="creating temp files" severity="high">
- IF creating temp files, THEN use tempfile.NamedTemporaryFile() not hardcoded paths like /tmp/file.yaml (prevents race conditions, symlink attacks)
- IF creating temp files, DON'T use hardcoded paths like /tmp/file.yaml; creates race conditions, symlink attacks
</rule>

<rule type="if-then" condition="constructing JSON/YAML/XML" severity="high">
- IF constructing JSON/YAML/XML, THEN use structured construction (json.dumps, yaml.safe_dump) not f-strings with user input
- IF constructing JSON/YAML/XML, DON'T build with f-strings/concatenation; user input with special chars breaks format or enables injection
</rule>

<rule type="if-then" condition="writing to files/directories" severity="medium">
- IF writing to files/directories, THEN ensure permissions are set correctly and verify paths exist and are writable before operations
- IF writing to files/directories, DON'T assume permissions are correct; verify output paths exist and are writable
</rule>
