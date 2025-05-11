## ✅ **Account Authentication and Logon/Logoff Events**

### **4624 – An account was successfully logged on**

- Indicates successful logon to Windows.
    
- Logs interactive logon, network logon, batch logon, or service logon.
    
- Helps track user authentication for auditing and identifying suspicious access.
    

### **4625 – An account failed to log on**

- Indicates failed logon attempts.
    
- Logs authentication failures (wrong password, user account locked out, or unauthorized attempts).
    
- Essential for identifying brute-force attacks or compromised credentials.
    

### **4634 – An account was logged off**

- Indicates the termination of a logon session.
    
- Occurs when the session ends gracefully, such as logging off from Windows or session timeout.
    
- Used to track user activity duration.
    

### **4647 – User initiated logoff**

- Indicates explicit logoff triggered by user action.
    
- Logged when a user manually selects "Log off".
    
- Useful to differentiate from system-initiated logoffs (4634).
    

---

## 🔐 **Explicit Credential Usage and Special Privileges**

### **4648 – A logon was attempted using explicit credentials**

- Logged when credentials are explicitly entered (e.g., running a program as another user).
    
- Helps detect unusual credential usage or lateral movement attempts.
    

### **4672 – Special privileges assigned to new logon**

- Indicates a logon with administrator or special privileges (e.g., SeDebugPrivilege).
    
- Often accompanies event 4624.
    
- Crucial for monitoring privileged accounts and potential privilege escalation.
    

### **4675 – SIDs were filtered**

- Logged when Security Identifiers (SIDs) were filtered during authentication.
    
- Useful to audit identity restrictions or SID-based security policies.
    

### **4964 – Special groups assigned to new logon**

- Indicates assignment of special group memberships upon logon.
    
- Useful for tracking group membership assignment and potential privilege escalation scenarios.
    

---

## 🖥️ **Session and Desktop Activity**

### **4778 – A session was reconnected to a Window Station**

- Indicates a previously disconnected Remote Desktop session was reconnected.
    
- Important for auditing remote user activity.
    

### **4779 – A session was disconnected from a Window Station**

- Indicates a Remote Desktop session has been disconnected.
    
- Helps track remote desktop usage and interruptions.
    

### **4800 – The workstation was locked**

- Indicates user explicitly locked the workstation.
    
- Used to track periods of inactivity or user absence.
    

### **4801 – The workstation was unlocked**

- Indicates workstation unlock event.
    
- Important for identifying potential unauthorized access.
    

### **4802 – The screen saver was invoked**

- Logged when screensaver starts.
    
- Useful to monitor inactivity and workstation protection.
    

### **4803 – The screen saver was dismissed**

- Indicates screensaver was ended, typically after authentication.
    
- Helps track user activity resumption.
    

---

## 🔒 **IPsec and IKE Events**

### **4646 – IKE DoS-prevention mode started**

- Indicates IPsec/IKE started denial-of-service (DoS) protection mechanisms.
    
- Security mechanism activated in response to excessive IKE negotiation requests.
    

### **4649 – A replay attack was detected**

- Logged when replay protection identifies duplicated packets (possible attack).
    
- Helps protect against spoofing or replay attacks.
    

### **4650/4651 – IPsec Main Mode security association established**

- Indicates successful creation of IPsec main mode Security Association (SA).
    
- Essential for verifying secure IPsec connections.
    

### **4652/4653 – IPsec Main Mode negotiation failed**

- Indicates IPsec SA failed during Main Mode negotiation.
    
- Useful for troubleshooting IPsec connectivity issues.
    

### **4654 – IPsec Quick Mode negotiation failed**

- Indicates Quick Mode negotiation failure after Main Mode.
    
- Signals potential configuration or compatibility issues between IPsec endpoints.
    

### **4655 – IPsec Main Mode security association ended**

- Indicates termination of IPsec Main Mode SA.
    
- Used for monitoring IPsec connection life cycle.
    

### **4976/4977/4978 – Invalid IPsec negotiation packet received**

- Indicates malformed or unexpected IPsec negotiation packets.
    
- Typically highlights configuration issues or security threats.
    

### **4979/4980/4981/4982 – IPsec Main/Extended Mode security associations established**

- Indicates IPsec Extended Mode (additional authentication, e.g., EAP) negotiations successfully completed.
    
- Vital for verifying secured extended-mode IPsec connections.
    

### **4983/4984 – IPsec Extended Mode negotiation failed**

- Indicates unsuccessful Extended Mode IPsec negotiation.
    
- Helps troubleshoot authentication issues during IPsec setup.
    

### **5451 – IPsec Quick Mode security association established**

- Indicates successful IPsec Quick Mode SA establishment.
    
- Confirms IPsec connection and tunnel security.
    

### **5452 – IPsec Quick Mode security association ended**

- Indicates Quick Mode SA termination.
    
- Monitors active IPsec tunnels lifecycle.
    

### **5453 – IPsec negotiation failed (IKEEXT service not started)**

- Indicates failure in IPsec negotiation due to critical IKEEXT service not running.
    
- Indicates potential system/service misconfiguration.
    

---

## 📶 **Network and Authentication Policy (NPS/RADIUS)**

### **5632 – Authentication to wireless network requested**

- Logged when attempting wireless network authentication.
    
- Monitors wireless network access attempts.
    

### **5633 – Authentication to wired network requested**

- Indicates wired network authentication request (e.g., 802.1X).
    
- Useful in secure wired environments for monitoring access.
    

### **6272 – NPS granted access to user**

- Indicates Network Policy Server approved access (RADIUS authorization success).
    
- Confirms user access per network policies.
    

### **6273 – NPS denied access to user**

- Indicates denial of access via NPS/RADIUS due to policy or authentication issues.
    
- Important for identifying unauthorized access attempts or policy enforcement issues.
    

### **6274 – NPS discarded user request**

- Logged when NPS intentionally discards an invalid or malformed request.
    
- Helps monitor client configuration or network issues.
    

### **6275 – NPS discarded accounting request**

- Indicates discard of invalid accounting (usage logging) data from a client.
    
- Signals client or system configuration issues.
    

### **6276 – NPS quarantined user**

- Indicates user is placed in quarantine (limited network access) due to policy.
    
- Used in network health and security policy enforcement.
    

### **6277 – NPS granted probationary access (health policy partially met)**

- Indicates limited access granted until device compliance is fully verified.
    
- Useful in network access protection scenarios.
    

### **6278 – NPS granted full access (host met health policy)**

- Indicates full access granted upon successful health validation.
    
- Validates endpoint compliance.
    

### **6279 – NPS locked user account due to repeated failures**

- Indicates lockout after multiple failed attempts via NPS authentication.
    
- Vital for security monitoring and account protection.
    

### **6280 – NPS unlocked user account**

- Logged when account is unlocked, restoring network access.
    
- Audits account lockout resolution activities.
    

---

## ⚠️ **Credential Delegation and Claims**

### **4626 – User/device claims information**

- Logged when identity/attribute claims are processed in authentication.
    
- Useful in advanced authentication scenarios, auditing claims-based access.
    

### **4627 – Group membership information**

- Indicates processing of user's group memberships.
    
- Useful to audit and track group membership handling.
    

### **5378 – Requested credentials delegation disallowed by policy**

- Indicates credential delegation attempts blocked by policy.
    
- Helps identify unauthorized or misconfigured delegation attempts.