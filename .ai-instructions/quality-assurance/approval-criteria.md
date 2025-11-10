# Approval Criteria and Graduated System | Load: Approval Decision | ~800 tokens | Prereq: validation-protocol.md

---

## CAPABILITY-BASED QUALITY ENFORCEMENT

### **Evidence-Based Approval Criteria**

**Critic Performance Standards:**
- **Demonstrate thorough analytical validation** through systematic capability testing
- **Prove analytical competence** rather than meeting arbitrary rejection quotas
- **Focus on quality substance** over process compliance metrics

---

### **Stage-Specific Capability Validation**

#### **Stage 1 - System Understanding Validation:**
- **Architecture Comprehension**: Explain system in different terms than source documentation
- **Assumption Identification**: Challenge key assumptions with alternative interpretations
- **Scope Clarity**: Define boundaries with clear inclusion/exclusion criteria
- **Output File Validation**: Verify `01-system-understanding.md` created with complete analysis content

#### **Stage 2 - Data Flow Analysis Validation:**
- **Trust Boundary Logic**: Justify trust boundary placement with security reasoning
- **Attack Surface Mapping**: Demonstrate understanding through alternative categorization approaches
- **Component Interaction**: Validate data flow accuracy against documented architecture
- **Output File Validation**: Verify all three required files created (`02-data-flow-analysis.md`, `02-data-flow-diagram.mermaid`, `02-data-flow-diagram.drawio.xml`)
- **MANDATORY DFD FORMAT VALIDATION**: Content equivalency across all three formats, no missing elements

#### **Stage 3 - Threat Identification Validation:**
- **Framework Integration**: Show systematic STRIDE+ATT&CK+Kill Chain application
- **Threat Feasibility**: Validate attack scenarios against documented system capabilities
- **Coverage Completeness**: Demonstrate comprehensive threat enumeration approach
- **Output File Validation**: Verify `03-threat-identification.md` created with complete threat inventory

#### **Stage 4 - Risk Assessment Validation:**
- **CVSS Appropriateness**: Verify CVSS scoring only applied to technical threats with sufficient documented data
- **Threat Type Validation**: Confirm business/organizational threats use qualitative risk assessment
- **Scoring Justification**: Each CVSS component must reference specific documented system characteristics
- **Data Sufficiency Check**: Validate technical details available for all base metrics
- **Impact Analysis**: Appropriate handling of business impact given available data
- **Prioritization Logic**: Clear ranking methodology with stakeholder utility focus
- **Output File Validation**: Verify `04-risk-assessment.md` created with appropriate scoring methodology

#### **Stage 5 - Mitigation Strategy Validation:**
- **Control Relevance**: Ensure recommendations address identified threats specifically
- **Implementation Feasibility**: Validate technical practicality within documented constraints
- **Cost-Benefit Reasoning**: Appropriate analysis given available business data
- **Output File Validation**: Verify `05-mitigation-strategy.md` created with actionable recommendations

#### **Stage 6 - Final Report Validation:**
- **Executive Communication**: Assess actionability for business decision-making
- **Technical Accuracy**: Verify consistency with previous stage technical details
- **Uncertainty Transparency**: Appropriate data limitation acknowledgment
- **Output File Validation**: Verify `06-final-comprehensive-report.md` created as self-contained deliverable
- **MANDATORY STRUCTURE VALIDATION**: All 7 sections present, ALL Stage 3 threats included, cross-stage consistency

---

### **Quality Assurance Without Forced Iteration**

#### **Graduated Approval System:**

**CONFIDENT APPROVAL (≥90% quality confidence)**: 
- All capability validations demonstrate competence
- Proceed immediately to next stage

**CONDITIONAL APPROVAL (70-89% quality confidence)**:
- Most validations successful with minor concerns
- Address specific guidance, then proceed without re-review

**TARGETED REVISION (40-69% quality confidence)**:
- Several capability gaps identified  
- Focused rework on specific areas with clear success criteria

**MAJOR REWORK (<40% quality confidence)**:
- Fundamental analytical approach problems
- Complete stage restart with enhanced guidance

---

## Related Resources

- **`validation-protocol.md`** - Detailed 3-phase validation procedures
- **`critic-review-template.md`** - Structured response format
- **`core-principles.md`** - Foundational quality assurance principles

---

**This file defines approval criteria and graduated decision framework. Load critic-review-template.md for response structure.**

