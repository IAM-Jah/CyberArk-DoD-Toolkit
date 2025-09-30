# ATO Control Narratives (Starter Kit)

This folder provides **SSP-ready narratives** aligned to NIST 800-53r5 with CyberArk‑specific implementation language and **evidence checklists**. Use `_template.md` to author additional controls and link artifacts via `mappings/controls-to-artifacts.yaml`.

Suggested workflow:
1. Tailor the narrative to your enclave (NIPR/SIPR) and categorization.
2. Run your automation to export artifacts into `./artifacts/...`.
3. Attach files to eMASS and reference the relative paths in the narrative.
