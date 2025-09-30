## Identity Pillar – CyberArk Playbook (Starter)

1) **Centralize Tier-0 credentials** into Safes; enforce OLAC and dual-approval.
2) **OTP + Rotation on Use** for break-glass, domain admins, and service accounts.
3) **Token-bound PSM** (CAC/PIV) for all interactive admin.
4) **Disable direct admin paths**; route through PSM/PSMP.

**Artifacts:** accounts-inventory.csv, master-policy.json, PSM component XML, PTA detections.  
**KPIs:** % Tier-0 under CPM; Avg time to rotate; % CAC-bound sessions; # anomalous session terminations.
