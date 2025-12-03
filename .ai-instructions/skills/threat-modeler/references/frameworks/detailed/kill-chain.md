# Cyber Kill Chain Framework Reference

**Framework:** Lockheed Martin Cyber Kill Chain  
**Purpose:** Map threats to attack progression stages  
**Application:** Stage 3 - Threat Identification

---

## Kill Chain Overview

The **Cyber Kill Chain** is a framework for understanding cyber attack progression through sequential stages from initial reconnaissance through achieving objectives. Originally developed by Lockheed Martin, it provides a strategic view of attack lifecycles.

**Purpose in Threat Modeling:**
- Contextualize threats within attack progression
- Understand where threats fit in multi-stage attack scenarios
- Prioritize based on attack stage criticality
- Design defense-in-depth controls addressing multiple stages

## The Seven Stages

### **1. Reconnaissance**
**Objective:** Research, identify, and select targets  
**Adversary Actions:** Information gathering, target profiling, vulnerability research

**Common Activities:**
- Open-source intelligence (OSINT) gathering
- Social media reconnaissance
- DNS enumeration and subdomain discovery
- Network mapping and port scanning
- Employee identification and role mapping
- Technology stack identification
- Public vulnerability database research

**Threat Examples:**
- Information disclosure through error messages
- Excessive data exposure in public APIs
- Unprotected directory listings
- Email harvesting from public sources
- Metadata leakage in documents
- API endpoint enumeration
- Security misconfiguration discovery

**STRIDE Mapping:** Primarily Information Disclosure

**Detection Opportunities:**
- Monitoring for reconnaissance scanning
- Tracking unusual public API queries
- Detecting automated scraping behavior

**Defensive Focus:**
- Information disclosure minimization
- Error handling without leaking details
- Rate limiting on public endpoints
- OSINT footprint reduction

---

### **2. Weaponization**
**Objective:** Create deliverable malicious payload  
**Adversary Actions:** Develop exploit, package malware, prepare delivery mechanism

**Common Activities:**
- Exploit development or acquisition
- Malware creation or customization
- Payload obfuscation
- Backdoor creation
- Exploit kit preparation
- Phishing email crafting
- Malicious document creation

**Threat Examples:**
- Vulnerabilities that enable exploit development
- Lack of input validation allowing injection attacks
- Client-side vulnerabilities enabling payload execution
- Insufficient file type restrictions

**STRIDE Mapping:** Tampering (exploit creation targeting integrity)

**Detection Opportunities:**
- Threat intelligence on exploit kits
- Malware signature detection
- Behavioral analysis of suspicious files

**Defensive Focus:**
- Vulnerability management and patching
- Secure coding practices
- Input validation frameworks
- Exploit mitigation technologies (DEP, ASLR)

---

### **3. Delivery**
**Objective:** Transmit weapon to target environment  
**Adversary Actions:** Deploy attack vector, deliver payload

**Common Activities:**
- Phishing email delivery
- Watering hole attacks (compromised websites)
- USB drop attacks
- Supply chain compromise
- Malicious attachments or links
- Drive-by downloads
- Social engineering

**Threat Examples:**
- Phishing susceptibility due to weak user awareness
- Lack of email security controls (SPF, DMARC, DKIM)
- Missing attachment scanning
- Insufficient web content filtering
- USB autorun vulnerabilities
- Supply chain security gaps

**STRIDE Mapping:** Spoofing (phishing), Tampering (malicious content)

**Detection Opportunities:**
- Email gateway filtering
- URL reputation checking
- Attachment sandboxing
- User reporting of suspicious content

**Defensive Focus:**
- Email security controls
- Web filtering and proxy
- User security awareness training
- USB port controls
- Supply chain security validation

---

### **4. Exploitation**
**Objective:** Exploit vulnerability to execute code  
**Adversary Actions:** Trigger exploit, execute initial code, leverage vulnerability

**Common Activities:**
- Triggering buffer overflow
- SQL injection execution
- Cross-site scripting (XSS) exploitation
- Authentication bypass
- Command injection
- Deserialization attacks
- Zero-day exploitation

**Threat Examples:**
- Unpatched vulnerabilities
- Injection vulnerabilities (SQL, command, LDAP)
- Authentication and authorization flaws
- Insecure deserialization
- Remote code execution vulnerabilities
- Memory corruption vulnerabilities

**STRIDE Mapping:** Tampering, Elevation of Privilege

