# Stage 6: Final Report | Documentation Specialist Support

**Role:** Worker Mode (Formatting Support) | **Constraints:** See `SKILL.md` | **On completion:** "Stage 6 work complete. Ready for critic analysis."

---

## Stage 6 Purpose

Supporting role for Stage 6: formatting, compilation, and presentation quality. The threat-modeler provides security analysis content; you organize and format for professional presentation.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** All `ai-working-docs/*.json` files (components, boundaries, assets, flows, threats, risks, mitigations)
- **Fallback:** All `*.md` files from Stages 1-5
- Source documentation as needed (for additional context)

**Output:** `00-final-report.md` - Self-contained stakeholder deliverable (no JSON output for Stage 6)

---

## Collaboration Model

| Role | Responsibilities |
|------|-----------------|
| **Threat-Modeler** | Security content synthesis, risk prioritization, mitigation selection, technical accuracy |
| **Documentation-Specialist** | Formatting, compilation, tables, diagrams, cross-references, professional presentation |

---

## Step-by-Step Workflow

### **Step 1: Review All Prior Stage Outputs**

**Action:** Read and comprehend outputs from Stages 1-5

**Files to Review (prefer JSON for structured data):**
- `ai-working-docs/01-*.json`, `02-*.json`, `03-threats.json`, `04-risk-assessments.json`, `05-mitigations.json`
- Fallback: `01-system-understanding.md` through `05-mitigation-strategy.md`

**Create Extraction Lists:**
```markdown
## Content Extraction Reference

### From Stage 1:
- System description and business purpose
- Component inventory (for architecture summary)
- Trust boundaries (for architecture summary)
- Key assumptions (for assumptions section)

### From Stage 2:
- Data flow summary (from JSON or markdown)
- Attack surface summary
- Critical data flow paths

### From Stage 3:
- ALL threats (complete inventory)
- Threat count by category
- Threat-modeler's prioritization

### From Stage 4:
- Risk ratings per threat
- Business impact analysis
- Risk prioritization matrix

### From Stage 5:
- Mitigation strategies by priority
- Implementation roadmap phases
- Quick wins identified
```

---

### **Step 2: Executive Summary Compilation**

**Action:** Create 1-2 page executive summary (collaborate with threat-modeler)

**Content Sources:**
- **System Overview:** From Stage 1 (your work)
- **Key Findings:** From threat-modeler's Stages 3-4
- **Critical Risks:** From threat-modeler's Stage 4
- **Recommendations:** From threat-modeler's Stage 5

**Executive Summary Structure:**
```markdown
## 1. Executive Summary

### Overview
[2-3 paragraphs: What system is, why threat modeling was conducted]
**Source:** Stage 1 system description
**Your Role:** Translate to executive-appropriate language

### Key Security Findings
**Threat-Modeler Content:**
- Total threats identified: [N] threats
- Critical priority: [N] threats requiring immediate action
- High priority: [N] threats requiring near-term remediation
- Primary risk areas: [Top 3-5 categories]

**Your Role:** Format as executive-friendly bullet points

### Business Impact Summary
**Threat-Modeler Content:**
- Regulatory exposure (GDPR, PCI-DSS, etc.)
- Financial risk assessment (if available)
- Operational risk considerations
- Reputational impact potential

**Your Role:** Organize into clear categories

### Priority Recommendations
**Threat-Modeler Content:**
1. Immediate actions (0-30 days)
2. Short-term improvements (1-3 months)
3. Strategic enhancements (3-12 months)

**Your Role:** Format for executive decision-making

### Analysis Confidence and Limitations
**Content:** From all stages (your Stage 1-2, threat-modeler's Stage 3-5)
- Overall confidence level
- Key limitations impacting analysis
- Data gaps affecting recommendations

**Your Role:** Synthesize into honest assessment
```

**Quality Criteria:**
- ✅ Non-technical language (no jargon without explanation)
- ✅ Business impact focus (not technical details)
- ✅ Actionable for C-level decision-making
- ✅ 1-2 pages maximum length

---

### **Step 3: Service Overview Consolidation**

**Action:** Compile business context from Stage 1

**Content Source:** Your Stage 1 work

