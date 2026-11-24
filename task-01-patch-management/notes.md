# ManageEngine Endpoint Central Cloud Lab — Combined Notes

## Lab Environment
* **Console:** ManageEngine Endpoint Central Cloud (`cloud.manageengine.com`)
* **Endpoints & Roles:**
  * Windows Server endpoint (managed endpoint; task spec notes Windows Server 2022, slides show Windows Server 2019)
  * Windows 10 Pro (1) (managed endpoint, hardening & threat simulation target)
  * Windows 10 Pro (2) (managed endpoint)
  * Kali Linux (simulation environment in Task 2)[cite: 1, 2, 3]

---

## Task 1: Patch Management & Endpoint Security Policy
* **Agent Enrollment & Inventory:** Enrolled and approved 3 managed endpoints (Windows Server + two Windows 10 Pro systems) and verified visibility in Inventory.
* **Patch Management:**
  * Identified 21 missing patches and 4 installed patches (~18% patch compliance).
  * Executed a test deployment (`Test_Patch_43006`) to a single test PC with status `Succeeded`.
  * Configured a recurring automated patch deployment policy (`Cersenbe_axsami_Policy`) scheduled for Wednesdays (`02:00–04:00`).
* **Endpoint Security & Inventory:**
  * Configured USB storage blocking (`Block_USB_Storage`) and verified blocked USB activity in Device Control / USB Audit logs.
  * Configured application blocking (`Block_Notepad++` using `notepad++.exe` and file hash) and confirmed blocked access in reports.
  * Reviewed CVSS v3 vulnerabilities (including high/critical items such as `CVE-2026-42990`) and audited installed software across the managed endpoints[cite: 1, 2].

---

## Task 2: Endpoint Threat Detection & CIS Hardening
* **Threat Analytics (EDR):**
  * Simulated reconnaissance and process export activity on Windows 10 (`whoami /all`, `ipconfig /all`, `net user /domain`, and `Get-Process | Export-CSV`).
  * Observed `0` new alerts from those standard administrative commands, noting signature-focused detection and limited behavioral analytics in the trial setup.
* **Endpoint Hardening (CIS Benchmark):**
  * Ran CIS Microsoft Windows 10 Enterprise Benchmark (Level 1), starting at **22%** compliance (`83/372` rules passed, `287` failed).
  * Applied remediation for 5 password policy rules (password history, minimum age, minimum length, complexity, and length relaxation) and re-scanned to **24%** compliance.
* **Browser Security:**
  * Published add-on management policies (`Block_Extensions_Chrome` and `Block_Extensions_Microsoft_Edge`) targeting extension blocking (such as Google Translate) and verified that blocked extensions cannot be installed[cite: 3].

---

## Endpoint Security Summary
* **Current Posture:** Baseline endpoint management, patch scheduling, USB/application/browser controls, and initial CIS Level 1 hardening are active, while high/critical vulnerabilities and unaddressed CIS rules remain.
* **Critical Findings:** Multiple CVSS >= 7 vulnerabilities across endpoints (with deployable patches for many items and manual fixes needed for others such as OpenSSL), low initial CIS Level 1 compliance (`22%` -> `24%`), and limited behavioral detection for built-in/administrative commands in the trial environment.
* **Recommendations:** Prioritize patching CVSS >= 9 vulnerabilities, remediate remaining CIS Level 1 failed rules in priority order, expand USB, application, and browser policies across all relevant endpoints, and evaluate stronger behavioral monitoring/detection where needed[cite: 1, 2, 3].
