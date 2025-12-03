# Threat Modeling Frameworks - Quick Reference | Load: Stage 3 | ~300 tokens

**Purpose:** Essential definitions for STRIDE, MITRE ATT&CK, and Kill Chain  
**Details:** See `detailed/` directory for comprehensive guidance

---

## STRIDE Threat Categories

**Apply ALL six categories to EACH component:**

| Category | Property | Definition | Key Question |
|----------|----------|------------|--------------|
| **S** - Spoofing | Authentication | Impersonating user/device/service | Can attacker impersonate legitimate entity? |
| **T** - Tampering | Integrity | Malicious modification of data/code | Can attacker modify data or system behavior? |
| **R** - Repudiation | Non-repudiation | Denying actions without proof | Can actions be performed without audit trail? |
| **I** - Information Disclosure | Confidentiality | Exposing information to unauthorized parties | Can attacker access confidential data? |
| **D** - Denial of Service | Availability | Denying or degrading service | Can attacker disrupt system availability? |
| **E** - Elevation of Privilege | Authorization | Gaining unauthorized permissions | Can attacker gain elevated access rights? |

**Critical:** Every component must be analyzed for all 6 categories - no skipping.

---

## MITRE ATT&CK Tactics (Core)

**Map threats to adversary techniques:**

1. **Initial Access** (TA0001) - Gain foothold (phishing, exploits, valid accounts)
2. **Execution** (TA0002) - Run malicious code (command execution, scripting)
3. **Persistence** (TA0003) - Maintain access (backdoors, scheduled tasks)
4. **Privilege Escalation** (TA0004) - Gain higher permissions (exploits, misconfigurations)
5. **Defense Evasion** (TA0005) - Avoid detection (obfuscation, log clearing)
6. **Credential Access** (TA0006) - Steal credentials (keylogging, dumping, brute force)
7. **Discovery** (TA0007) - Explore environment (enumeration, account discovery)
8. **Lateral Movement** (TA0008) - Move through network (remote services, internal spearphishing)
9. **Collection** (TA0009) - Gather target data (data staging, screen capture)
10. **Command and Control** (TA0011) - Communicate with compromised systems (C2 channels)
11. **Exfiltration** (TA0010) - Steal data (transfer to C2, cloud storage)
12. **Impact** (TA0040) - Disrupt availability/integrity (data destruction, ransomware)

**Reference:** https://attack.mitre.org/ for specific techniques (T-numbers)

---

## Cyber Kill Chain Stages

**Contextualize threats within attack progression:**

1. **Reconnaissance** - Information gathering (OSINT, scanning, profiling)
2. **Weaponization** - Create malicious payload (exploits, trojans)
3. **Delivery** - Transmit weapon to target (email, web, USB)
4. **Exploitation** - Trigger vulnerability (code execution, auth bypass)
5. **Installation** - Establish persistence (backdoor, malware)
6. **Command & Control** - Remote control channel (C2 communication)
7. **Actions on Objectives** - Achieve goals (data theft, disruption, fraud)

**Purpose:** Understand where threat fits in multi-stage attack scenarios.

---

## Application Workflow

### **For Each Threat:**
1. **STRIDE:** Categorize by which security property is violated
2. **ATT&CK:** Map to relevant tactic(s) and technique(s)
3. **Kill Chain:** Identify which attack stage(s) the threat enables

### **Example Threat Mapping:**
```
Threat: SQL Injection in user input field
├─ STRIDE: Tampering (data), Information Disclosure (database access), Elevation of Privilege (query execution)
├─ ATT&CK: T1190 (Exploit Public-Facing Application)
└─ Kill Chain: Exploitation → Installation (if web shell deployed)
```

---

## Detailed Guidance

**For comprehensive framework documentation:**
- `detailed/stride.md` - Complete STRIDE guidance with examples per category
- `detailed/mitre-attack.md` - Full tactic/technique listings and mapping guidance
- `detailed/kill-chain.md` - Detailed stage descriptions with defensive strategies

**Load detailed files when:**
- Need specific threat examples for a category
- Require technique-level ATT&CK mapping guidance
- Designing defense-in-depth controls across kill chain stages

---

**This quick reference provides essential definitions. Load detailed files only when comprehensive guidance needed.**