**Format:**
```markdown
## 2. Service Overview

### Business Purpose
[Extract from Stage 1, ensure clarity for executives]

### Primary Users and Use Cases
**Users:**
- [User Type 1]: [Role and access]
- [User Type 2]: [Role and access]

**Key Use Cases:**
1. [Use Case 1]: [Description from Stage 1]
2. [Use Case 2]: [Description from Stage 1]

### Operational Context
[Deployment environment, scale, criticality - from Stage 1]

**Your Role:**
- Extract relevant content from Stage 1
- Ensure executive-appropriate language
- Maintain factual accuracy
- Add context for comprehensibility
```

---

### **Step 4: Architectural Design Summary**

**Action:** Create architecture overview with data flow summary

**Content Sources:**
- Stage 1: Component inventory, trust boundaries (your work)
- Stage 2: Data flow inventory, attack surfaces (your work)

**Structure:**
```markdown
## 3. Architectural Design Summary

### System Components Overview
[Table format for clarity]

| Component | Type | Function | Security Criticality |
|-----------|------|----------|---------------------|
| [Name] | [Type] | [Function from Stage 1] | [HIGH/MEDIUM/LOW] |
| [Name] | [Type] | [Function from Stage 1] | [HIGH/MEDIUM/LOW] |

**Your Role:** Compile from Stage 1, format professionally

### Component Interaction Overview
[Narrative description of how components work together]
**Source:** Stage 2 data flow analysis
**Your Role:** Create narrative for non-technical readers

### Trust Boundaries
**Major Trust Boundaries Identified:** [N] boundaries

1. **[Boundary Name]:** [Description from Stage 1]
   - **Separates:** [Zone A] ↔ [Zone B]
   - **Security Significance:** [Why this boundary matters]

[Repeat for all major boundaries]

### Data Flow Architecture

**Narrative Description:**
[High-level explanation of data movement patterns]
**Source:** Stage 2
**Your Role:** Executive-friendly description

#### Key Data Flows
[Summary of critical data paths from Stage 2, presented in prose or table format for executive understanding]

### Technology Stack Summary
**Source:** Stage 1
**Your Role:** Organize by documented/inferred/unknown

- **Documented Technologies:** [List]
- **Inferred Technologies:** [List with confidence]
- **Unknown Elements:** [List gaps]

### Attack Surface Summary
**Source:** Stage 2
**External Entry Points:** [N] identified

1. **[Entry Point Name]:** [Brief description and security relevance]
2. **[Entry Point Name]:** [Brief description and security relevance]
```

---

### **Step 5: Major System Assumptions Compilation**

**Action:** Consolidate critical assumptions from all stages

**Content Sources:**
- Stage 1: Your documented assumptions
- Stage 2: Your data flow assumptions
- Stages 3-5: Threat-modeler's analytical assumptions

**Format:**
```markdown
## 4. Major System Assumptions

### Critical Assumptions Affecting Analysis

#### Assumption 1: [Statement]
**Category:** [Technology/Architecture/Business/Operational]
**Stage:** [Where assumption originated]
**Confidence:** [HIGH/MEDIUM/LOW/INSUFFICIENT]
**Impact:** [How affects threat model]
**Source Stage:** [Stage number and file]

[Repeat for all major assumptions]

### Data Availability Summary
**HIGH Confidence Areas:**
- [Area 1]: [Description]

**MEDIUM Confidence Areas:**
- [Area 2]: [Description with gaps]

**LOW Confidence Areas:**
- [Area 3]: [Description with significant unknowns]

**INSUFFICIENT Data Areas:**
- [Area 4]: [Critical gaps]

### Recommendations for Improving Analysis
1. **[Recommendation]:** [What information would help]
2. **[Recommendation]:** [What documentation needed]

**Your Role:**
- Compile from all stage files
- Organize by confidence level
- Ensure clear presentation
```

---

### **Step 6: Priority-Sorted Threat Inventory**

**Action:** Create comprehensive table of ALL threats from Stage 3

**CRITICAL REQUIREMENT:** ALL threats must be included

**Content Source:** Threat-modeler's Stage 3 output file

