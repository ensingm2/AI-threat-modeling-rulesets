# Threat Modeling Terminology | Load: Stage 3

**Scope:** STRIDE, MITRE ATT&CK, Kill Chain, and threat identification concepts

---

## Threat Modeling Concepts

### **Threat Actor**
- **Definition:** An individual or group that poses a security threat to the system
- **Categories:** external attackers, malicious insiders, nation-states, hacktivists, accidental users
- **Characteristics:** Defined by capabilities, motivations, and access levels

### **Mitigation Control**
- **Definition:** A security measure implemented to reduce the likelihood or impact of a threat
- **Types:**
  - **Preventive:** Blocks threat before it occurs (e.g., input validation, encryption)
  - **Detective:** Identifies threat when it occurs (e.g., logging, intrusion detection)
  - **Corrective:** Responds to threat after it occurs (e.g., incident response, backup restoration)
- **Implementation:** Can be technical (encryption, firewalls) or procedural (policies, training)

### **STRIDE**
- **Definition:** Threat categorization framework developed by Microsoft
- **Categories:**
  - **S**poofing: Pretending to be something or someone other than yourself
  - **T**ampering: Modifying data or code
  - **R**epudiation: Claiming you didn't do something or were not responsible
  - **I**nformation Disclosure: Exposing information to unauthorized individuals
  - **D**enial of Service: Denying or degrading service to valid users
  - **E**levation of Privilege: Gaining capabilities without proper authorization

### **MITRE ATT&CK**
- **Definition:** Globally-accessible knowledge base of adversary tactics and techniques based on real-world observations
- **Structure:** Organized into tactics (adversary goals) and techniques (methods to achieve those goals)
- **Usage:** Maps specific threat scenarios to documented attacker behaviors

### **Kill Chain**
- **Definition:** Model describing the stages of a cyber attack from reconnaissance to achieving objectives
- **Stages:** Reconnaissance, Weaponization, Delivery, Exploitation, Installation, Command & Control, Actions on Objectives
- **Usage:** Positions threats within attack progression stages for strategic prioritization

---

**For complete framework details, see:** `threat-modeler/frameworks/quick-reference.md` or `threat-modeler/frameworks/detailed/`

