

### **Event ID 1100: The event logging service has shut down**

- **Explanation**:  
    Indicates that the Windows Event Log service has stopped. This event occurs when the system is shutting down, restarting, or if the service crashes.
    
- **Significance**:  
    Can be normal (system shutdown or restart) or indicate an unexpected event logging service failure.
    

---

### **Event ID 1101: Audit events have been dropped by the transport**

- **Explanation**:  
    Occurs when the system cannot keep up with audit events being generated, causing the event log transport to drop events.
    
- **Significance**:  
    Indicates potential overload, misconfiguration, performance bottlenecks, or attempts to flood the event log, possibly as part of a security attack (e.g., event log flooding to obscure malicious activities).
    

---

### **Event ID 1102: The audit log was cleared**

- **Explanation**:  
    Indicates someone intentionally cleared the security event log. Usually performed by an administrator or someone with sufficient privileges.
    
- **Significance**:  
    A critical security event. Often considered suspicious, as attackers might attempt to cover their tracks by clearing audit logs.
    

---

### **Event ID 1104: The security log is now full**

- **Explanation**:  
    Occurs when the security log reaches its maximum defined size. This prevents new events from being logged, depending on log retention policies.
    
- **Significance**:  
    Indicates the need to increase log size or adjust audit log settings. Can result in loss of audit information critical for security analysis.
    

---

### **Event ID 1105: Event log automatic backup**

- **Explanation**:  
    Triggered when the security log automatically backs itself up based on configuration settings. Typically occurs when the log file reaches its maximum capacity.
    
- **Significance**:  
    Generally routine, indicating normal operation and rotation of security logs. Important to verify backup procedures to avoid loss of crucial audit data.
    

---

### **Event ID 1108: The event logging service encountered an error**

- **Explanation**:  
    Indicates that the Event Logging service encountered an unexpected error and may not function properly until the issue is resolved.
    
- **Significance**:  
    Indicates a significant system issue. Immediate investigation is necessary as it could signal corruption of logs, configuration errors, or serious system malfunctions.
    

---

### **Recommendations for Monitoring:**

- **Critical Monitoring Events**:
    
    - **Event 1102**: Always investigate promptly.
        
    - **Event 1101**: Examine the reason for event drops (possible malicious flooding or resource issues).
        
    - **Event 1108**: Indicates instability in logging; investigate immediately.
        
- **Routine Events to Monitor**:
    
    - **Event 1100 & 1105**: Typically informational but useful to verify proper system operation and shutdown sequences.