**Format:**
```markdown
## 5. Priority-Sorted Threat Inventory

### Threat Inventory Summary
- **Total Threats Identified:** [N] threats
- **CRITICAL Priority:** [N] threats
- **HIGH Priority:** [N] threats
- **MEDIUM Priority:** [N] threats
- **LOW Priority:** [N] threats

**Verification:**
Stage 3 File Threat Count: [N]
Stage 6 Report Threat Count: [N]
**Status:** [✓ MATCH / ✗ MISMATCH - must fix if mismatch]

### Comprehensive Threat Table

#### CRITICAL Priority Threats

| ID | Threat Name | STRIDE | Risk | Business Impact | Mitigation Summary | Stage Ref |
|----|-------------|--------|------|-----------------|-------------------|-----------|
| T-XXX | [Name] | [S/T/R/I/D/E] | [Rating] | [Impact] | [1-2 sentences] | S3, S4, S5 |

**Detailed CRITICAL Threats:**

##### T-XXX: [Threat Name]
**STRIDE Category:** [Category]
**Risk Rating:** [CRITICAL/HIGH/MEDIUM/LOW]
**Description:** [Brief threat description]
**Business Impact:** [Impact from Stage 4]
**Recommended Mitigation:** [Primary control from Stage 5]
**Implementation Priority:** [From Stage 5]
**Detailed Analysis:** See Stage 3 (T-XXX), Stage 4 (Risk Assessment), Stage 5 (Mitigation)

[Repeat for all CRITICAL threats]

#### HIGH Priority Threats
[Same format - table + details]

#### MEDIUM Priority Threats
[Same format - can condense if many threats]

#### LOW Priority Threats
[Same format - condensed acceptable]

### Threat Coverage Statistics

**By STRIDE Category:**
| STRIDE | Total | Critical | High | Medium | Low |
|--------|-------|----------|------|--------|-----|
| Spoofing | [N] | [N] | [N] | [N] | [N] |
| Tampering | [N] | [N] | [N] | [N] | [N] |
[etc.]

**By Component:**
| Component | Total | Critical | High | Medium | Low |
|-----------|-------|----------|------|--------|-----|
| [Component 1] | [N] | [N] | [N] | [N] | [N] |
| [Component 2] | [N] | [N] | [N] | [N] | [N] |
[etc.]

**Your Role:**
- Extract ALL threats from Stage 3 file
- Organize by priority (from Stage 4)
- Create professional tables
- Summarize mitigation (from Stage 5)
- Verify completeness (count check)
- **CRITICAL:** Do NOT omit any threats
```

---

### **Step 7: Generalized Recommendations Compilation**

**Action:** Organize mitigation strategies from Stage 5

**Content Source:** Threat-modeler's Stage 5 output

**Format:**
```markdown
## 6. Generalized Recommendations

### Implementation Roadmap Overview
**Source:** Stage 5 mitigation strategy
- **Total Controls Recommended:** [N]
- **Implementation Phases:** [N] phases
- **Expected Risk Reduction:** [Summary from Stage 5]

### Phase 0: Immediate Actions (0-30 days)
**Priority:** CRITICAL

#### Action 1: [Control Name]
**Threats Addressed:** [IDs from inventory]
**Risk Reduction:** [From Stage 5]
**Implementation Summary:** [Brief from Stage 5]
**Success Criteria:** [From Stage 5]

[Repeat for all immediate actions]

**Phase 0 Expected Outcomes:**
- [Outcome 1 from Stage 5]
- [Outcome 2 from Stage 5]

### Phase 1: Short-Term Improvements (1-3 months)
[Same format]

### Phase 2-3: Medium and Long-Term
[Can condense if comprehensive]

### Defense-in-Depth Strategy
**Source:** Stage 5

**Perimeter Security Controls:**
- [Control 1]: [Brief from Stage 5]
- [Control 2]: [Brief from Stage 5]

**Application Security Controls:**
[etc.]

### Quick Wins
**High Impact, Low Effort Controls:**
1. **[Control Name]:** [Brief description and impact]
2. **[Control Name]:** [Brief description and impact]

### Strategic Investments
**High Impact, High Effort Controls:**
1. **[Control Name]:** [Long-term value proposition]
2. **[Control Name]:** [Long-term value proposition]

**Your Role:**
- Organize content from Stage 5
- Format for executive consumption
- Maintain threat-modeler's prioritization
- Create clear roadmap visualization
```

---

### **Step 8: Conclusion Compilation**

**Action:** Synthesize analysis completeness and next steps

**Content Sources:** All stages

