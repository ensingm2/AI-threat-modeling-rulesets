# Confidence Calibration | Load: All Stages

**Purpose:** Standardized confidence levels for uncertainty quantification

---

## Confidence Level Quick Reference

| Level | Range | Criteria | When to Use | Documentation Required |
|-------|-------|----------|-------------|------------------------|
| **HIGH** | 85-95% | Direct source documentation, explicit quotes | Documented facts | Source quote + line reference |
| **MEDIUM** | 70-<85% | Reasonable inference, documented assumptions | Partial documentation | Inference + alternatives + impact |
| **LOW** | 50-<70% | Industry patterns, significant assumptions | Limited documentation | Pattern + alternatives + recommendation |
| **INSUFFICIENT** | <50% | Inadequate data, speculation required | No relevant documentation | Explicit gap + qualitative approach |

---

## Application Guidelines

### **HIGH (85-95%)**
**Criteria:** Direct quotes, minimal inference, alternatives excluded  
**Examples:** Explicit component lists, specified technology stacks, documented data flows  
**Format:** `Component X | Source: "quote" (file, line Y) | HIGH (Z%) - Directly documented`

### **MEDIUM (70-<85%)**
**Criteria:** Reasonable inference, alternatives evaluated, multiple sources  
**Examples:** Technology inferred from clues, trust boundaries from interactions, sensitivity from regulations  
**Format:** `Claim | Source: partial evidence | Inference: logic | MEDIUM (Z%) | Alternatives: X, Y | Impact if wrong: consequence`

### **LOW (50-<70%)**
**Criteria:** Industry patterns, limited system-specific data, multiple alternatives plausible  
**Examples:** Generic threats, business impact estimates, industry statistics  
**Format:** `Claim | Basis: industry pattern | Source: none system-specific | LOW (Z%) | Alternatives: X, Y | Recommendation: obtain data`

### **INSUFFICIENT (<50%)**
**Criteria:** Inadequate data for confident assessment, explicit gap acknowledgment  
**Examples:** Unknown technology details, undocumented business metrics, unspecified architectures  
**Format:** `Claim impossible | Data Gap: X, Y, Z | INSUFFICIENT | Approach: qualitative | Limitation: cannot quantify`

---

## Critical Rules

**ALWAYS:**
- ✅ Document confidence level for ALL claims requiring inference
- ✅ Include source references for HIGH confidence
- ✅ Identify alternatives for MEDIUM/LOW confidence
- ✅ Acknowledge data gaps explicitly

**NEVER:**
- ❌ Claim HIGH confidence without direct source quotes
- ❌ Omit confidence levels for inferences or assumptions
- ❌ Use INSUFFICIENT as excuse to fabricate - use qualitative assessment instead

---

## CVSS and Confidence

**CRITICAL:** CVSS scoring requires HIGH or MEDIUM confidence for ALL base metrics

| Confidence for Metrics | Action |
|------------------------|--------|
| HIGH/MEDIUM for all 8 | ✅ Apply CVSS with documented justification |
| LOW/INSUFFICIENT for any | ❌ Use qualitative risk rating instead |
| Mixed | ❌ Use qualitative (err on side of caution) |

**When in doubt:** Omit CVSS, use qualitative assessment (HIGH/MEDIUM/LOW risk rating)

---

**For detailed examples and edge cases, see:** `confidence-calibration.md` (full version)

