---
control_id: IA-5
control_name: Authenticator Management
system: CyberArk PAM Self-Hosted – NIPR
assessment_methods: ["Interview","Examine","Test"]
---

## Implementation Narrative
CyberArk **Platforms** enforce password complexity, rotation cadence, and reuse prevention for privileged accounts. **Master Policy** sets global rules (OTP, change-on-use, reconcile on failure). For SSH keys, **PSMP + Platform plugins** rotate and distribute keys with inventory and attribution. Smartcard enforcement for interactive sessions is provided by **PSM CAC/PIV redirect** to ensure token-bound access.

## Assessment Approach
- **Interview:** Platform owners; PKI team for CAC dependencies.
- **Examine:** Platform password/SSH policies; Master Policy export; PSM connection component settings.
- **Test:** Force rotation; verify new credential works; attempt session without CAC and confirm denial.

## Evidence Artifacts
- `artifacts/platforms/password-policy.json`
- `artifacts/platforms/ssh-policy.json`
- `artifacts/screenshots/psm-cac-settings.png`

## Deviations / Compensating Controls
- In environments with strict FIPS cipher lists, validate SCHANNEL and OpenSSL settings per STIG matrix.

## Residual Risk / POA&M
- Moderate for legacy systems that cannot support automated rotation; POA&M references per enclave.
