# MITRE ATT&CK Framework Reference

**Framework:** MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)  
**Purpose:** Map threats to real-world adversary behaviors and techniques  
**Application:** Stage 3 - Threat Identification

---

## MITRE ATT&CK Overview

**MITRE ATT&CK** is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. It provides a common language for describing adversary behaviors across the attack lifecycle.

**Key Concepts:**
- **Tactics:** The "why" - adversary's tactical objective (e.g., initial access, credential access)
- **Techniques:** The "how" - specific methods adversaries use to achieve tactical objectives
- **Sub-techniques:** More specific descriptions of techniques
- **Procedures:** Specific implementations observed in the wild

## Application in Threat Modeling

### **Purpose:**
Map identified STRIDE threats to ATT&CK techniques to:
1. Contextualize threats within real-world attack patterns
2. Leverage documented adversary behaviors and mitigations
3. Communicate threats using industry-standard terminology
4. Reference existing detection and mitigation guidance

### **Mapping Approach:**
For each threat identified in Stage 3, identify the most relevant ATT&CK technique(s) that describe how the threat would be realized by an adversary.

## MITRE ATT&CK Matrices

### **Enterprise ATT&CK**
- Windows, Linux, macOS, Cloud (AWS, Azure, GCP), Network, Containers
- Primary matrix for most corporate systems

### **Mobile ATT&CK**
- Android and iOS
- Use for mobile application threat modeling

### **ICS ATT&CK**
- Industrial Control Systems
- Use for OT/ICS environments

## Core Tactics (Enterprise ATT&CK)

### **TA0001 - Initial Access**
**Objective:** Gain initial foothold in the system

**Common Techniques:**
- **T1190 - Exploit Public-Facing Application:** Vulnerabilities in web servers, APIs, databases
- **T1133 - External Remote Services:** VPN, RDP, SSH vulnerabilities
- **T1566 - Phishing:** Email-based initial access (spear-phishing, attachments, links)
- **T1078 - Valid Accounts:** Using legitimate credentials (stolen, default, weak)
- **T1195 - Supply Chain Compromise:** Third-party software or hardware compromise

**Threat Modeling Application:**
- Map threats targeting external entry points
- Authentication bypass threats
- Phishing and social engineering threats

---

### **TA0002 - Execution**
**Objective:** Run malicious code on victim system

**Common Techniques:**
- **T1059 - Command and Scripting Interpreter:** Shell commands, PowerShell, Python
- **T1203 - Exploitation for Client Execution:** Exploiting software vulnerabilities
- **T1204 - User Execution:** Tricking users into executing malicious code
- **T1569 - System Services:** Abusing system services for execution
- **T1053 - Scheduled Task/Job:** Persistence through scheduled execution

**Threat Modeling Application:**
- Remote code execution vulnerabilities
- Injection attack threats (command injection, code injection)
- Malicious file upload threats

---

### **TA0003 - Persistence**
**Objective:** Maintain foothold across restarts and credential changes

**Common Techniques:**
- **T1098 - Account Manipulation:** Creating backdoor accounts
- **T1136 - Create Account:** Creating new accounts for persistence
- **T1176 - Browser Extensions:** Malicious browser extensions
- **T1053 - Scheduled Task/Job:** Persistent scheduled execution
- **T1543 - Create or Modify System Process:** Service installation

**Threat Modeling Application:**
- Account creation and modification threats
- Unauthorized persistence mechanism installation
- Configuration tampering for persistence

---

### **TA0004 - Privilege Escalation**
**Objective:** Gain higher-level permissions

**Common Techniques:**
- **T1078 - Valid Accounts:** Using stolen privileged credentials
- **T1068 - Exploitation for Privilege Escalation:** Kernel exploits, privilege escalation bugs
- **T1055 - Process Injection:** Injecting into privileged processes
- **T1548 - Abuse Elevation Control Mechanism:** Bypass UAC, sudo abuse
- **T1134 - Access Token Manipulation:** Token impersonation and theft

**Threat Modeling Application:**
- Vertical privilege escalation threats (STRIDE Elevation of Privilege)
- Authorization bypass threats
- Kernel and OS-level exploitation

---

### **TA0005 - Defense Evasion**
**Objective:** Avoid detection and analysis

**Common Techniques:**
- **T1070 - Indicator Removal:** Log deletion, file deletion
- **T1027 - Obfuscated Files or Information:** Code obfuscation, encryption
- **T1222 - File and Directory Permissions Modification:** Hiding files
- **T1562 - Impair Defenses:** Disabling security software
- **T1036 - Masquerading:** Process name spoofing

