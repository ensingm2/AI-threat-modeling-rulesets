# Documentation Specialist: Stage 6 Guide | Output: 06-final-comprehensive-report.md | Partner: Threat-Modeler

---

## Stage 6 Purpose

As a **supporting** documentation specialist for Stage 6, your responsibility is **formatting, compilation, and presentation quality**. The threat-modeler provides the security analysis content; you organize, format, and ensure professional presentation.

**Your Mission:**
- Compile information from Stages 1-5 into comprehensive report
- Format for executive and technical audiences
- Ensure professional presentation quality
- Verify completeness and internal consistency
- Create self-contained, comprehensible deliverable

**NOT Your Responsibility:**
- Security analysis synthesis (threat-modeler's role)
- Risk prioritization decisions (threat-modeler's role)
- Mitigation strategy selection (threat-modeler's role)

---

## Collaboration Model

### **Threat-Modeler Responsibilities (Content):**
- Synthesize security findings from Stages 3-5
- Prioritize threats and risks
- Select mitigation strategies to highlight
- Provide executive-appropriate security messaging
- Ensure technical accuracy of security content

### **Documentation-Specialist Responsibilities (Format & Organization):**
- Compile information from all stages
- Format for professional presentation
- Organize content for comprehensibility
- Create comprehensive tables and inventories
- Embed diagrams and visual elements
- Ensure self-contained report structure
- Verify cross-references and consistency

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `documentation-specialist/role-reminder.md` - Your role definition (formatting focus)
- `documentation-specialist/stage-6-guide.md` - This file
- `threat-modeler/role-reminder.md` - Collaborative partner's role (content synthesis)
- `threat-modeler/stage-6-final-reporting.md` - Content synthesis guidance
- `shared/output-file-requirements.md` - Output format specifications

### **REQUIRED Inputs (From Previous Stages):**
- `01-system-understanding.md` - System overview and architecture
- `02-data-flow-analysis.md` + DFD files - Data flow documentation
- `03-threat-identification.md` - Identified threats
- `04-risk-assessment.md` - Risk scores and priorities
- `05-mitigation-strategy.md` - Mitigation recommendations

### **OPTIONAL Files (Load if Needed):**
- `.ai-instructions/threat-modeling/stage-6-final-report-requirements.md` - Detailed report structure specifications
- `shared/confidence-calibration.md` - For verifying confidence level consistency

### **NOT NEEDED (Can Unload):**
- `documentation-specialist/stage-1-guide.md` - Stage 1 work complete
- `documentation-specialist/stage-2-guide.md` - Stage 2 work complete
- `threat-modeler/stage-3-threat-identification.md` - Stage 3 work complete
- `threat-modeler/stage-4-risk-assessment.md` - Stage 4 work complete
- `threat-modeler/stage-5-mitigation-strategy.md` - Stage 5 work complete
- Framework files (STRIDE, ATT&CK, Kill Chain) - Analysis complete, not needed for formatting

### **Outputs (Final Deliverable):**
- `06-final-comprehensive-report.md` - Self-contained comprehensive threat model report

---

## Step-by-Step Workflow

### **Step 1: Review All Prior Stage Outputs**

**Action:** Read and comprehend outputs from Stages 1-5

**Files to Review:**
- `01-system-understanding.md` (your Stage 1 work)
- `02-data-flow-analysis.md`, diagrams (your Stage 2 work)
- `03-threat-identification.md` (threat-modeler's work)
- `04-risk-assessment.md` (threat-modeler's work)
- `05-mitigation-strategy.md` (threat-modeler's work)

**Create Extraction Lists:**
```markdown
## Content Extraction Reference

### From Stage 1:
- System description and business purpose
- Component inventory (for architecture summary)
- Trust boundaries (for architecture summary)
- Key assumptions (for assumptions section)

### From Stage 2:
- Data Flow Diagram (Mermaid to embed)
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

**Action:** Create architecture overview with embedded DFD

**Content Sources:**
- Stage 1: Component inventory, trust boundaries (your work)
- Stage 2: Data Flow Diagram Mermaid (your work)

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

#### System Architecture Diagram

```mermaid
[EMBED FULL MERMAID DIAGRAM FROM STAGE 2]
```

**Diagram Description for Non-Technical Readers:**
[Explain what diagram shows, how to read it]

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
**Risk Rating:** [CVSS or qualitative]
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

**Report Completion Date:** [Date]
**Analysis Team:** Documentation Specialist + Threat Modeler
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
- [ ] Mermaid diagram embedded correctly
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
- [ ] **Architecture summary clear with embedded DFD**
- [ ] **Assumptions comprehensively documented**
- [ ] **Recommendations aligned with Stage 5**
- [ ] **Report self-contained** (comprehensible without stage files)
- [ ] **Professional formatting throughout**
- [ ] **Cross-references accurate**
- [ ] **No fabricated data** (maintain data integrity from earlier stages)
- [ ] **Limitations transparently acknowledged**

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
1. Save `06-final-comprehensive-report.md` to target directory
2. Verify with quality checklist above
3. Signal work phase complete
4. Quality-critic will review for:
   - Completeness (all threats included)
   - Self-contained comprehensibility
   - Professional presentation quality
   - Cross-stage consistency
   - Executive actionability

---

