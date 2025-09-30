
# CyberArk‑DoD‑Toolkit

**Central knowledge store for U.S. Federal and DoD‑specific CyberArk implementation patterns**—optimized for ATO packages, STIG alignment, Zero Trust execution, and day‑2 operations. This repo curates opinionated templates, playbooks, and evidence scaffolding that go beyond vendor docs so federal teams can move faster with higher confidence.

> **Audience:** DoD and U.S. Federal programs deploying CyberArk Self‑Hosted PAM (Vault, PVWA, PSM, CPM), PTA, PSMP, and select SaaS where FedRAMP‑applicable.  
> **Goal:** Provide “80% complete” artifacts that can be tailored to your enclave (NIPR/SIPR) and plugged directly into eMASS/SSP workflows.

---

## Table of Contents
- [What’s Inside](#whats-inside)
  - [Control Mapping (Excel)](#control-mapping-excel)
  - [SSP Control Narratives (ATO Starter Kit)](#ssp-control-narratives-ato-starter-kit)
  - [STIG Conflict & Compensating Controls Matrix](#stig-conflict--compensating-controls-matrix)
  - [DoD Zero Trust Execution Roadmap Crosswalk](#dod-zero-trust-execution-roadmap-crosswalk)
  - [Ansible: STIG‑friendly Builds (PSM & PSMP)](#ansible-stigfriendly-builds-psm--psmp)
  - [Bruno Collections: DoD‑Ready CyberArk APIs](#bruno-collections-dodready-cyberark-apis)
- [Quick Start](#quick-start)
- [Repository Layout](#repository-layout)
- [Evidence & Artifacts](#evidence--artifacts)
- [Contributing](#contributing)
- [Security Notes](#security-notes)
- [Roadmap](#roadmap)
- [License](#license)

---

## What’s Inside

### Control Mapping (Excel)
**File:** `CyberArk-Controls-Mapped-To-US-Federal.xlsx`  
A starter spreadsheet that maps CyberArk capabilities to common U.S. Federal control frameworks (NIST 800‑53, DISA/DoD needs, FedRAMP context). Use it to trace CyberArk features to controls and to plan **evidence collection**.  
**Typical uses**
- Build eMASS control inheritance and “evidence needed” lists.
- Identify which CyberArk features (e.g., OTP, Master Policy, PSM CAC enforcement) satisfy which controls.
- Export rows into your PMO tracker or POA&M planning.

---

### SSP Control Narratives (ATO Starter Kit)
**Path:** `/compliance/ssp-narratives/`  
**What it is:** SSP‑ready narratives with CyberArk‑specific implementation detail, assessment methods, and evidence checklists—written in plain Markdown with YAML front‑matter.

**Highlights**
- `/_template.md` – copy to author new controls.
- `AC-2.md`, `IA-5.md` – complete examples you can tailor.
- `mappings/controls-to-artifacts.yaml` – machine‑readable links from controls → expected artifacts.
- `README.md` – how to integrate with eMASS and your SSP.

**Why it’s useful**
- Replaces blank‑page writing with vetted language: PVWA approval flows, OLAC, CPM rotation/OTP, PSM isolation, PTA detection.
- Standardizes **evidence references** (e.g., `./artifacts/policy/master-policy.json`).

---

### STIG Conflict & Compensating Controls Matrix
**Path:** `/compliance/stig-exception-matrix/`  
**What it is:** A living matrix of **known frictions** between DISA STIGs and operational CyberArk builds (especially PSM). For each conflict we provide a compensating control pattern and what evidence your AO typically expects.

**Highlights**
- `Windows-PSM.md` – populated with common items (screensaver timers, NLA/CredSSP, clipboard, device redirection, SCHANNEL/FIPS).
- `_schema.csv` – contribution schema for new rows (PVWA/IIS, Vault, RHEL PSMP).

**Why it’s useful**
- Turns “we can’t enable that STIG as‑is” into an AO‑friendly **compensating control story** with validation steps and artifacts.

---

### DoD Zero Trust Execution Roadmap Crosswalk
**Path:** `/compliance/zter-crosswalk/`  
**What it is:** A CSV/JSON mapping from ZTER activities to concrete **CyberArk tasks, KPIs, and deliverables** by pillar (Identity, Device, Visibility, Automation/Orchestration, Network).

**Highlights**
- `zter-crosswalk.csv` – ready to import into PMO trackers (tasks, dependencies, owners, cadence, and KPIs).
- `Pillar-Playbooks/*.md` – human‑readable playbooks (e.g., Identity pillar: “CAC‑bound PSM”, “OTP + change‑on‑use”).

**Why it’s useful**
- Converts strategy to action and defines **evidence** up front so you’re never scrambling before an audit.

---

### Ansible: STIG‑friendly Builds (PSM & PSMP)
**Path:** `/ansible/`  
**What it is:** Reproducible infrastructure roles that **meet STIG intent** without breaking CyberArk functions.

**Highlights**
- `roles/psm-windows-stig/` – SCHANNEL hardening, NLA/RDP tuning for smartcard redirect, PSM connection component deployment, audit hooks.
- `roles/psmp-rhel-stig/` – FIPS enablement, hardened `sshd_config` for proxy, auditd rules, SELinux contexts (extend as needed).
- `inventories/example/` – sample inventory and group vars.
- `playbooks/build-psm.yml` / `build-psmp.yml` – quick entrypoints.

**Example**
```bash
ansible-playbook -i ansible/inventories/example/hosts.ini ansible/playbooks/build-psm.yml
ansible-playbook -i ansible/inventories/example/hosts.ini ansible/playbooks/build-psmp.yml
```

**Why it’s useful**
- Gives Infra a starting point that aligns with the **STIG Exception Matrix** so your security conversation is documented and consistent.

---

### Bruno Collections: DoD‑Ready CyberArk APIs
**Path:** `/bruno/DoD/`  
**What it is:** Opinionated Bruno collections/envs to automate CyberArk operations with **DoD context** (Tier, enclave, POA&M ID, ticket #). Great for onboarding, policy reads, evidence exports.

**Highlights**
- `environments/NIPR.bru` – example env (swap for SIPR as needed).
- `collections/PAM-Admin.bru` – logon, create safe with Tier‑aware naming, read Master Policy, rotate accounts, etc.
- `tests/assertions.md` – suggested assertions and evidence export tips.

**Example flow**
1. Import `NIPR.bru` and set secrets.  
2. Run **Logon** → save token.  
3. Run **Get Master Policy** and **Create Safe** → persist responses to `./artifacts/exports/` for ATO evidence.  
4. **Logoff**.

**Why it’s useful**
- Speeds up Day‑0/Day‑1 tasks and creates repeatable **evidence bundles** for auditors.

---

## Quick Start

1. **Clone** the repo:
   ```bash
   git clone https://github.com/<your-org>/CyberArk-DoD-Toolkit.git
   ```

2. **Use a narrative**: copy `/compliance/ssp-narratives/_template.md` and tailor for your control; attach evidence paths that your automation populates under `/artifacts`.

3. **Plan STIG exceptions**: review `/compliance/stig-exception-matrix/Windows-PSM.md` and adapt rows to your enclave; capture the listed evidence.

4. **Execute ZT tasks**: import `zter-crosswalk.csv` into your tracker, assign owners/cadence, and track KPIs.

5. **Build hardened hosts** (optional): run the Ansible playbooks above in a lab; update variables to match your environment.

6. **Automate via APIs**: open Bruno, load `/bruno/DoD/collections/PAM-Admin.bru`, set env secrets, and run your evidence pulls.

---

## Repository Layout
```
.
├─ CyberArk-Controls-Mapped-To-US-Federal.xlsx
├─ compliance/
│  ├─ ssp-narratives/           # SSP-ready control narratives + artifact mappings
│  ├─ stig-exception-matrix/    # STIG conflicts and compensating controls
│  └─ zter-crosswalk/           # ZT tasks → CyberArk actions, KPIs, artifacts
├─ ansible/
│  ├─ roles/psm-windows-stig/   # Hardened Windows PSM role
│  ├─ roles/psmp-rhel-stig/     # Hardened RHEL PSMP role
│  └─ playbooks/                # build-psm.yml / build-psmp.yml
└─ bruno/
   └─ DoD/                      # Bruno environments & collections
```

---

## Evidence & Artifacts
You’ll see references like `./artifacts/...` throughout the templates. Create this folder in your working copy and export evidence there (policy exports, ACL lists, PTA policies, screenshots). These paths are designed to be **pasted directly into eMASS** as attachments with consistent naming (`YYYYMMDD` stamps).

---

## Contributing
PRs welcome. Helpful contributions include:
- New **narratives** or improvements to existing ones (with artifact links).
- Additional **STIG rows** using `_schema.csv`.
- More **ZTER activities** and pillar playbooks.
- Hardened tasks/handlers for the Ansible roles.
- Bruno **tests** that save evidence bundles safely.

Please avoid committing any **secrets** or live tokens. Use redaction where screenshots are required.

---

## Security Notes
- Treat all exports and screenshots as **sensitive**. Sanitize before committing.
- Do not commit real endpoints, keys, or Vault details.  
- Validate compensating controls with your **AO**—the matrix provides patterns, not universal approvals.

---

## Roadmap
- Evidence export scripts (policy/ACL snapshots → timestamped bundles).
- SIEM search packs for Splunk and Sentinel aligned to PTA signals.
- Terraform/IaC starters for PVWA/PSM infra where feasible.

---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Disclaimer

This repository is for informational purposes and does not constitute legal advice. Ensure to consult with compliance and legal professionals for specific guidance. This is an unofficial repository and is not affiliated with CyberArk Software, Ltd.

---