# Stage 6: Final Report | Threat Modeler + Documentation Specialist

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 6 work complete. Ready for critic analysis."

---

## Stage 6 Purpose

Stage 6 is the **ONLY** stage that produces a stakeholder-ready report. This is where executive summaries, comprehensive narratives, and polished presentation belong.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** All `ai-working-docs/*.json` files (components, boundaries, assets, flows, threats, risks, mitigations)
- **Fallback:** All `*.md` files from Stages 1-5
- Source documentation as needed (for additional context)

**Output:** `06-final-comprehensive-report.md` - Self-contained stakeholder deliverable (no JSON output for Stage 6)

**Guidance:** Comprehensive but focused - length scales with system complexity

---

## Required Report Structure

```markdown
# Threat Model Report: [System Name]
**Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## Executive Summary
[1-2 pages for leadership - this is the ONLY executive summary in all outputs]

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
1. **Immediate (0-30 days):** [Summary]
2. **Short-Term (1-3 months):** [Summary]
3. **Strategic (3-12 months):** [Summary]

### Limitations
- [Key limitation 1]
- [Key limitation 2]

---

## 1. System Overview
[Consolidated from Stage 1 - business purpose, users, functionality]

## 2. Architecture Summary
[Key components table, data flow summary from Stage 2]

## 3. Assumptions
| # | Assumption | Basis | Impact if Wrong |
|---|------------|-------|-----------------|
[From Stage 1]

## 4. Threat Inventory (Priority-Sorted)

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
- [ ] Threat count matches Stage 3 exactly
- [ ] All CRITICAL/HIGH threats have mitigations listed
- [ ] Executive summary is non-technical
- [ ] Data flow overview in architecture section
- [ ] Assumptions documented
- [ ] Limitations acknowledged

---

## Completion Signal

**⚠️ Do NOT include this in the output file. Communicate completion in your response only.**

After saving the output file, report completion in your response:
- Output File: 06-final-comprehensive-report.md
- Total Threats: [N] (verified matches Stage 3)
- Location: [target]/output/threat-model/
- Status: THREAT MODEL COMPLETE

---