**Threat Modeling Application:**
- Log tampering threats (STRIDE Repudiation)
- Security control bypass threats
- Monitoring evasion threats

---

### **TA0006 - Credential Access**
**Objective:** Steal credentials and authentication material

**Common Techniques:**
- **T1110 - Brute Force:** Password guessing, credential stuffing
- **T1555 - Credentials from Password Stores:** Browser passwords, keychain theft
- **T1056 - Input Capture:** Keylogging, form grabbing
- **T1552 - Unsecured Credentials:** Credentials in files, source code, config
- **T1558 - Steal or Forge Kerberos Tickets:** Kerberoasting attacks

**Threat Modeling Application:**
- Credential theft threats (STRIDE Spoofing)
- Password storage vulnerabilities
- Session token theft

---

### **TA0007 - Discovery**
**Objective:** Learn about the system and internal network

**Common Techniques:**
- **T1087 - Account Discovery:** Enumerating user accounts
- **T1083 - File and Directory Discovery:** Exploring file systems
- **T1046 - Network Service Discovery:** Port scanning, service enumeration
- **T1057 - Process Discovery:** Enumerating running processes
- **T1518 - Software Discovery:** Identifying installed software

**Threat Modeling Application:**
- Information disclosure threats exposing system structure
- API enumeration threats
- Insufficient access controls enabling reconnaissance

---

### **TA0008 - Lateral Movement**
**Objective:** Move through the environment to reach target assets

**Common Techniques:**
- **T1021 - Remote Services:** RDP, SSH, SMB lateral movement
- **T1080 - Taint Shared Content:** Compromising shared resources
- **T1550 - Use Alternate Authentication Material:** Pass-the-hash, pass-the-ticket
- **T1563 - Remote Service Session Hijacking:** Session takeover
- **T1570 - Lateral Tool Transfer:** Moving tools between systems

**Threat Modeling Application:**
- Trust boundary traversal threats
- Service-to-service authentication weaknesses
- Internal network segmentation bypass

---

### **TA0009 - Collection**
**Objective:** Gather data of interest

**Common Techniques:**
- **T1005 - Data from Local System:** Harvesting local files
- **T1039 - Data from Network Shared Drive:** Accessing network shares
- **T1056 - Input Capture:** Capturing keystrokes and form data
- **T1113 - Screen Capture:** Taking screenshots
- **T1125 - Video Capture:** Accessing cameras

**Threat Modeling Application:**
- Unauthorized data access threats (STRIDE Information Disclosure)
- Excessive data exposure in APIs
- Insecure direct object references (IDOR)

---

### **TA0010 - Exfiltration**
**Objective:** Steal data from the network

**Common Techniques:**
- **T1041 - Exfiltration Over C2 Channel:** Using command-and-control
- **T1048 - Exfiltration Over Alternative Protocol:** DNS exfiltration, ICMP tunneling
- **T1567 - Exfiltration Over Web Service:** Using cloud services for exfiltration
- **T1020 - Automated Exfiltration:** Scripted data theft
- **T1029 - Scheduled Transfer:** Periodic data exfiltration

**Threat Modeling Application:**
- Data exfiltration threats
- Insufficient data loss prevention
- Unmonitored outbound communications

---

### **TA0011 - Command and Control (C2)**
**Objective:** Communicate with compromised systems

**Common Techniques:**
- **T1071 - Application Layer Protocol:** HTTP/HTTPS C2
- **T1568 - Dynamic Resolution:** Domain generation algorithms
- **T1573 - Encrypted Channel:** Encrypted C2 communications
- **T1001 - Data Obfuscation:** Encoding C2 traffic
- **T1105 - Ingress Tool Transfer:** Downloading additional tools

**Threat Modeling Application:**
- Malware communication channels
- Insufficient egress filtering
- Unmonitored outbound connections

---

### **TA0040 - Impact**
**Objective:** Disrupt availability or integrity

**Common Techniques:**
- **T1485 - Data Destruction:** Deleting or corrupting data
- **T1486 - Data Encrypted for Impact:** Ransomware
- **T1491 - Defacement:** Website or application defacement
- **T1498 - Network Denial of Service:** DDoS attacks
- **T1499 - Endpoint Denial of Service:** Resource exhaustion

**Threat Modeling Application:**
- Denial of service threats (STRIDE DoS)
- Data tampering threats (STRIDE Tampering)
- Ransomware and destructive malware threats

---

## Mobile ATT&CK Tactics

