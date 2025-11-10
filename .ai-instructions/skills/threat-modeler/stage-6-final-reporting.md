# Stage 6: Final Comprehensive Reporting | Output: 06-final-comprehensive-report.md

---

## ⚠️ CRITICAL: Batched Execution Requirement

**THIS RESPONSE MUST CONTAIN ONLY THE STAGE 6 WORK PHASE**

**MANDATORY PATTERN:**
1. Complete Stage 6 synthesis (consolidate all previous stages)
2. Create and save `06-final-comprehensive-report.md` using INCREMENTAL BUILDING (see below)
3. **END THIS RESPONSE** with completion signal
4. **DO NOT proceed to critic phase in same response**

**Completion Signal Format:**
```
✅ STAGE 6 WORK PHASE COMPLETE
- Output File: 06-final-comprehensive-report.md
- Total Threats in Report: [N] (must match Stage 3)
- Location: [target]/output/threat-model/
- Status: Ready for critic review
- Next Batch: Stage 6 Critic Phase
```

**PROHIBITED IN THIS RESPONSE:**
- ❌ Performing critic analysis
- ❌ Validating your own work
- ❌ Declaring threat model complete
- ❌ Combining work + validation phases

---

## ⚠️ CRITICAL: Incremental File Building - MANDATORY FOR STAGE 6

**PROBLEM:** Stage 6 produces a comprehensive report that consolidates ALL previous stages (including all Stage 3 threats). This creates a very large file (20,000+ lines) that WILL exceed tool parameter limits if created in a single `write` tool call.

**SOLUTION: ALWAYS build Stage 6 incrementally - this is NOT optional**

### **Incremental Building Pattern for Stage 6:**

```
Step 1: Create initial structure with executive summary
  → Use write tool (keeps file small)

Step 2: Add architecture and system overview sections
  → Use search_replace to add these sections

Step 3: Add priority-sorted threat inventory incrementally
  → Use search_replace to add threats in batches (e.g., CRITICAL, then HIGH, etc.)
  → This is the largest section - add in multiple batches

Step 4: Add mitigation recommendations
  → Use search_replace to add remaining sections

Final: Remove END_OF_FILE marker and verify completeness
```

### **Detailed Implementation:**

**Step 1 - Create Initial Structure:**
```markdown
Use write tool to create:
# Final Comprehensive Threat Model Report
[Header info + metadata]

## Executive Summary
[1-2 page executive summary - complete this first]

## Table of Contents
[TOC entries]

## 1. System Overview
[Placeholder - will add next]

---
END_OF_FILE
```

**Step 2 - Add System Overview and Architecture:**
```markdown
Use search_replace:
OLD: "## 1. System Overview\n[Placeholder - will add next]\n\n---\nEND_OF_FILE"
NEW: "## 1. System Overview\n[Full content from Stage 1]\n\n## 2. Architecture\n[Content + embedded DFD]\n\n## 3. Threat Landscape\n[Placeholder]\n\n---\nEND_OF_FILE"
```

**Step 3 - Add Priority-Sorted Threat Inventory (IN BATCHES):**

This is CRITICAL - Stage 3 threats can be 100+ items. Add incrementally by risk level:

```markdown
Batch 1 - Add CRITICAL threats:
OLD: "## 3. Threat Landscape\n[Placeholder]\n\n---\nEND_OF_FILE"
NEW: "## 3. Threat Landscape\n\n### 3.1 CRITICAL Risk Threats\n[All CRITICAL threats]\n\n[Next risk level placeholder]\n\n---\nEND_OF_FILE"

Batch 2 - Add HIGH threats:
OLD: "[Next risk level placeholder]\n\n---\nEND_OF_FILE"
NEW: "### 3.2 HIGH Risk Threats\n[All HIGH threats]\n\n[Next risk level placeholder]\n\n---\nEND_OF_FILE"

Continue for MEDIUM, LOW risk levels...
```

**Alternative:** Add by component if threats too numerous:
```markdown
## 3. Threat Landscape
### 3.1 Mobile Application Threats
[Add all mobile app threats - search_replace]

### 3.2 Backend API Threats  
[Add all backend threats - search_replace]

[Continue for each major component]
```

**Step 4 - Add Remaining Sections:**
```markdown
After all threats added:
- Mitigation Recommendations (search_replace)
- Assumptions and Limitations (search_replace)
- Conclusion (search_replace)
- Appendices (search_replace if needed)
```

