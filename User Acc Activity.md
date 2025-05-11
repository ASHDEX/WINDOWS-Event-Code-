## 🧑‍💼 **User Account Lifecycle Events**

These events capture every stage of a user account's lifecycle, from creation to deletion and changes.

### **4720 – A user account was created**

- **Indicates**: A new user account was created.
    
- **Key Fields**: Creator account, new account name, domain, privileges assigned.
    
- **Use Case**: Detect unauthorized or unexpected user provisioning.
    

### **4722 – A user account was enabled**

- **Indicates**: A previously disabled account was enabled.
    
- **Use Case**: Track potential reactivation of stale or suspicious accounts.
    

### **4723 – An attempt was made to change an account's password**

- **Indicates**: Self-service password change (user knows old password).
    
- **Use Case**: Monitor for frequent password changes or failed attempts.
    

### **4724 – An attempt was made to reset an account's password**

- **Indicates**: Admin password reset without knowledge of the current password.
    
- **Use Case**: Detect unauthorized account takeovers.
    

### **4725 – A user account was disabled**

- **Use Case**: Account deactivation — useful to track de-provisioning and response to threats.
    

### **4726 – A user account was deleted**

- **Use Case**: Track removal of identities — important for insider threat or forensics.
    

---

## 👥 **Group Management (Global, Local, Universal)**

Group changes impact **access control and privilege management**.

### **4727–4730 – Global Group Events**

- **Creation (4727)**, **Member added (4728)**, **Member removed (4729)**, **Deletion (4730)**.
    
- **Use Case**: Audit access changes for groups used in domain-wide policies.
    

### **4731–4735 – Local Group Events**

- **Creation (4731)**, **Member added (4732)**, **Member removed (4733)**, **Deletion (4734)**, **Modified (4735)**.
    
- **Use Case**: Focus on groups like “Administrators” on local machines; helpful for lateral movement detection.
    

### **4737 – A security-enabled global group was changed**

- **Indicates**: Changes to group attributes (not membership).
    
- **Use Case**: Look for privilege escalations or role modifications.
    

---

## 🔧 **User & Domain Configuration**

### **4738 – A user account was changed**

- **Indicates**: Any user property changed (e.g., login hours, group membership, description).
    
- **Use Case**: General audit trail for account modifications.
    

### **4739 – Domain Policy was changed**

- **Use Case**: Monitor for GPO changes; may indicate mass impact on users or security settings.
    

### **4740 – A user account was locked out**

- **Use Case**: Track brute-force attacks, account abuse, or misconfigured clients.
    

---

## 🖥️ **Computer Account Management**

Computer accounts are critical for **domain trust and authentication**.

|Event ID|Meaning|
|---|---|
|**4741**|A computer account was created|
|**4742**|A computer account was changed|
|**4743**|A computer account was deleted|

- **Use Case**: Ensure that machine identities are legitimate, detect rogue devices.
    

---

## 🚫 **Security-Disabled Groups**

These groups exist for organizational purposes and don’t confer access directly.

|Event ID|Description|
|---|---|
|**4744–4748**|Local Group: Created, Changed, Member added/removed, Deleted|
|**4749–4753**|Global Group: Created, Changed, Member added/removed, Deleted|
|**4759–4763**|Universal Group: Created, Changed, Member added/removed, Deleted|

- **Use Case**: Even though disabled, membership may indicate **intent or shadow admin paths**.
    

---

## 🔄 **Group Type & SID History Events**

### **4764 – A group’s type was changed**

- **Use Case**: Detect elevation from a disabled to a security-enabled group.
    

### **4765 – SID History was added to an account**

- **Use Case**: SID history is used during migrations; can be abused for privilege escalation.
    

### **4766 – Failed attempt to add SID history**

- **Use Case**: May indicate an attempted attack or misconfigured migration tool.
    

### **4767 – A user account was unlocked**

- **Use Case**: After a lockout, this shows recovery. Investigate who unlocked and why.
    

---

## 🛡️ **Administrator Groups & Account Name Changes**

### **4780 – ACL set on admin group members**

- **Use Case**: Detect changes in permissions on accounts in Admin groups (highly critical).
    

### **4781 – The name of an account was changed**

- **Use Case**: Used in account takeover, reassigning stale usernames.
    

---

## 🔑 **Sensitive Password Operations**

### **4782 – Password hash accessed**

- **Use Case**: May indicate password hash extraction (e.g., for offline cracking or pass-the-hash attacks).
    

### **4783–4789 – Basic Application Group Management**

- **Use Case**: These are App-specific groups; changes should be tracked for Shadow IT or rogue app behavior.
    

### **4790–4792 – LDAP Query Group Management**

- **Use Case**: Rarely used; changes could signal automation or delegated access escalation.
    

---

## 🔐 **Password Policy & Directory Services Restore Mode (DSRM)**

|Event ID|Description|
|---|---|
|**4793**|Password Policy Checking API called – custom apps checking passwords.|
|**4794**|Attempt to set DSRM password – DSRM is the **"God-mode"** password for a DC.|
|**4797**|Check for blank password – can indicate enumeration.|

---

## 📋 **Group Membership Enumeration**

|Event ID|Description|
|---|---|
|**4798**|User’s local group membership enumerated|
|**4799**|Security-enabled local group membership enumerated|

- **Use Case**: Often seen during **reconnaissance or automated malware activity**.
    

---

## 🔐 **Credential Manager Operations**

|Event ID|Description|
|---|---|
|**5376**|Credentials backed up|
|**5377**|Credentials restored|

- **Use Case**: Indicates sensitive credential handling; monitor for endpoint credential theft or exfiltration.
    

---

## 📊 **Recommended Use in Security Monitoring**

| Scenario                                 | Correlating Event IDs        |
| ---------------------------------------- | ---------------------------- |
| **User Creation & Privilege Escalation** | 4720, 4728, 4732, 4756       |
| **Brute Force & Account Abuse**          | 4723, 4740, 4767             |
| **Reconnaissance or Enumeration**        | 4798, 4799, 4797             |
| **Insider Threats**                      | 4782, 4738, 4781, 4765       |
| **GPO or Policy Manipulation**           | 4739, 4780                   |
| **Suspicious Admin Actions**             | 4724, 4726, 4722, 4780, 4794 |