**Format:**
```markdown
## 7. Conclusion

### Analysis Completeness
**Methodology Applied:**
- ✅ 6-stage systematic threat modeling
- ✅ STRIDE + MITRE ATT&CK + Kill Chain frameworks
- ✅ Evidence-based quality assurance

**Coverage Assessment:**
- **[N] system components** analyzed
- **[N] trust boundaries** assessed
- **[N] data flows** analyzed
- **[N] threats** identified
- **[N] security controls** recommended

### Analysis Quality and Confidence
**Overall Confidence:** [HIGH/MEDIUM/LOW]
**Source:** Confidence assessments from all stages

**High Confidence Areas:**
[From Stage 1-5 confidence assessments]

**Limited Confidence Areas:**
[From Stage 1-5 limitations]

### Known Limitations
**Documentation Gaps:**
1. **[Gap]:** [Impact from Stages 1-2]
2. **[Gap]:** [Impact from Stages 3-5]

**Analytical Constraints:**
[Compile from all stages]

### Recommended Next Steps

#### Immediate Actions (Within 7 Days)
1. **[Action]:** [From threat-modeler recommendations]
2. **[Action]:** [From threat-modeler recommendations]

#### Short-Term Actions (Within 30 Days)
1. **[Action]:** [Planning/initiation activities]
2. **[Action]:** [Documentation gathering]

#### Ongoing Activities
- **Threat Model Updates:** [Guidance from threat-modeler]
- **Continuous Monitoring:** [Metrics to track]
- **Incident Response Integration:** [How to use threat model]

### Final Remarks
[Threat-modeler provides security posture messaging]
**Your Role:** Format for executive consumption

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

### **Step 9: Self-Contained Comprehensibility Check**

**Action:** Verify report understandable without reading stage files

**Test Questions:**
- Can executive understand system without Stage 1?
- Are threats comprehensible without Stage 3 details?
- Are recommendations actionable without Stage 5 file?
- Does architecture make sense without full Stage 2?

**Comprehensibility Checklist:**
- [ ] Sufficient system context in Section 2
- [ ] Architecture description clear in Section 3
- [ ] Threats have enough detail in Section 5
- [ ] Recommendations actionable in Section 6
- [ ] Assumptions clearly explained in Section 4
- [ ] Cross-references supplementary, not required
- [ ] Non-technical readers can understand
- [ ] Technical readers find sufficient detail

**If Gaps Found:** Add context to make self-contained

---

### **Step 10: Professional Formatting & Quality**

**Action:** Apply professional presentation standards

**Formatting Checklist:**
- [ ] Consistent heading hierarchy (H1 → H2 → H3)
- [ ] Professional table formatting (aligned, complete)
- [ ] Data flow summary included
- [ ] Lists properly formatted (bullets vs. numbers)
- [ ] Cross-references accurate
- [ ] No broken links
- [ ] Consistent terminology (from Stage 1)
- [ ] Page breaks appropriate (if needed)
- [ ] Table of contents (if length warrants)

**Presentation Quality:**
- [ ] Executive summary polished
- [ ] Threat inventory complete and organized
- [ ] Recommendations clear and actionable
- [ ] Conclusion provides next steps
- [ ] Overall professional appearance

---

## Quality Checklist

Before considering Stage 6 complete:

- [ ] **ALL threats from Stage 3 included in inventory**
- [ ] **Threat count verification passed** (Stage 3 count = Stage 6 count)
- [ ] **Executive summary non-technical and actionable**
- [ ] **Architecture summary clear with data flow overview**
- [ ] **Assumptions comprehensively documented**
- [ ] **Recommendations aligned with Stage 5**
- [ ] **Report self-contained** (comprehensible without stage files)
- [ ] **Professional formatting throughout**
- [ ] **Cross-references accurate**
- [ ] **No fabricated data** (maintain data integrity from earlier stages)
- [ ] **Limitations transparently acknowledged**
- [ ] **Mandatory footer included** (see `shared/output-file-requirements.md`)

---

## Role Boundaries

**Remember Your Role:**
- ✅ **DO:** Format, organize, compile, present
- ✅ **DO:** Ensure professional quality and comprehensibility
- ✅ **DO:** Verify completeness (all threats included)
- ✅ **DO:** Create tables, embed diagrams, format text

- ❌ **DON'T:** Change threat-modeler's security analysis
- ❌ **DON'T:** Reprioritize threats or risks
- ❌ **DON'T:** Select different mitigation strategies
- ❌ **DON'T:** Add security content not in Stage 3-5 files

**When in Doubt:** Preserve threat-modeler's content; improve presentation only

---

## Output Handoff

**After Stage 6 Complete:**
1. Save `00-final-report.md` to target directory
2. Verify with quality checklist above
3. Signal work phase complete
4. Quality-critic will review for:
   - Completeness (all threats included)
   - Self-contained comprehensibility
   - Professional presentation quality
   - Cross-stage consistency
   - Executive actionability

---