**Step 5 - Remove END_OF_FILE marker:**
```markdown
Use search_replace:
OLD: "---\nEND_OF_FILE"
NEW: "" (empty string)
```

**Step 6 - Verify Completeness:**
```markdown
Critical verification:
- Read back threat count sections
- Confirm threat count matches Stage 3 exactly
- Verify all major sections present
```

### **Stage 6 Specific Tips:**

- **Threat consolidation:** All Stage 3 threats MUST be included - verify count matches
- **Priority sorting:** Group by risk level for easier incremental building
- **Executive summary last:** Write executive summary after building full report (or update it)
- **DFD embedding:** Embed Mermaid DFD in architecture section (copy from Stage 2)
- **Section size:** If one risk category has >30 threats, split into sub-batches
- **Cross-references:** Ensure internal cross-references accurate after all sections added

### **Why This is MANDATORY for Stage 6:**

- ❌ Single write tool call: WILL FAIL - report consolidates all 5 previous stages
- ❌ Building entire report in memory: WILL FAIL - exceeds limits
- ✅ Incremental building: Each major section manageable size
- ✅ Threat completeness: Can verify threat count incrementally
- ✅ Quality verification: Can review each section as added

### **CRITICAL Quality Gate:**

**Before signaling Stage 6 complete, VERIFY:**
- [ ] Threat count in report matches Stage 3 threat count EXACTLY
- [ ] All CRITICAL and HIGH threats from Stage 3 present in report
- [ ] Executive summary reflects complete report content
- [ ] DFD embedded in architecture section
- [ ] All assumptions from previous stages documented

---

## Stage Objectives

### **Primary Goals:**
1. Create single consolidated report serving as primary stakeholder deliverable
2. Synthesize findings from all previous stages (1-5) into coherent narrative
3. Present executive summary suitable for C-level decision-making
4. Provide comprehensive priority-sorted threat inventory (ALL threats from Stage 3)
5. Document major assumptions and analytical limitations transparently
6. Deliver actionable recommendations aligned with risk priorities
7. Ensure report is self-contained and comprehensible without referencing stage outputs

### **Success Criteria:**
- Report actionable for intended stakeholders (executives and technical teams)
- ALL threats from Stage 3 included in priority-sorted inventory
- Executive summary appropriate for business decision-making
- Self-contained report comprehensible without stage outputs
- Professional formatting suitable for stakeholder presentation
- Transparent documentation of assumptions and limitations
- Recommendations aligned with risk assessment and mitigation strategy

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `threat-modeler/role-reminder.md` - Your role definition (content synthesis focus)
- `threat-modeler/stage-6-final-reporting.md` - This file
- `documentation-specialist/role-reminder.md` - Collaborative partner's role (formatting)
- `documentation-specialist/stage-6-guide.md` - Formatting and organization guidance
- `shared/output-file-requirements.md` - Output format specifications

### **REQUIRED Inputs (From Previous Stages):**
- `01-system-understanding.md` - System overview and architecture
- `02-data-flow-analysis.md` + DFD files - Data flow documentation to embed
- `03-threat-identification.md` - Complete threat inventory
- `04-risk-assessment.md` - Risk priorities and scores
- `05-mitigation-strategy.md` - Mitigation recommendations and roadmap

### **OPTIONAL Files (Load if Needed):**
- `.ai-instructions/threat-modeling/stage-6-final-report-requirements.md` - Detailed report structure specifications
- `shared/confidence-calibration.md` - For verifying consistency

### **NOT NEEDED (Can Unload):**
- All stage-specific instruction guides (1-5) - Work complete, only outputs needed
- Framework files (STRIDE, ATT&CK, Kill Chain) - Analysis complete
- `shared/core-terms.md` - Core terminology internalized

### **Outputs (Final Deliverable):**
- `06-final-comprehensive-report.md` - Self-contained comprehensive threat model report for stakeholders

**Collaboration Note:** Work closely with Documentation Specialist for formatting; Threat Modeler provides content synthesis and security messaging, Documentation Specialist ensures professional presentation

---

## MANDATORY REPORT STRUCTURE

### **Required 7 Sections:**

Stage 6 MUST produce a comprehensive report with the following sections in this order:

