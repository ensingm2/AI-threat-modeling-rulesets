# Stage 4: Risk Assessment | Threat Modeler

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 4 work complete. Ready for critic analysis."

---

## ⚠️ CRITICAL: Concise From The Start

**Stage 4 is a WORKING DOCUMENT, not a final report. DO NOT create verbose output then trim - create concise output from the start.**

| ❌ PROHIBITED | ✅ REQUIRED |
|---------------|-------------|
| Executive Summary | Risk assessment table first |
| Methodology sections | 1-2 sentence justifications |
| Multi-paragraph analyses | Qualitative ratings only (C/H/M/L) |
| Verbose impact descriptions | Priority grouping by rating |

**Self-check before saving:**
- [ ] No executive summary or methodology section?
- [ ] Each justification ≤2 sentences?
- [ ] Using qualitative ratings only?
- [ ] No fabricated metrics?

**Stage 6 is where elaboration belongs. Keep Stage 4 lean.**

---

## Stage 4 Purpose

Assess risk for all Stage 3 threats using qualitative ratings. Prioritize threats for mitigation planning.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** `ai-working-docs/01-*.json`, `02-*.json`, `03-threats.json`
- **Fallback:** `01-system-understanding.md`, `02-data-flow-analysis.md`, `03-threat-identification.md`
- Source documentation as needed (for impact/likelihood context)

**Outputs:**
- **AI Working Doc:** `ai-working-docs/04-risk-assessments.json`
- **Human-Readable:** `04-risk-assessment.md`

---

## Risk Rating Framework

Use **qualitative ratings only**: CRITICAL, HIGH, MEDIUM, LOW

| Rating | Criteria |
|--------|----------|
| **CRITICAL** | Immediate business impact; regulatory violations; complete system compromise; data breach affecting all users |
| **HIGH** | Significant impact; major data exposure; service disruption; requires near-term remediation |
| **MEDIUM** | Moderate impact; limited scope; standard remediation timeline acceptable |
| **LOW** | Minor impact; unlikely exploitation; acceptable residual risk |

---

## Required Output Structure

```markdown
# Stage 4: Risk Assessment
**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## Risk Assessment Table

| ID | Threat Name | Impact | Likelihood | Rating | Business Impact | Confidence |
|----|-------------|--------|------------|--------|-----------------|------------|
| T-001 | [Name] | HIGH | HIGH | CRITICAL | [Brief impact] | H |
| T-002 | [Name] | MEDIUM | HIGH | HIGH | [Brief impact] | M |

## Priority Groups

### CRITICAL Priority (Immediate Action)
| ID | Threat | Rating | Justification |
|----|--------|--------|---------------|
| T-001 | [Name] | CRITICAL | [1-2 sentence reason] |

### HIGH Priority (Near-Term)
| ID | Threat | Rating | Justification |
|----|--------|--------|---------------|
| T-005 | [Name] | HIGH | [1-2 sentence reason] |

### MEDIUM Priority (Planned)
| ID | Threat | Rating | Justification |
|----|--------|--------|---------------|

### LOW Priority (Monitor)
| ID | Threat | Rating | Justification |
|----|--------|--------|---------------|

## Data Limitations
| Gap | Affected Threats | Impact on Assessment |
|-----|------------------|---------------------|
| [Missing info] | T-001, T-005 | [How it affects rating] |

**Total Threats:** [N] | **CRITICAL:** [n] | **HIGH:** [n] | **MEDIUM:** [n] | **LOW:** [n]
**Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence]
```

---

## Assessment Factors

For each threat, consider:

### Impact Assessment
- **Confidentiality:** Data exposure scope and sensitivity
- **Integrity:** Data modification consequences
- **Availability:** Service disruption extent
- **Business:** Financial, regulatory, reputational consequences

### Likelihood Assessment
- **Attack Complexity:** Technical skill/resources required
- **Access Required:** Network position, credentials needed
- **Existing Controls:** Documented security measures
- **Attacker Motivation:** Value of target assets

### Combined Rating
| Impact ↓ / Likelihood → | HIGH | MEDIUM | LOW |
|-------------------------|------|--------|-----|
| **HIGH** | CRITICAL | HIGH | MEDIUM |
| **MEDIUM** | HIGH | MEDIUM | LOW |
| **LOW** | MEDIUM | LOW | LOW |

---

## Compact Threat Assessment Template

```markdown
### T-XXX: [Threat Name]
**Impact:** [H/M/L] - [Brief reason: e.g., "PII exposure", "service unavailable"]
**Likelihood:** [H/M/L] - [Brief reason: e.g., "no auth required", "requires insider"]
**Rating:** [CRITICAL/HIGH/MEDIUM/LOW]
**Business Impact:** [1 sentence: regulatory, financial, operational, reputational]
**Confidence:** [H/M/L] - [Data quality note if needed]

---
```

**Keep entries concise** - Brief justification, not lengthy analysis per threat

---

## Quality Rules

- **No fabricated metrics** - Don't invent user counts, revenue figures, costs
- **Justify ratings** - Brief reason for each impact/likelihood assessment
- **Document uncertainty** - Note when data gaps affect confidence
- **Reference Stage 1** - Use documented business context for impact assessment

---

## Completion Signal

```
✅ STAGE 4 WORK PHASE COMPLETE
- Output File: 04-risk-assessment.md
- Total Threats Assessed: [N]
- Priority Distribution: CRITICAL:[n] HIGH:[n] MEDIUM:[n] LOW:[n]
- Location: [target]/output/threat-model/
- Confidence: [HIGH/MEDIUM/LOW]
```

---
