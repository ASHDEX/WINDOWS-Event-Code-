# Expanded Detailed View of Each Windows Event ID

---

## 🔒 Object and Rights Changes

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**4670**|Permissions on an object were changed|- Object Type (e.g., File, Key)  <br>- Old and New DACLs  <br>- SIDs modified|Detects attempts to weaken ACLs on critical objects (files, registry keys, services). For example, adding `Everyone: Full Control` to `C:\Windows\System32\services.exe`.|
|**4703**|A token right was adjusted|- Specific privileges adjusted (e.g., SeDebugPrivilege)  <br>- Process and user info|Malicious tools often enable **SeDebugPrivilege** to inject into or dump other processes (like `lsass.exe`).|
|**4704**|A user right was assigned|- Assigned rights (e.g., SeRemoteInteractiveLogonRight)  <br>- Target user/group|Attackers add logon rights (e.g., RDP) to unauthorized users.|
|**4705**|A user right was removed|- Removed rights from user/group|Legitimate but if sudden rights removal occurs after compromise, it may attempt to hide a backdoor account.|
|**4715**|The audit policy (SACL) on an object was changed|- Object name and SACLs (Audit rules)|Attackers disable SACLs to hide object access attempts (turn off file auditing).|
|**4817**|Auditing settings on object were changed|- Detailed breakdown of auditing flags changed|Slightly more granular view than 4715; often seen together.|
|**4907**|Auditing settings on object changed|- Focused on SACL updates too|Similar purpose but can also reflect more system-level changes.|
|**4911**|Resource attributes changed|- DAC-related attributes modified (like confidentiality labels)|Only in environments using Dynamic Access Control (rare).|

---

## 🌐 Domain and Trust Relationships

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**4706**|New trust created to domain|- Trust type (External, Forest, Shortcut)  <br>- Trusting/trusted domains|Dangerous: Attackers might add trust to rogue domains to pivot across environments.|
|**4707**|Trust to domain was removed|- Name of trust/domain removed|Could indicate an attacker cleaning tracks or disrupting network communications.|
|**4716**|Trusted domain info modified|- Updates to domain trust properties (trust direction, encryption)|Can weaken a trust relationship (e.g., disable secure channels).|
|**4865–4867**|Trusted forest information entries added/removed/modified|- Cross-forest trust changes (e.g., added foreign users/groups)|Critical for enterprise environments. Unauthorized forest trust manipulation can lead to massive security breaches.|

---

## 🛡️ Security and Audit Policy Changes

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**4713**|Kerberos policy changed|- Changes in ticket lifetimes, renewable periods|Attackers could lower security (e.g., TGT lifetime = very long).|
|**4714**|Encrypted Data Recovery Policy changed|- Which recovery agents are added/removed|Attackers could insert their certificate to decrypt encrypted user data (EFS attack).|
|**4719**|**System audit policy changed**|- Success/failure audit settings (sub-categories like logon, object access)|Turning off auditing to go "silent" is very common post-compromise.|
|**4819**|Central Access Policies changed|- New CAP settings applied|Not common unless using DAC. Attackers may tamper to alter resource access policies.|
|**4912**|Per-user audit policy changed|- Per-user specific audit config altered|Bypass standard audit settings by focusing on users instead of computers.|
|**4913**|Central Access Policy on object changed|- Object’s Central Access Policy was replaced/altered|Can allow unauthorized access to critical resources under DAC.|
|**4902**|Per-user audit policy table created|- New user-audit policy deployed|Initial creation when a new user receives a non-standard auditing policy.|
|**4908**|Special Groups Logon table modified|- "Special Groups" membership updated|If a new group is added, logons of those group members will be tracked (good for catching privileged account usage).|

---

## 🌐 Firewall and Filtering Platform (WFP) Events

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**4944–4945**|Firewall rules and policies listed at startup|- Baseline snapshot for firewall inspection|Important for incident response—know what rules were active at boot.|
|**4946**|Firewall rule added|- Rule details (ports, programs, direction)|Attackers often add inbound RDP rules!|
|**4947**|Firewall rule modified|- Changed rule info|Tamper legitimate rules to allow C2 (Command & Control) channels.|
|**4948**|Firewall rule deleted|- Deleted rule name and program/path|Remove protection against malware or lateral movement.|
|**4949**|Firewall reset to default|- No rules, very loose security|Hard to detect manually unless monitored.|
|**4950**|Firewall setting changed|- Changed global settings like logging behavior|Disable logging = hide malicious flows.|
|**4954**|GPO firewall settings changed|- Updated from AD Group Policy Objects|Misconfigurations here could open entire networks accidentally.|
|**4956**|Active profile changed (e.g., Public vs. Private)|- Profile change info|Changing to "Public" or "Domain" affects firewall rule enforcement.|
|**4957–4958**|Rules failed to apply|- Rules ignored due to config errors|Critical rules missing = security gaps.|

---

## 🔐 Cryptographic and Certificate Events

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**5063–5070**|Crypto provider/context/function operations attempted/modified|- Which function (e.g., Encrypt, Decrypt, CreateKey)  <br>- Success or failure status|Rare, but attacks against certificate stores, keys (DPAPI abuse, credential theft) generate these events. Advanced persistent threats (APT) often touch these areas.|

---

## 🔒 IPsec/PAStore (Policy Store) Engine Events

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**4709–4712**|IPsec service started/disabled/failure detected|- Audit if network encryption is active|IPsec protects traffic—disablement = traffic plaintext exposure.|
|**5456–5474**|IPsec policies applied/failed (GPO, Local, Cached)|- Which policies were successfully applied or failed|Failure to enforce security policies exposes network to sniffing or MITM attacks.|
|**5462**|Failure to apply some rules of active IPsec policy|- Missing rules information|Half-applied IPsec policies open serious security gaps!|
|**5466–5468**|Changes detected in Active Directory IPsec policies|- Found changes or fallback to cached|Indicates potential AD or network outage—or malicious attack on Group Policies.|

---

## 🌍 Filtering Platform Base Filtering Engine (BFE) Startup

|**Event ID**|**Description**|**Details**|**Why It Matters**|
|---|---|---|---|
|**5440–5444**|Lists of callouts/filters/providers/sublayers at BFE start|- Filter type (Permit/Block)  <br>- Context and application info|Ensures packet filtering engine started with expected filters. Rootkits might attempt to disable/replace filters.|
|**5446–5450**|Callout/filter/provider/sublayer changed dynamically|- New vs. Old configuration|Malware can insert packet inspection code to snoop or manipulate traffic without user noticing.|

---

## ⚙️ Miscellaneous Core Security Events

| **Event ID**  | **Description**                              | **Details**                                     | **Why It Matters**                                                                                   |
| ------------- | -------------------------------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **4904–4905** | Register or unregister security event source | - Source name and process ID                    | Attackers may add or remove custom log providers to hide actions.                                    |
| **4906**      | CrashOnAuditFail changed                     | - Now 1 or 0 (enabled/disabled)                 | Disabling CrashOnAuditFail allows systems to continue without enforcing audit policy = stealth mode. |
| **4826**      | Boot Configuration Data loaded               | - BCD settings like boot debug enabled/disabled | Detects boot-time tampering (e.g., enabling test signing, disabling integrity checks).               |
| **6144–6145** | Security GPO applied / errors applying       | - GPO names and error descriptions              | If GPOs can't apply, security baselines might be missing.                                            |
![[Pasted image 20250514002046.png]]