1. **Executive Summary** (1-2 pages)
2. **Service Overview** (Business context)
3. **Architectural Design Summary** (with embedded DFD)
4. **Major System Assumptions** (Analytical constraints)
5. **Priority-Sorted Threat Inventory** (ALL threats from Stage 3)
6. **Generalized Recommendations** (Implementation roadmap)
7. **Conclusion** (Next steps and limitations)

## Required Report Content

### **1. Executive Summary**

**Purpose:** High-level overview for executive decision-making  
**Length:** 1-2 pages maximum  
**Audience:** Senior leadership, non-technical stakeholders

**Required Content:**

```markdown
## 1. Executive Summary

### Overview
[2-3 paragraph system summary and threat modeling purpose]

### Key Findings
- **Total Threats Identified:** [N] threats across [N] system components
- **Critical Priority Threats:** [N] requiring immediate action
- **High Priority Threats:** [N] requiring near-term remediation
- **Primary Risk Areas:** [List top 3-5 risk categories]
- **Overall Risk Posture:** [CRITICAL/HIGH/MEDIUM/LOW with brief justification]

### Critical Security Concerns
1. **[Concern 1]:** [Brief description and business impact]
2. **[Concern 2]:** [Brief description and business impact]
3. **[Concern 3]:** [Brief description and business impact]

### Business Impact Summary
- **Regulatory Exposure:** [GDPR, PCI-DSS, HIPAA, or other applicable regulations]
- **Financial Risk:** [Qualitative or quantitative if data available]
- **Operational Risk:** [Service disruption and business continuity concerns]
- **Reputational Risk:** [Customer trust and competitive positioning impact]

### Priority Recommendations
1. **Immediate Actions (0-30 days):** [Brief summary of critical controls]
2. **Short-Term Improvements (1-3 months):** [Brief summary of high-priority controls]
3. **Strategic Enhancements (3-12 months):** [Brief summary of foundational improvements]

### Analysis Confidence and Limitations
**Overall Confidence:** [HIGH/MEDIUM/LOW]
**Key Limitations:**
- [Limitation 1 - e.g., specific technology stack not documented]
- [Limitation 2 - e.g., business impact data unavailable for quantification]
- [Limitation 3 - e.g., operational scale and metrics not specified]

### Investment Priorities
[Brief guidance on resource allocation priorities based on risk and feasibility]

**Next Steps:** [Clear actions required from stakeholders]
```

### **2. Service Overview**

**Purpose:** Business context and operational understanding  
**Source:** Consolidated from Stage 1 system understanding

**Required Content:**

```markdown
## 2. Service Overview

### Business Purpose
[Service description, primary value proposition, business objectives]
**Source:** [Reference to Stage 1 documentation]

### Primary Users and Use Cases
**User Personas:**
- **[Persona 1]:** [Role, access level, primary activities]
- **[Persona 2]:** [Role, access level, primary activities]
- **[Persona 3]:** [Role, access level, primary activities]

**Key Use Cases:**
1. **[Use Case 1]:** [Description from Stage 1 analysis]
2. **[Use Case 2]:** [Description from Stage 1 analysis]
3. **[Use Case 3]:** [Description from Stage 1 analysis]

### Operational Context
**Deployment Environment:** [Documented deployment context]
**Operational Scale:** [If documented, otherwise note as undocumented]
**Business Criticality:** [Assessment based on documented requirements]
**Regulatory Context:** [Applicable regulations and compliance requirements]

### Key Functionality
[List major features and capabilities documented in Stage 1]
```

### **3. Architectural Design Summary**

**Purpose:** Technical context for security analysis  
**Source:** Consolidated from Stage 1 and Stage 2 analysis  
**MANDATORY:** Must include Data Flow Diagram

**Required Content:**

