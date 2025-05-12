
## 1 Object-Access & Registry/Handle Events

_Audit sub-category: **Object Access ➜ File/Registry/Kernel Object**_

|Event ID|What It Logs|Why It Matters (Typical Use)|
|---|---|---|
|**4656**|A handle _request_ for any securable object (file, key, pipe, mutex, etc.).|First “intent” event—pairs with 4663 (access) or 4658 (close). Hunt for abnormal `Desired Access` such as `DELETE` or `WRITE_DAC`.|
|**4657**|Registry _value_ modified.|Detect HKLM/Run-key persistence, tampering with security policies.|
|**4658**|Handle _closed_.|Lets you calculate how long an object stayed open. Rarely watched unless for DFIR timeline reconstruction.|
|**4659**|Handle requested **with intent to delete**.|Triggers when `DELETE` is in Desired Access. Good for finding wipers or cleanup scripts.|
|**4660**|Object was _deleted_.|Confirmatory event—tells you deletion actually happened.|
|**4661**|A handle _request_ to a directory service object (AD object).|Part of directory-object auditing; noisy in DCs.|
|**4663**|**Access attempt succeeded** (file, registry, printer, etc.).|Bread-and-butter file auditing. Correlate with 4656/4658.|
|**4664**|Hard-link creation.|Rare in normal use; malware sometimes abuses hard links for privilege escalation.|
|**4665–4668**|COM+ application-client context creation / deletion / init.|Mostly useful on Citrix or COM+-heavy servers; rarely enabled.|
|**4670**|ACL or owner on an object changed.|Detects permission tampering.|
|**4671**|Blocked ordinal access through TBS (Trusted Base Services).|Intel TPM / virtualization; watch for repeated failures.|
|**4690**|A handle was duplicated to another process.|Common in token-theft or LSASS dumping (handle dupe).|
|**4691**|_Indirect_ object access (e.g., Section objects).|Rare; mainly low-level forensics.|

---

## 2 Scheduled-Task Life-Cycle

_Audit sub-category: **Object Access ➜ Task Scheduler**_

| 4698 | **Task created** | Classic persistence indicator. |  
| 4699 | Task deleted | Rapid add-delete cycles can hide malicious jobs. |  
| 4700 | Task enabled | — |  
| 4701 | Task disabled | — |  
| 4702 | Task updated | Look for suspicious XML in the details. |

---

## 3 Central Access Policy & Dynamic-Access-Control

_Audit sub-category: **Detailed File Share**_

| 4818 | Proposed CAP doesn’t match current CAP | Usually noise in test labs; ignore unless you deploy DAC. |

---

## 4 Certificate-Services “PKI Life-Cycle”

_Audit sub-category: **Certification Services**_  
_(These all appear on the CA in the **Security** log.)_

|Range|Quick Purpose|
|---|---|
|**4868–4870**|Denial / approval / revocation of certs|
|**4871–4874**|CRL publication & request attribute changes|
|**4875–4879**|CA shutdown / backup / restore|
|**4880–4886**|CA start-stop, security descriptor change, audit filter change|
|**4887–4889**|Request approved, denied, set to pending|
|**4890–4894**|CA config or property change; key archive/import|
|**4895–4900**|CA template operations & role separation|

> **Why you care:** Rogue certificate issuance, sudden CA config changes, or an attacker disabling a template so they can re-upload a tampered one will all surface here.

---

## 5 Transaction Manager

_Audit sub-category: **Audit Other System Events**_

| 4985 | Transaction state changed | Mainly database or TxF/TxR forensics. Rarely enabled. |

---

## 6 Windows Firewall & Windows Filtering Platform

_Audit sub-category: **Filtering Platform Packet Drop/Connection**_

|Event ID|Meaning|
|---|---|
|**5031**|Firewall _service_ blocked an app from listening.|
|**5148–5153**|DoS detection & packet-level blocks by WFP.|
|**5150–5153**|Packet allowed/blocked due to restrictive rule.|
|**5154–5159**|Listen/Bind/Connect allowed or blocked. Great for spotting reverse shells or unexpected listeners.|
|**5168**|SMB SPN check failed (Kerberos service mis-bind).|

---

## 7 Network-Share Usage

_Audit sub-category: **File Share**_

| 5140 | Share object accessed (every new handle) |  
| 5142 | Share created |  
| 5143 | Share modified |  
| 5144 | Share deleted |  
| 5145 | Access check on share (granular Operation = Read/Write/Delete) |

> **Tip:** Filter 5140/5145 for `\\*\ADMIN$` or `\\*\IPC$` to spot pass-the-hash and lateral-movement tools.

---

## 8 OCSP Responder

| 5120 | OCSP service started |

---

## 9 Windows Filtering Platform (continued)

_See section 6 for most 51xx events._

---

## 10 COM+ Catalog

| 5888 / 5889 | COM+ object modified or deleted (rare; watch only on high-security app servers). |