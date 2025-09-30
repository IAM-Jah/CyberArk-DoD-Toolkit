---
control_id: AC-2
control_name: Account Management
system: CyberArk PAM Self-Hosted – NIPR
assessment_methods: ["Interview","Examine","Test"]
---

## Implementation Narrative
CyberArk centralizes privileged account lifecycle. Onboarding requires a PVWA request with **dual approval** and produces a Safe with **OLAC** enforcing least-privilege. The **CPM** rotates credentials on schedule and on-use; **OTP** prevents reuse after disclosure. Deprovisioning is API‑driven and removes platform bindings, disables the target account, and archives the Safe per records retention.

## Assessment Approach
- **Interview:** PAM Ops on approvals; Service Owners on ownership tagging.
- **Examine:** Safe ACL export; Master Policy; CPM log excerpts; workflow settings.
- **Test:** Create/approve a request, onboard a lab account, rotate and reconcile; verify PVWA and CPM evidence.

## Evidence Artifacts
- `artifacts/exports/safe-acls-YYYYMMDD.csv`
- `artifacts/policy/master-policy.json`
- `artifacts/logs/cpm/rotation-sample.txt`

## Deviations / Compensating Controls
- If STIG screen‑lock interferes with PSM brokered sessions, enforce **PSM session timeout + PTA dormant-session alert**. See `/compliance/stig-exception-matrix/Windows-PSM.md`.

## Residual Risk / POA&M
- Low; tracked under POA‑2025‑1234 for legacy accounts not yet under CPM.