```markdown
## 3. Architectural Design Summary

### System Components

#### Component 1: [Component Name]
**Type:** [Component type from Stage 1]
**Function:** [Primary functionality]
**Technology:** [Documented or "Not specified"]
**Security Criticality:** [HIGH/MEDIUM/LOW]
**Key Security Considerations:** [Brief summary]

[Repeat for all major components]

### Component Interaction Overview
[High-level description of how components interact, referencing Stage 2 data flows]

### Trust Boundaries
**Major Trust Boundaries Identified:** [N] boundaries
- **[Boundary 1]:** [Description and security significance]
- **[Boundary 2]:** [Description and security significance]
- **[Boundary 3]:** [Description and security significance]

### Data Flow Architecture

[Narrative description of major data flows and trust boundary crossings]

#### System Architecture Diagram

```mermaid
[Embed Mermaid diagram from Stage 2 - 02-data-flow-diagram.mermaid]
```

**Diagram Description:** [Brief explanation of diagram elements for non-technical readers]

### Technology Stack Summary
**Documented Technologies:** [List explicitly documented technologies]
**Inferred Technologies:** [List reasonably inferred technologies with confidence levels]
**Unknown Elements:** [List technology areas not specified in documentation]

### Attack Surface Summary
**External Entry Points:** [N] identified
- [Entry point 1 with brief security considerations]
- [Entry point 2 with brief security considerations]
- [Entry point 3 with brief security considerations]

**Internal Attack Vectors:** [Brief summary of internal security considerations]
```

### **4. Major System Assumptions**

**Purpose:** Document analytical limitations and dependencies  
**Source:** Consolidated from all stages with confidence levels

**Required Content:**

```markdown
## 4. Major System Assumptions

### Critical Assumptions Affecting Analysis

#### Assumption 1: [Assumption Statement]
**Category:** [Technology/Architecture/Business/Operational]
**Basis:** [Why this assumption reasonable]
**Confidence Level:** [HIGH/MEDIUM/LOW/INSUFFICIENT]
**Impact on Analysis:** [How this assumption affects threat model]
**Validation Recommendation:** [How to confirm or refute]
**Source:** [Stage where assumption originated]

[Repeat for all major assumptions]

### Data Availability Summary
**HIGH Confidence Data:**
- [List areas with strong documentation]

**MEDIUM Confidence Data:**
- [List areas with reasonable inferences]

**LOW Confidence Data:**
- [List areas relying on industry patterns]

**Insufficient Data:**
- [List areas requiring additional documentation]

### Impact of Assumptions on Risk Assessment
[Explain how data limitations affect risk quantification and prioritization]

### Recommendations for Improving Analysis Confidence
1. **[Recommendation 1]:** [Specific documentation or information needed]
2. **[Recommendation 2]:** [Specific documentation or information needed]
3. **[Recommendation 3]:** [Specific documentation or information needed]
```

### **5. Priority-Sorted Threat Inventory**

**Purpose:** Complete actionable threat list for risk prioritization  
**CRITICAL REQUIREMENT:** ALL threats from Stage 3 output file MUST be included  
**Source:** Stage 3 (threat identification) and Stage 4 (risk assessment)

**Required Content:**

```markdown
## 5. Priority-Sorted Threat Inventory

### Threat Inventory Summary
- **Total Threats Identified:** [N]
- **CRITICAL Priority:** [N] threats
- **HIGH Priority:** [N] threats
- **MEDIUM Priority:** [N] threats
- **LOW Priority:** [N] threats

### Comprehensive Threat List

#### CRITICAL Priority Threats

| Threat ID | Threat Name | STRIDE | Risk Rating | Business Impact | Mitigation Summary | Stage Reference |
|-----------|-------------|--------|-------------|-----------------|-------------------|-----------------|
| T-XXX | [Threat name] | [S/T/R/I/D/E] | [CVSS/Rating] | [Impact] | [1-2 sentence mitigation] | Stage 3, 4, 5 |
| T-XXX | [Threat name] | [S/T/R/I/D/E] | [CVSS/Rating] | [Impact] | [1-2 sentence mitigation] | Stage 3, 4, 5 |

**Critical Threat Details:**

##### T-XXX: [Threat Name]
**Category:** [STRIDE category]
**Risk Rating:** [CVSS score or qualitative rating]
**Description:** [Brief threat description]
**Business Impact:** [Impact on business operations, compliance, reputation]
**Recommended Mitigation:** [Primary control recommendation]
**Implementation Priority:** [Immediate/High/Medium]
**Detailed Analysis:** See Stage 3 (T-XXX), Stage 4 (Risk Assessment), Stage 5 (Mitigation)

[Repeat for all critical threats]

#### HIGH Priority Threats

[Same format as Critical - table + detailed entries]

#### MEDIUM Priority Threats

[Same format - may use condensed format if many threats]

#### LOW Priority Threats

[Same format - condensed format acceptable]

### Threat Coverage by STRIDE Category

| STRIDE Category | Threat Count | Critical | High | Medium | Low |
|-----------------|--------------|----------|------|--------|-----|
| Spoofing | [N] | [N] | [N] | [N] | [N] |
| Tampering | [N] | [N] | [N] | [N] | [N] |
| Repudiation | [N] | [N] | [N] | [N] | [N] |
| Information Disclosure | [N] | [N] | [N] | [N] | [N] |
| Denial of Service | [N] | [N] | [N] | [N] | [N] |
| Elevation of Privilege | [N] | [N] | [N] | [N] | [N] |

### Threat Coverage by Component

| Component | Threat Count | Critical | High | Medium | Low |
|-----------|--------------|----------|------|--------|-----|
| [Component 1] | [N] | [N] | [N] | [N] | [N] |
| [Component 2] | [N] | [N] | [N] | [N] | [N] |
| [Component 3] | [N] | [N] | [N] | [N] | [N] |
```

