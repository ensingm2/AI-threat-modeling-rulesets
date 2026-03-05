# Stage 6: Final Report | Threat Modeler + Documentation Specialist

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 6 work complete. Ready for critic analysis."

---

## Stage 6 Purpose

Stage 6 is the **ONLY** stage that produces a stakeholder-ready report. This is where executive summaries, comprehensive narratives, and polished presentation belong.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** All `ai-working-docs/*.json` files (components, boundaries, assets, flows, threats, risks, mitigations)
- **Fallback:** All `*.md` files from Stages 1-5
- Source documentation as needed (for additional context)

**Output:** `00-final-report.md` - Self-contained stakeholder deliverable (no JSON output for Stage 6)

**Guidance:** Comprehensive but focused - length scales with system complexity

---

## Required Report Structure

```markdown
# Threat Model Report: [System Name]
**Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## Executive Summary
[1-2 pages for leadership - this is the ONLY executive summary in all outputs]

### About This Threat Model
A threat model identifies **potential** security threats that could affect a system based on its architecture, technology stack, and data flows. It is important to understand that:

- **Threats are theoretical**: The presence of a threat in this report does not mean the system is currently vulnerable. Proper security controls and mitigations may already be in place.
- **This is not a vulnerability assessment**: We have not verified whether these threats are exploitable in the current implementation. A threat model informs secure design and highlights areas requiring attention.
- **Purpose**: This analysis helps prioritize security efforts, validate existing controls, and identify gaps requiring additional protection.

### Key Findings
- Total Threats: [N] across [N] components
- CRITICAL: [N] | HIGH: [N] | MEDIUM: [N] | LOW: [N]
- Primary Risk Areas: [Top 3-5]
- Overall Risk Posture: [CRITICAL/HIGH/MEDIUM/LOW]

### Critical Concerns
1. [Concern]: [Business impact]
2. [Concern]: [Business impact]
3. [Concern]: [Business impact]

### Priority Recommendations
1. **Immediate (CRITICAL):** [Summary]
2. **Short-Term (HIGH):** [Summary]
3. **Strategic (MEDIUM/LOW):** [Summary]

### Limitations
- [Key limitation 1]
- [Key limitation 2]

---

## 1. System Overview
[Consolidated from Stage 1 - business purpose, users, functionality]

## 2. Architecture Summary
> *For detailed component definitions (COMP-XXX) and trust boundary specifications (TB-XXX), refer to `01-system-understanding.md`. For data flow details (DF-XXX) and attack surface analysis (AS-XXX), refer to `02-data-flow-analysis.md`.*

[Key components table, data flow summary from Stage 2]

## 3. Assumptions
> *For detailed assumption rationale and impact analysis, refer to `01-system-understanding.md`.*

| # | Assumption | Basis | Impact if Wrong |
|---|------------|-------|-----------------|
[From Stage 1]

## 4. Threat Inventory (Priority-Sorted)
> *For detailed threat descriptions, attack scenarios, and affected components for any threat (T-XXX), refer to `03-threat-identification.md`.*

### CRITICAL Priority
| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
[ALL CRITICAL threats from Stage 3 with Stage 5 controls]

### HIGH Priority
| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
[ALL HIGH threats]

### MEDIUM Priority
| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
[ALL MEDIUM threats]

### LOW Priority
| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
[ALL LOW threats]

## 5. Implementation Roadmap
> *For detailed implementation steps, success criteria, and control specifications, refer to `05-mitigation-strategy.md`. For risk rating justifications, refer to `04-risk-assessment.md`.*

[Consolidated from Stage 5 - phased control implementation]

## 6. Conclusion
- Analysis completeness assessment
- Confidence level
- Recommended next steps
- Threat model maintenance guidance

---

## Appendices
- A: Detailed Stage Outputs (reference only)
- B: Glossary

---

## Report Generation Details

> **⚠️ AI-Generated Content Disclaimer**
> 
> This report was generated using the [AI Threat Modeling Framework](https://github.com/ensingm2/AI-threat-modeling-rulesets). AI-generated security analysis should be reviewed by qualified security professionals before use. No guarantees of accuracy or completeness are provided. This report is intended as a starting point for security analysis, not a definitive security assessment.

| Field | Value |
|-------|-------|
| **Generated** | [YYYY-MM-DD] |
| **Framework Version** | [Run `git rev-parse --short HEAD` or "Unknown"] |
| **Model** | [AI model name, e.g., "Claude Opus 4"] |
```

---

## Incremental Building Pattern

Stage 6 consolidates ALL threats - build incrementally:

1. **Create structure** with executive summary (write tool)
2. **Add system overview** and architecture (search_replace)
3. **Add threats by priority** - CRITICAL, then HIGH, then MEDIUM, then LOW (search_replace batches)
4. **Add roadmap and conclusion** (search_replace)
5. **Remove END_OF_FILE marker**
6. **Verify threat count** matches Stage 3 exactly

---

## Critical Requirements

### Threat Completeness
- **ALL Stage 3 threats MUST be in report** - Verify count matches exactly
- Priority-sort by Stage 4 ratings
- Include Stage 5 mitigations for each

### Executive Summary Quality
- **"About This Threat Model" section REQUIRED** - Define what a threat model is and clarify that threats are theoretical (not confirmed vulnerabilities)
- Non-technical language for leadership
- Business impact focus
- Actionable recommendations
- Clear next steps

### Self-Contained Document
- Report must be understandable without reading Stage 1-5 outputs
- Reference previous stages for details, but include essential context
- Include data flow summary in architecture section

---

## Quality Checklist

Before completion:
- [ ] **"About This Threat Model" section included** explaining that threats are theoretical and don't indicate current vulnerability
- [ ] Threat count matches Stage 3 exactly
- [ ] All CRITICAL/HIGH threats have mitigations listed
- [ ] Executive summary is non-technical
- [ ] Data flow overview in architecture section
- [ ] Assumptions documented
- [ ] Limitations acknowledged
- [ ] Mandatory footer included (see `shared/output-file-requirements.md`)

---

## Completion Signal

**⚠️ Do NOT include this in the output file. Communicate completion in your response only.**

After saving the output file, report completion in your response:
- Output File: 00-final-report.md
- Total Threats: [N] (verified matches Stage 3)
- Location: [target]/output/threat-model/
- Status: THREAT MODEL COMPLETE

---
