# Risk Assessment Terminology | Load: Stage 4

**Scope:** CVSS, confidence levels, and risk assessment concepts

---

## Risk Assessment Concepts

### **CVSS (Common Vulnerability Scoring System)**
- **Definition:** Standardized framework for rating the severity of security vulnerabilities
- **Version:** CVSS v4.0 is the current standard used in threat modeling
- **Components:**
  - **Base Metrics:** Attack Vector (AV), Attack Complexity (AC), Attack Requirements (AT), Privileges Required (PR), User Interaction (UI), Vulnerable System Impact (VC/VI/VA), Subsequent System Impact (SC/SI/SA)
  - **Threat Metrics:** Exploit maturity
  - **Environmental Metrics:** Modified base metrics, security requirements

**Critical Guidance:** CVSS should ONLY be applied when sufficient technical data exists for ALL base metrics. When data is insufficient, use qualitative risk assessment.

### **Confidence Level**
- **Definition:** Degree of certainty in a claim, assessment, or analysis
- **Levels:**
  - **HIGH (85-95%):** Direct source documentation with specific references and validation
  - **MEDIUM (70-<85%):** Reasonable inferences with documented assumptions and alternative interpretations
  - **LOW (50-<70%):** Industry patterns with explicit external source notation and limitations
  - **INSUFFICIENT (<50%):** Inadequate data requiring qualitative assessment with explicit constraints

### **Business Impact**
- **Definition:** The effect of a security incident on business operations, finances, and reputation
- **Categories:** Financial loss, regulatory penalties, operational disruption, reputation damage, legal liability
- **Assessment:** May be qualitative (HIGH/MEDIUM/LOW) or quantitative (dollar amounts) depending on available data

---

**For complete CVSS guidance, see:** Stage 4 guide and confidence-calibration.md

