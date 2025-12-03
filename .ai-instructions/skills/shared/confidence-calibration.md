# Confidence Calibration | Load: All Stages

**Purpose:** Standardized confidence levels for uncertainty quantification

---

## Quick Reference

| Level | Range | Criteria | Documentation Required |
|-------|-------|----------|------------------------|
| **HIGH** | 85-95% | Direct source documentation, explicit quotes | Source quote + line reference |
| **MEDIUM** | 70-<85% | Reasonable inference, documented assumptions | Inference + alternatives + impact |
| **LOW** | 50-<70% | Industry patterns, significant assumptions | Pattern + alternatives + recommendation |
| **INSUFFICIENT** | <50% | Inadequate data, speculation required | Explicit gap + qualitative approach |

---

## Application Guidelines

### HIGH (85-95%)

**Criteria:** Direct quotes, minimal inference, alternatives excluded  
**Examples:** Explicit component lists, specified technology stacks, documented data flows

**Format:**
```markdown
**Component:** Authentication Service
**Source:** "Authentication is handled by Auth0 OAuth 2.0" (architecture.md, line 123)
**Confidence:** HIGH (95%) - Directly documented
```

### MEDIUM (70-<85%)

**Criteria:** Reasonable inference, alternatives evaluated, multiple sources  
**Examples:** Technology inferred from clues, trust boundaries from interactions

**Format:**
```markdown
**Component:** Backend API
**Source:** "npm packages" mentioned (contributing.md, line 45)
**Inference:** Likely Node.js-based
**Confidence:** MEDIUM (75%)
**Alternatives:** Could be browser-side JavaScript only
**Impact if wrong:** Server-side Node.js vulnerabilities may not apply
```

### LOW (50-<70%)

**Criteria:** Industry patterns, limited system-specific data, multiple alternatives plausible  
**Examples:** Generic threats when implementation unknown, industry statistics

**Format:**
```markdown
**Threat:** SQL Injection vulnerabilities
**Basis:** Industry pattern - web apps commonly use SQL databases
**Source:** No database technology specified
**Confidence:** LOW (60%)
**Alternatives:** May use NoSQL, ORM with parameterized queries
**Recommendation:** Confirm database technology for targeted analysis
```

### INSUFFICIENT (<50%)

**Criteria:** Inadequate data, speculation required, no reasonable inference path  
**Examples:** Completely undocumented architecture, no financial data for quantification

**Format:**
```markdown
**Assessment:** Authentication mechanism security
**Data Gap:** Implementation not documented
**Confidence:** INSUFFICIENT (<50%)
**Qualitative Assessment:** Authentication is critical - requires verification
**Required Information:** Protocol, credential storage, session management, MFA
**Recommendation:** Obtain architecture documentation before detailed analysis
```

---

## Critical Rules

**ALWAYS:**
- ✅ Document confidence level for ALL claims requiring inference
- ✅ Include source references for HIGH confidence
- ✅ Identify alternatives for MEDIUM/LOW confidence
- ✅ Acknowledge data gaps explicitly

**NEVER:**
- ❌ Claim HIGH confidence without direct source quotes
- ❌ Omit confidence levels for inferences
- ❌ Use INSUFFICIENT as excuse to fabricate - use qualitative assessment

---

## Risk Rating Integration

| Confidence | Approach |
|------------|----------|
| HIGH | State rating with justification |
| MEDIUM | State rating with noted uncertainty |
| LOW | Conservative rating with explicit limitations |
| INSUFFICIENT | Note gap; use conservative estimate |

---

## Stage-Specific Requirements

| Stage | HIGH Required For | MEDIUM Acceptable For |
|-------|-------------------|----------------------|
| **1-2** | Component identification, documented flows | Trust boundaries, inferred flows |
| **3** | System-specific threats | Generic technical threats |
| **4** | Quantitative business impact | Qualitative risk categories |
| **5** | Specific control recommendations | Generic control guidance |
| **6** | Overall analysis confidence | Individual limitations |

---

## Anti-Fabrication Controls

**PROHIBITED:**
- ❌ Inventing technical details to justify HIGH confidence
- ❌ Assuming specific technologies for quantitative assessment
- ❌ Fabricating business metrics for financial impact
- ❌ Creating precise numbers when only ranges appropriate

**REQUIRED:**
- ✅ Use lower confidence level appropriate to available data
- ✅ Document data gaps explicitly
- ✅ Provide qualitative assessment when quantitative infeasible
- ✅ Recommend information gathering to improve confidence

---

## Critic Validation

**Critic Must Verify:**
- HIGH confidence claims have specific source documentation
- MEDIUM confidence claims have documented assumptions and alternatives
- LOW confidence items acknowledge limitations
- INSUFFICIENT data gaps explicitly documented

**Challenge:**
- HIGH confidence without adequate source → Should be MEDIUM or LOW
- Quantitative assessments with LOW confidence → Should use qualitative
- Missing uncertainty acknowledgment → Confidence likely too high