**Detection Opportunities:**
- Intrusion detection/prevention systems (IDS/IPS)
- Application security monitoring
- Exploit detection signatures
- Anomalous application behavior

**Defensive Focus:**
- Vulnerability patching
- Input validation and sanitization
- Web application firewalls (WAF)
- Runtime application self-protection (RASP)
- Exploit prevention (DEP, ASLR, CFG)

---

### **5. Installation**
**Objective:** Install persistent backdoor or implant  
**Adversary Actions:** Establish foothold, install malware, create persistence

**Common Activities:**
- Backdoor installation
- Malware persistence mechanisms
- Registry modification (Windows)
- Scheduled task/cron job creation
- Service installation
- Browser extension installation
- Boot/logon autostart creation

**Threat Examples:**
- Insufficient file integrity monitoring
- Missing system baseline controls
- Lack of application whitelisting
- Insufficient privilege separation
- Weak change management controls
- Missing system hardening

**STRIDE Mapping:** Tampering (system modification), Elevation of Privilege

**Detection Opportunities:**
- File integrity monitoring (FIM)
- System baseline deviation detection
- Unusual persistence mechanism creation
- Behavioral analysis of startup items

**Defensive Focus:**
- Application whitelisting
- File integrity monitoring
- System hardening and configuration management
- Least privilege access
- Regular system integrity audits

---

### **6. Command and Control (C2)**
**Objective:** Establish remote control channel  
**Adversary Actions:** Beacon out, establish C2 channel, maintain communication

**Common Activities:**
- HTTP/HTTPS C2 communication
- DNS tunneling
- Custom protocol C2
- Cloud service abuse for C2
- Encrypted C2 channels
- Domain generation algorithms (DGA)
- Fast flux DNS

**Threat Examples:**
- Insufficient egress filtering
- Lack of outbound connection monitoring
- Missing DNS security controls
- Unmonitored cloud service usage
- Insufficient proxy controls
- Missing anomaly detection

**STRIDE Mapping:** Spoofing (C2 impersonation), Information Disclosure (data exfiltration preparation)

**Detection Opportunities:**
- Network traffic analysis
- DNS query monitoring
- Beaconing detection
- Anomalous outbound connections
- Threat intelligence integration

**Defensive Focus:**
- Egress filtering and proxy controls
- DNS security (sinkholing, RPZ)
- Network segmentation
- Encrypted traffic inspection
- Anomaly-based detection

---

### **7. Actions on Objectives**
**Objective:** Achieve attack goals  
**Adversary Actions:** Data exfiltration, destruction, encryption, lateral movement

**Common Activities:**
- Data exfiltration
- Data destruction or encryption (ransomware)
- Lateral movement to additional systems
- Privilege escalation for broader access
- Intellectual property theft
- Financial fraud
- Service disruption
- System defacement

**Threat Examples:**
- Insufficient data loss prevention
- Weak internal segmentation
- Missing privileged access management
- Inadequate backup and recovery
- Insufficient audit logging
- Weak incident detection and response

**STRIDE Mapping:** All categories depending on objective:
- Information Disclosure (data theft)
- Tampering (data destruction/modification)
- Denial of Service (ransomware, disruption)
- Elevation of Privilege (lateral movement)

**Detection Opportunities:**
- Data loss prevention (DLP)
- User and entity behavior analytics (UEBA)
- Abnormal data access patterns
- Large data transfers
- Backup deletion attempts

**Defensive Focus:**
- Data loss prevention controls
- Network segmentation
- Privileged access management
- Backup and recovery procedures
- Incident response capabilities
- Forensics and monitoring

---

## Multi-Stage Attack Progression

### **Understanding Attack Chains:**

Most sophisticated attacks progress through multiple Kill Chain stages:

**Example: Ransomware Attack**
1. **Reconnaissance:** Email address harvesting
2. **Weaponization:** Malicious Office document with macro
3. **Delivery:** Phishing email delivery
4. **Exploitation:** Macro execution enabling PowerShell
5. **Installation:** Ransomware binary installation
6. **Command & Control:** C2 communication for encryption key
7. **Actions on Objectives:** File encryption and ransom demand

### **Breaking the Chain:**

**Defensive Strategy:** Disrupt attack progression at ANY stage

**Early Stage Disruption (More Effective):**
- Reconnaissance → Reduce information disclosure
- Weaponization → Vulnerability management
- Delivery → Email filtering, user training
- Exploitation → Patching, input validation

**Late Stage Disruption (Damage Control):**
- Installation → Application whitelisting, FIM
- C2 → Network monitoring, egress filtering
- Actions → DLP, backups, incident response