### **6. Generalized Recommendations**

**Purpose:** Strategic security guidance and implementation roadmap  
**Source:** Consolidated from Stage 5 mitigation strategies

**Required Content:**

```markdown
## 6. Generalized Recommendations

### Implementation Roadmap Overview

**Total Controls Recommended:** [N]
**Implementation Phases:** [N] phases over [timeframe]
**Expected Risk Reduction:** [Overall assessment]

### Phase 0: Immediate Actions (0-30 days)

**Priority:** CRITICAL
**Objectives:** Address critical threats with rapid-deployment controls

#### Immediate Action 1: [Control Name]
**Threats Addressed:** [List threat IDs]
**Risk Reduction Impact:** [Quantified or qualitative assessment]
**Implementation Summary:** [Brief 2-3 sentence description]
**Success Criteria:** [How to verify effective implementation]
**Detailed Guidance:** See Stage 5, Section [X]

[Repeat for all immediate actions]

**Phase 0 Expected Outcomes:**
- [N] critical threats mitigated to acceptable levels
- [Overall risk reduction assessment]
- [Business impact protection achieved]

### Phase 1: Short-Term Improvements (1-3 months)

**Priority:** HIGH
**Objectives:** Implement high-priority controls requiring moderate effort

[Same format as Phase 0]

### Phase 2: Medium-Term Enhancements (3-6 months)

**Priority:** MEDIUM
**Objectives:** Address medium-risk threats and foundational improvements

[Similar format, may be more condensed]

### Phase 3: Long-Term Strategic Improvements (6-12 months)

**Priority:** MEDIUM to LOW
**Objectives:** Comprehensive security program maturity

[Similar format, condensed]

### Defense-in-Depth Strategy Summary

**Layer 1: Perimeter Security**
- [List key controls]
- Threats addressed: [Count and brief description]

**Layer 2: Network Security**
- [List key controls]
- Threats addressed: [Count and brief description]

**Layer 3: Application Security**
- [List key controls]
- Threats addressed: [Count and brief description]

**Layer 4: Data Security**
- [List key controls]
- Threats addressed: [Count and brief description]

**Layer 5: Monitoring & Response**
- [List key controls]
- Threats addressed: [Count and brief description]

### Quick Wins (High Impact, Low Effort)
1. **[Quick Win 1]:** [Brief description and impact]
2. **[Quick Win 2]:** [Brief description and impact]
3. **[Quick Win 3]:** [Brief description and impact]

### Strategic Investments (High Impact, High Effort)
1. **[Investment 1]:** [Brief description and long-term value]
2. **[Investment 2]:** [Brief description and long-term value]
3. **[Investment 3]:** [Brief description and long-term value]

### Resource Planning Considerations
**Cost Assessment:** [Qualitative categories if quantitative data unavailable]
**Effort Estimates:** [General effort levels by phase]
**Skill Requirements:** [Technical capabilities needed for implementation]
**Vendor/Tool Requirements:** [Third-party dependencies if applicable]

**Detailed Implementation Guidance:** See Stage 5 output file for complete technical specifications
```

### **7. Conclusion**

**Purpose:** Analysis completeness summary and next steps  
**Required Content:** Honest acknowledgment of data gaps and analytical constraints

**Required Content:**

