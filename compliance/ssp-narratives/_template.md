---
control_id: AC-2
control_name: Account Management
system: CyberArk PAM Self-Hosted (Vault, PVWA, PSM, CPM) – NIPR
categorization: MOD/HIGH (adjust as applicable)
related_disa_stigs: ["Windows Server STIG", "IIS STIG", "RHEL STIG (PSMP)"]
assessment_methods: ["Interview", "Examine", "Test"]
inheritance: 
  - type: FedRAMP Shared Control (optional SaaS usage)
  - provider: <Org GRC>
scope_notes: >
  Scope includes Tier-0 accounts, jump hosts (PSM), CPM managed platforms, PTA.
---

# Implementation Narrative
- **People/Process:** Request → Approve → Onboard through PVWA workflow with dual-approval mapped to DoD role catalog.
- **Technology:** Safes + OLAC + Master Policy; CPM rotates on schedule and on-use; OTP enforced for Tier-0.
- **Boundary:** PSM isolates interactive admin; PTA watches for risk (e.g., unusual hour, command anomalies).

# Assessment Approach
- **Interview:** PAM Ops, SOC Tier-2 on workflows.
- **Examine:** Master Policy export; Safe ACL exports; PTA detection configs.
- **Test:** Create a test account, rotate, reconcile, approve PSM session, verify audit artifacts.

# Evidence Artifacts
- `./artifacts/exports/safe-acls-YYYYMMDD.csv`
- `./artifacts/policy/master-policy.json`
- `./artifacts/pta/policies/high-risk.json`
- `./artifacts/screenshots/pvwa-approval.png`

# Deviations / Compensating Controls
- Screensaver/NLA conflicts on PSM jump hosts handled per STIG matrix (link).

# Residual Risk / POA&M Link
- <placeholder>