---

## Threat-to-Kill Chain Mapping Format

```markdown
### Threat: T-XXX - [Threat Title]
**STRIDE Category:** [S/T/R/I/D/E]
**MITRE ATT&CK:** [T#### - Technique Name]
**Kill Chain Stage:** [Stage(s)]
**Attack Progression Context:** [How threat fits in multi-stage attack]
```

## Example Mappings

### **Example 1: API Enumeration**
```markdown
**Kill Chain Stage:** 1 - Reconnaissance
**Progression Context:** Initial information gathering enabling targeted exploitation in later stages
**Defensive Priority:** Early prevention - reduces attacker knowledge
```

### **Example 2: SQL Injection**
```markdown
**Kill Chain Stage:** 4 - Exploitation
**Progression Context:** Exploits vulnerability to gain unauthorized data access or execute code
**Defensive Priority:** Critical prevention point before installation/persistence
```

### **Example 3: Credential Theft**
```markdown
**Kill Chain Stage:** 4 - Exploitation, 5 - Installation (if persistence established)
**Progression Context:** Enables both immediate unauthorized access and future persistence
**Defensive Priority:** High - enables multiple subsequent attack stages
```

### **Example 4: Data Exfiltration**
```markdown
**Kill Chain Stage:** 7 - Actions on Objectives
**Progression Context:** Final stage achieving attacker's goal after successful compromise
**Defensive Priority:** Last-ditch prevention - earlier stages should have stopped attack
```

## Integration with STRIDE and MITRE ATT&CK

**Three-Framework Integration Pattern:**

```markdown
### Threat: T-015 - Authentication Bypass Enabling Data Exfiltration

**STRIDE Category:** Spoofing, Information Disclosure
**MITRE ATT&CK:**
- **TA0006 - Credential Access:** T1110.004 (Credential Stuffing)
- **TA0009 - Collection:** T1005 (Data from Local System)
**Kill Chain Stages:**
- **Stage 4 (Exploitation):** Bypass authentication controls
- **Stage 7 (Actions on Objectives):** Exfiltrate sensitive data

**Multi-Stage Attack Context:**
This threat represents both the exploitation of weak authentication (Stage 4) and enables the attacker's ultimate objective of data theft (Stage 7). Successful mitigation at Stage 4 prevents progression to Stage 7 data exfiltration.

**Defensive Implications:**
- **Stage 4 Controls:** MFA, rate limiting, account lockout
- **Stage 7 Controls:** DLP, network monitoring, data classification
```

## Kill Chain and Risk Prioritization

### **Early Stage = Higher Priority**

**Rationale:** Breaking the chain early prevents all subsequent stages

**Prioritization Guidance:**
- **Reconnaissance/Delivery threats:** MEDIUM-HIGH priority (early prevention)
- **Exploitation threats:** HIGH-CRITICAL priority (critical decision point)
- **Installation/C2 threats:** HIGH priority (last chance before objectives)
- **Actions on Objectives threats:** CRITICAL priority (immediate business impact)

**Exception:** Some Stage 7 threats (data exfiltration, ransomware) warrant CRITICAL priority due to immediate business impact even though they're late-stage.

### **Defense-in-Depth Mapping**

Map security controls to Kill Chain stages for comprehensive coverage:

| Kill Chain Stage | Defense Layer | Control Examples |
|------------------|---------------|------------------|
| Reconnaissance | Perimeter | Information disclosure prevention, rate limiting |
| Weaponization | Vulnerability Mgmt | Patching, secure SDLC |
| Delivery | Email/Web Security | Email filtering, web proxy, user training |
| Exploitation | Application Security | WAF, input validation, RASP |
| Installation | Endpoint Security | Application whitelisting, FIM, EDR |
| C2 | Network Security | Egress filtering, DNS security, NIDS |
| Actions | Data Security | DLP, segmentation, backups, IR |

## Quality Validation

**Critic Must Verify:**
- Each threat mapped to appropriate Kill Chain stage(s)
- Multi-stage threats identify all relevant stages
- Attack progression context explains how threat enables subsequent stages
- Kill Chain mapping informs risk prioritization rationale
- Integration with STRIDE and ATT&CK is coherent

**Avoid:**
- ❌ Mapping all threats to single stage without justification
- ❌ Ignoring multi-stage attack progression
- ❌ Inconsistent prioritization vs. Kill Chain stage
- ❌ Missing defensive implications per stage
