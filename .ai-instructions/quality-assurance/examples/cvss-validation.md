# CVSS Scoring Validation - Examples | Load: Stage 4 Critic (Optional) | ~500 tokens

---

## ENHANCED EXAMPLES: CVSS SCORING VALIDATION

### **❌ FAILED CRITIC REVIEW (INAPPROPRIATE CVSS USAGE):**

```markdown
# CRITIC REVIEW - Stage 4
**Risk Assessment Quality:** CVSS scoring applied systematically across all threats
**Scoring Justification:** All CVSS components documented with rationale
**APPROVAL DECISION:** CONFIDENT APPROVAL - risk assessment meets standards
```

**Problem:** This critic failed to catch inappropriate CVSS application to non-technical threats.

---

### **✅ PROPER CRITIC REVIEW (CATCHING INAPPROPRIATE CVSS):**

```markdown
# CRITIC REVIEW - Stage 4
**CRITICAL CVSS MISAPPLICATION IDENTIFIED:**

**Threat T035 - Discriminatory Customer Profiling:**
- **Issue**: CVSS 7.5 assigned to business policy threat
- **Problem**: GDPR consent violation is regulatory/business risk, not technical vulnerability
- **No Technical Exploitation**: Profiling occurs through legitimate business logic, not system compromise
- **VIOLATION**: CVSS inappropriate for organizational policy and regulatory compliance threats

**Threat T019 - Inadequate Incident Response Procedures:**
- **Issue**: CVSS 6.2 assigned to operational capability gap
- **Problem**: Missing procedures is organizational risk, not exploitable technical weakness
- **VIOLATION**: CVSS requires technical attack vector - operational gaps need qualitative assessment

**Threat T007 - SQL Injection (Appropriate CVSS):**
- **Validation**: CVSS 9.8 correctly applied to technical vulnerability
- **Technical Data Available**: Attack vector (network), complexity (low), privileges (none), impacts (high) all documented
- **CORRECT USAGE**: Technical exploitation path with sufficient source data

**REQUIRED CORRECTIONS:**
- Remove CVSS scores from T035, T019, and similar business/organizational threats
- Replace with: "Risk Rating: CRITICAL (Regulatory Risk) - CVSS Not Applicable"
- Add explicit business impact justification: regulatory penalties, legal exposure, reputation damage
- Maintain CVSS only for threats with technical exploitation vectors and sufficient data

**DECISION:** TARGETED REVISION REQUIRED - CVSS misapplied to 8 non-technical threats
```

---

### **Critic Success Criteria for CVSS Validation:**
- **Every CVSS score must map to technical vulnerability with documented attack vector**
- **Business/regulatory/operational threats must use qualitative risk categories**
- **Insufficient technical data must trigger qualitative assessment, not speculative CVSS**
- **Mixed threats (technical + business) require dual assessment approach**

---

## CVSS Appropriateness Checklist

**CVSS IS APPROPRIATE when:**
- ✅ Threat involves technical exploitation (SQL injection, XSS, authentication bypass)
- ✅ ALL base metrics can be determined from documentation (AV, AC, PR, UI, S, C, I, A)
- ✅ Attack vector is clearly technical (network, adjacent, local, physical)
- ✅ No assumptions needed to determine metric values

**CVSS IS NOT APPROPRIATE when:**
- ❌ Threat is business process or policy violation
- ❌ Threat is regulatory compliance gap without technical exploit
- ❌ Threat is organizational capability deficiency
- ❌ Technical details insufficient to determine metrics without assumptions
- ❌ Threat is strategic or operational risk

**USE QUALITATIVE ASSESSMENT when:**
- Business process threats: "Risk Rating: HIGH (Business Impact)"
- Regulatory threats: "Risk Rating: CRITICAL (Regulatory Risk)"
- Operational threats: "Risk Rating: MEDIUM (Operational Impact)"
- Insufficient data: "Risk Rating: MEDIUM (Insufficient Data for CVSS)"

---

**This example demonstrates proper CVSS validation. Return to validation-protocol.md for complete validation procedures.**

