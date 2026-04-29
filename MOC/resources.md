<!-- Assisted by: Claude Sonnet 4.5 -->
# Resource Management

<rule type="always" severity="high">
- DO add consistent metadata/labels to all created resources (app.kubernetes.io/managed-by, version) for querying, bulk ops, tracking
- DON'T create resources without consistent metadata/labels; cannot query what was created, bulk cleanup impossible
</rule>

<rule type="if-then" condition="verifying resource availability" severity="high">
- IF verifying resource availability, THEN query actual system state not just tracking systems; use max(actual, tracked) to prevent over-allocation
- IF verifying resource availability, DON'T rely solely on tracking systems; reality diverges from tracking causing over-allocation
- IF verifying resource availability, DON'T ignore actual system state for allocation decisions; leads to resource exhaustion
</rule>

<rule type="if-then" condition="configuring system components" severity="medium">
- IF configuring system components that inspect/monitor environments, THEN add tolerations/permissions for those environments
</rule>