```markdown
## 7. Conclusion

### Analysis Completeness

**Methodology Applied:**
- ✅ STRIDE framework applied systematically across all components
- ✅ MITRE ATT&CK technique mapping completed for all threats
- ✅ Kill Chain stage association documented
- ✅ CVSS v4.0 scoring applied where sufficient technical data available
- ✅ Qualitative risk assessment used appropriately for non-technical threats
- ✅ Defense-in-depth mitigation strategy developed

**Coverage Assessment:**
- **[N] system components** analyzed for security vulnerabilities
- **[N] trust boundaries** identified and assessed
- **[N] data flows** analyzed for security considerations
- **[N] threats** identified using systematic threat modeling
- **[N] security controls** recommended across [N] implementation phases

### Analysis Quality and Confidence

**Overall Confidence Level:** [HIGH/MEDIUM/LOW]

**High Confidence Areas:**
- [List areas with strong documentation and analysis confidence]

**Medium Confidence Areas:**
- [List areas with reasonable inferences but some uncertainty]

**Low Confidence Areas:**
- [List areas with significant data limitations]

**Insufficient Data Areas:**
- [List areas requiring additional documentation for proper analysis]

### Known Limitations

**Documentation Gaps:**
- [Limitation 1 affecting analysis]
- [Limitation 2 affecting analysis]
- [Limitation 3 affecting analysis]

**Analytical Constraints:**
- [Constraint 1 affecting recommendations]
- [Constraint 2 affecting recommendations]
- [Constraint 3 affecting recommendations]

**Impact of Limitations:**
[Explain how limitations affect actionability and completeness of recommendations]

### Recommended Next Steps

#### Immediate Actions (Within 7 Days)
1. **[Action 1]:** [Specific next step for stakeholders]
2. **[Action 2]:** [Specific next step for stakeholders]
3. **[Action 3]:** [Specific next step for stakeholders]

#### Short-Term Actions (Within 30 Days)
1. **[Action 1]:** [Planning or initiation activities]
2. **[Action 2]:** [Documentation or resource gathering]
3. **[Action 3]:** [Stakeholder engagement or approval]

#### Ongoing Activities
- **Threat Model Updates:** [Guidance on when to refresh analysis]
- **Continuous Monitoring:** [Key security metrics to track]
- **Incident Response Integration:** [How to leverage threat model in IR]

### Threat Model Maintenance

**Update Triggers:**
- Significant architectural changes
- New features or functionality additions
- Major technology stack changes
- Security incidents or vulnerability discoveries
- Regulatory requirement changes

**Recommended Update Frequency:** [Quarterly/Semi-annually/Annually based on system change velocity]

### Final Remarks
[Closing statement emphasizing security posture improvement opportunity and stakeholder action importance]

---

**Report Completion Date:** [Date]
**Analysis Team:** [If applicable]
**Report Distribution:** [Intended audience if applicable]
**Contact for Questions:** [If applicable]
```

## Output File Requirements

### **File Name:** `06-final-comprehensive-report.md`

### **File Location:** `[target-directory]/output/threat-model/`

### **Complete File Structure Template:**

```markdown
# Threat Modeling Report: [System Name]

**Report Date:** [Date]
**Analysis Methodology:** STRIDE + MITRE ATT&CK + Kill Chain
**Operational Mode:** [Collaborative/Automatic]

---

## Table of Contents
1. Executive Summary
2. Service Overview
3. Architectural Design Summary
4. Major System Assumptions
5. Priority-Sorted Threat Inventory
6. Generalized Recommendations
7. Conclusion

---

[All 7 sections as detailed above]

---

## Appendices (Optional)

### Appendix A: Detailed Stage Outputs
- Stage 1: System Understanding (`01-system-understanding.md`)
- Stage 2: Data Flow Analysis (`02-data-flow-analysis.md`, DFD files)
- Stage 3: Threat Identification (`03-threat-identification.md`)
- Stage 4: Risk Assessment (`04-risk-assessment.md`)
- Stage 5: Mitigation Strategy (`05-mitigation-strategy.md`)

### Appendix B: Methodology References
- STRIDE Framework: [Brief description or reference]
- MITRE ATT&CK: [Brief description or reference]
- Kill Chain: [Brief description or reference]
- CVSS v4.0: [Brief description or reference]

### Appendix C: Glossary
[Key terms and definitions for stakeholder reference]
```

## Quality Validation Checklist

**Before completing Stage 6, verify:**