### **Mobile-Specific Tactics:**
- **Initial Access:** App store distribution, physical access, supply chain
- **Persistence:** App auto-start, modify system partition
- **Privilege Escalation:** Exploit OS vulnerabilities, root/jailbreak
- **Defense Evasion:** App obfuscation, hide artifacts
- **Credential Access:** Access stored credentials, input capture
- **Discovery:** System network configuration, location tracking
- **Collection:** Audio capture, SMS capture, clipboard data
- **Command and Control:** Commonly used port, web service
- **Exfiltration:** Over C2 channel, over alternative protocol
- **Impact:** Delete device data, generate fraudulent revenue

### **Mobile-Specific Techniques:**
- **T1411 - Device Access:** Lock screen bypass
- **T1408 - Device Orientation:** Detect emulation environments
- **T1430 - Location Tracking:** GPS spoofing and tracking
- **T1475 - Deliver Malicious App via Other Means:** Sideloading
- **T1517 - Access Notifications:** Notification hijacking

---

## Threat-to-ATT&CK Mapping Format

```markdown
### Threat: T-XXX - [Threat Title]
**STRIDE Category:** [S/T/R/I/D/E]
**Description:** [Threat description]
**MITRE ATT&CK Mapping:**
- **Tactic:** [TA#### - Tactic Name]
- **Technique:** [T#### - Technique Name]
- **Sub-technique:** [T####.### - Sub-technique Name] (if applicable)
**ATT&CK Reference:** https://attack.mitre.org/techniques/T####/
```

## Example Mappings

### **Example 1: SQL Injection Threat**
```markdown
**STRIDE:** Tampering, Information Disclosure, Elevation of Privilege
**MITRE ATT&CK:**
- **Tactic:** TA0001 (Initial Access), TA0006 (Credential Access)
- **Technique:** T1190 (Exploit Public-Facing Application)
- **Technique:** T1552.001 (Unsecured Credentials: Credentials In Files)
```

### **Example 2: Credential Stuffing**
```markdown
**STRIDE:** Spoofing
**MITRE ATT&CK:**
- **Tactic:** TA0001 (Initial Access), TA0006 (Credential Access)
- **Technique:** T1110.004 (Brute Force: Credential Stuffing)
- **Technique:** T1078 (Valid Accounts)
```

### **Example 3: Mobile App Reverse Engineering**
```markdown
**STRIDE:** Information Disclosure
**MITRE ATT&CK (Mobile):**
- **Tactic:** TA0028 (Defense Evasion), TA0032 (Collection)
- **Technique:** T1627 (Execution Guardrails)
- **Technique:** T1418 (Application Discovery)
```

## Integration with STRIDE and Kill Chain

**Three-Framework Integration Pattern:**
```markdown
### Threat: T-015 - Authentication Bypass via Session Hijacking

**STRIDE Category:** Spoofing, Elevation of Privilege
**MITRE ATT&CK:**
- **Tactic:** TA0006 (Credential Access)
- **Technique:** T1539 (Steal Web Session Cookie)
- **Reference:** https://attack.mitre.org/techniques/T1539/
**Kill Chain Stage:** Exploitation, Installation

**Description:** [Detailed threat description]
```

## Using ATT&CK for Mitigation Research

**ATT&CK Provides:**
- **Detection Guidance:** How to detect technique usage
- **Mitigation Guidance:** Controls to prevent or limit techniques
- **Real-World Examples:** Documented APT group usage
- **Data Sources:** What telemetry is needed for detection

**Accessing Mitigations:**
Each ATT&CK technique page includes:
- Procedure examples (real attacks)
- Detection strategies
- Mitigation recommendations
- Data sources for monitoring

**Example Usage in Stage 5:**
When developing mitigations, reference ATT&CK technique pages for industry-standard defensive controls and detection methods.

## Quality Validation

**Critic Must Verify:**
- Each threat mapped to at least one ATT&CK technique
- Technique IDs are valid (T#### format)
- Tactics appropriate for mapped techniques
- ATT&CK matrix selection appropriate (Enterprise vs. Mobile vs. ICS)
- Mappings enhance threat understanding rather than just adding labels

**Avoid:**
- ❌ Generic or incorrect technique mappings
- ❌ Mapping all threats to T1190 (Exploit Public-Facing Application)
- ❌ Skipping ATT&CK mapping for documented threats
- ❌ Using outdated or deprecated technique IDs

## Reference Resources

**Official MITRE ATT&CK Resources:**
- Enterprise ATT&CK: https://attack.mitre.org/matrices/enterprise/
- Mobile ATT&CK: https://attack.mitre.org/matrices/mobile/
- ICS ATT&CK: https://attack.mitre.org/matrices/ics/
- ATT&CK Navigator: https://mitre-attack.github.io/attack-navigator/

**Note:** External access requires explicit user approval per project protocols.

---

**REMINDER: When modifying this framework guidance, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

