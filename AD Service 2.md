## **Object Access Events**

### **4661: A handle to an object was requested**

**Scenario:**  
A user tries to open a confidential HR document (`Employee_Salaries.xlsx`). Even if they don’t succeed (maybe access is denied), Windows logs that they _requested a handle_ to the file.

> **Example Log Insight:**  
> User _JohnDoe_ requested access to file `\\server\HR\Employee_Salaries.xlsx` with _Read_ permissions.

---

### **4662: An operation was performed on an object**

**Scenario:**  
A domain admin modifies user account properties (like resetting the password) in Active Directory.  
Windows logs the specific operation performed on the user object.

> **Example Log Insight:**  
> Admin _JaneAdmin_ changed the `PasswordLastSet` attribute for user _bsmith_.

---

## **Active Directory Replication Events**

### **4928: An Active Directory replica source naming context was established**

**Scenario:**  
Two domain controllers (DC1 and DC2) establish replication for the `corp.local` domain after a reboot.

> **Example Log Insight:**  
> DC1 started replicating `corp.local` naming context with DC2.

---

### **4929: An Active Directory replica source naming context was removed**

**Scenario:**  
DC2 is being decommissioned and replication links are removed from DC1.

> **Example Log Insight:**  
> Replication for `corp.local` naming context from DC2 was removed.

---

### **4930: An Active Directory replica source naming context was modified**

**Scenario:**  
An admin changes replication schedule settings for a replication link.

> **Example Log Insight:**  
> Modified replication interval for `corp.local` on DC1.

---

### **4931: An Active Directory replica destination naming context was modified**

**Scenario:**  
Similar to 4930 but at the _destination_ DC side. Maybe replication filters were changed.

> **Example Log Insight:**  
> Destination replication filter updated for `corp.local` on DC2.

---

### **4932: Synchronization of a replica of an Active Directory naming context has begun**

**Scenario:**  
DC1 starts synchronizing changes with DC2 after a network recovery.

> **Example Log Insight:**  
> Synchronization started for `corp.local` between DC1 and DC2.

---

### **4933: Synchronization of a replica of an Active Directory naming context has ended**

**Scenario:**  
Synchronization that started earlier has now completed successfully.

> **Example Log Insight:**  
> Synchronization finished for `corp.local`.

---

### **4934: Attributes of an Active Directory object were replicated**

**Scenario:**  
A user's phone number was updated, and that attribute change is replicated to other DCs.

> **Example Log Insight:**  
> Replicated attribute `telephoneNumber` for user _jsmith_.

---

### **4935: Replication failure begins**

**Scenario:**  
Network outage causes replication between two domain controllers to fail.

> **Example Log Insight:**  
> Replication failure started for `corp.local` between DC1 and DC2.

---

### **4936: Replication failure ends**

**Scenario:**  
Network issue resolved; replication resumes correctly.

> **Example Log Insight:**  
> Replication failure ended for `corp.local`.

---

### **4937: A lingering object was removed from a replica**

**Scenario:**  
An outdated user account that should have been deleted a year ago is finally purged from a domain controller.

> **Example Log Insight:**  
> Lingering object (old user account _tempuser1_) removed from DC2.

---

## **Directory Service Object Events**

### **5136: A directory service object was modified**

**Scenario:**  
An admin changes the department field for user _jane.doe_ in AD.

> **Example Log Insight:**  
> Modified `Department` attribute for user _jane.doe_ to "Finance".

---

### **5137: A directory service object was created**

**Scenario:**  
A new user account `newhire123` is created for onboarding a new employee.

> **Example Log Insight:**  
> Created new user object _newhire123_ in OU=Employees.

---

### **5138: A directory service object was undeleted**

**Scenario:**  
An admin restores a mistakenly deleted service account using Active Directory Recycle Bin.

> **Example Log Insight:**  
> Undeleted object _svc_backupuser_.

---

### **5139: A directory service object was moved**

**Scenario:**  
A user _temp.staff_ is moved from `OU=TemporaryStaff` to `OU=FullTimeEmployees` after promotion.

> **Example Log Insight:**  
> Moved user _temp.staff_ to OU=FullTimeEmployees.

---

### **5141: A directory service object was deleted**

**Scenario:**  
An admin deletes an obsolete group `SalesOldTeam`.

> **Example Log Insight:**  
> Deleted group object _SalesOldTeam_.

---

### **5169: A directory service object was modified**

**Scenario:**  
A background replication service modifies internal attributes related to replication metadata.

> **Example Log Insight:**  
> System modified replication metadata for user _svc-ReplicationAccount_.

---

### **5170: A directory service object was modified during a background cleanup task**

**Scenario:**  
Active Directory performs automated cleanup, modifying tombstoned (deleted) objects during maintenance.

> **Example Log Insight:**  
> Background cleanup modified object _deletedAccount123_.

---

# 📌 Summary

- **4661 and 4662** are common in file/registry access auditing.
    
- **4928–4937** are **replication events**, mainly useful when **troubleshooting AD issues**.
    
- **5136–5170** focus on **Active Directory object lifecycle**: create, move, delete, modify, recover.