- [ ] Executive Summary is non-technical and actionable for C-level stakeholders
- [ ] Service Overview provides sufficient business context
- [ ] Architecture Overview accurately represents system from Stage 1/2 analysis
- [ ] Mermaid DFD embedded and renders correctly in markdown preview
- [ ] Assumptions section comprehensively documents analytical constraints
- [ ] **ALL threats from Stage 3 output file (`03-threat-identification.md`) included in priority-sorted inventory**
- [ ] Threat inventory properly sorted by risk priority (Critical → High → Medium → Low)
- [ ] Risk ratings consistent with Stage 4 assessment
- [ ] Mitigation recommendations align with Stage 5 strategies
- [ ] Cross-references to detailed stage outputs are accurate and complete
- [ ] Report is self-contained - executives can make decisions without reading all stage files
- [ ] Professional formatting with clear section headings and table of contents
- [ ] Known limitations and data gaps transparently acknowledged
- [ ] Next steps are clear and actionable
- [ ] No fabricated data (costs, metrics, technologies without documentation)
- [ ] Appropriate confidence levels documented throughout

## Common Pitfalls to Avoid

### **Incomplete Threat Inventory:**
```markdown
❌ INCORRECT:
[Only listing critical and high threats in final report]

✅ CORRECT:
[Including ALL threats from Stage 3, organized by priority]
**Total Threats from Stage 3:** 45 threats
- CRITICAL: 5 threats (detailed entries)
- HIGH: 12 threats (detailed entries)
- MEDIUM: 18 threats (condensed entries)
- LOW: 10 threats (condensed entries)
```

### **Over-Technical Executive Summary:**
```markdown
❌ INCORRECT:
"CVSS 8.1 SQL injection vulnerability in API endpoint /users/{id} due to insufficient parameterization..."

✅ CORRECT:
"Critical security vulnerabilities could enable unauthorized access to customer data, resulting in regulatory violations and reputational damage. Immediate security improvements recommended."
```

### **Missing Self-Contained Context:**
```markdown
❌ INCORRECT:
"See Stage 3 for threat details" [without providing sufficient context in report]

✅ CORRECT:
"Threat T-015 (Authentication Bypass) allows unauthorized account access through session management flaws. Detailed analysis in Stage 3 (T-015), Stage 4 (Risk Assessment), Stage 5 (Mitigation Controls)."
```

### **Unacknowledged Limitations:**
```markdown
❌ INCORRECT:
[Presenting recommendations as definitive without noting data gaps]

✅ CORRECT:
"Recommendations based on generic mobile application security patterns due to undocumented specific technology stack. Implementation guidance should be refined once React Native framework confirmed."
```

## Stage 6 Critic Validation Focus

**Critic Must Verify:**
- Executive summary appropriate for non-technical stakeholders
- ALL threats from Stage 3 included in priority inventory
- Threat inventory properly sorted by risk priority
- Architecture summary matches Stage 1/2 analysis
- DFD embedded correctly and renders
- Assumptions documented transparently
- Recommendations aligned with Stage 4/5 analysis
- Report is self-contained and comprehensible
- No fabricated data or unjustified claims
- Professional formatting and presentation quality

**Critic Must Challenge:**
- Missing threats from Stage 3 inventory
- Overly technical language in executive summary
- Inconsistencies between stages
- Missing or inadequate assumption documentation
- Recommendations not aligned with risk priorities
- Inadequate acknowledgment of limitations
- Report requiring stage output references to understand
- Unprofessional formatting or presentation

**Minimum Issues Requirement:**
- Critic must identify at least 2-3 genuine analytical problems
- UNLESS work demonstrably meets all quality standards after thorough critical analysis
- Must actively seek issues rather than rubber-stamping

## References

**Related Skills:**
- `stage-1-system-understanding.md` - Source for service overview and architecture
- `stage-2-data-flow-analysis.md` - Source for DFD and data flow narrative
- `stage-3-threat-identification.md` - **CRITICAL SOURCE for complete threat inventory**
- `stage-4-risk-assessment.md` - Source for risk ratings and prioritization
- `stage-5-mitigation-strategy.md` - Source for recommendations and roadmap
- `../shared/confidence-calibration.md` - Confidence level documentation guidance
- `../shared/output-file-requirements.md` - Output file format specifications

---

**REMINDER: When modifying this skill, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

