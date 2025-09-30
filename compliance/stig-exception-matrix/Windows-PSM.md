# Windows PSM – STIG Conflicts & Compensating Controls

| STIG ID | Requirement | Component | Why Conflict | Compensating Control | Validation Steps | Evidence | References |
|---|---|---|---|---|---|---|---|
| V-220881 | Screen lock ≤15 min | PSM Jump Host | Long-running brokered sessions; analysts may switch to ticketing tools | Enforce PSM session policy timeout; PTA dormant-session alert; CAC re-auth on unlock | Idle for 20 min → verify PSM terminates or locks; PTA alert generated | PSM ConnectionComponent XML; PTA policy export | Windows Server STIG; CyberArk PSM Guide |
| V-220971 | NLA mandatory | PSM/RDP | CredSSP + smartcard redirect can conflict with strict NLA enforcement | Brokered auth with TLS/mTLS; verified cipher suite (FIPS) | Confirm SCHANNEL cipher list; test CAC SSO via PSM | `gpresult` export; TLS report | Windows Server STIG; UCAPL |
| V-220803 | Clipboard restriction | PSM/RDP | PSM may need controlled clipboard for copy/paste of commands | Limit clipboard to text; PTA detection for bulk paste | Attempt file clipboard → blocked; text only allowed | Component XML; PTA rule screenshot | Windows Server STIG |
| V-220804 | Device redirection | PSM/RDP | Redirecting drives/printers violates isolation policy | Disable drive/port redirection in PSM component | Verify no drive mapping shown in session | Component XML diff | Windows Server STIG |
| V-36709 | SCHANNEL config (FIPS) | PSM Gateway | Default ciphers not FIPS-aligned | Apply hardened SCHANNEL reg; verify FIPS mode | Run cipher test; check registry keys | `schannel-ciphers.reg`; test output | Windows SSL/TLS Guidance |
