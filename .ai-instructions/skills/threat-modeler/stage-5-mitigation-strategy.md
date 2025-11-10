# Stage 5: Mitigation Strategy | Output: 05-mitigation-strategy.md

---

## Stage Objectives

### **Primary Goals:**
1. Recommend security controls mapped to specific identified threats
2. Provide implementation guidance appropriate to documented architecture
3. Prioritize controls based on risk assessment results
4. Assess implementation feasibility within documented constraints
5. Analyze residual risk after control implementation
6. Categorize recommendations into quick wins vs. long-term improvements

### **Success Criteria:**
- Mitigation strategies technically feasible within documented constraints
- Controls mapped to specific identified threats from Stage 3
- Priority-based implementation roadmap aligned with Stage 4 risk ratings
- Residual risk analysis complete for all proposed controls
- Implementation guidance actionable for technical teams
- Cost estimates ONLY if budget/resource data documented

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `threat-modeler/role-reminder.md` - Your role definition (worker mode, prohibitions)
- `threat-modeler/stage-5-mitigation-strategy.md` - This file
- `shared/confidence-calibration.md` - Confidence level framework
- `shared/output-file-requirements.md` - Output format specifications

### **REQUIRED Inputs (From Previous Stages):**
- `03-threat-identification.md` - Threats requiring mitigation
- `04-risk-assessment.md` - Risk priorities to guide mitigation prioritization
- `01-system-understanding.md` - Architecture constraints for feasibility assessment

### **OPTIONAL Files (Load if Needed):**
- None for this stage (all essential files listed as REQUIRED)

### **NOT NEEDED (Can Unload):**
- `threat-modeler/stage-3-threat-identification.md` - Stage 3 instruction work complete
- `threat-modeler/stage-4-risk-assessment.md` - Stage 4 instruction work complete
- Framework files (STRIDE, ATT&CK, Kill Chain) - Analysis complete
- `shared/core-terms.md` - Core terminology internalized

### **Outputs for Next Stages:**
- `05-mitigation-strategy.md` - Prioritized control recommendations and implementation roadmap
- Will be used by Stage 6 for final comprehensive report

---

## Required Analysis Activities

### **1. Threat-to-Control Mapping**

**For Each Identified Threat:**

```markdown
## Threat: T-XXX - [Threat Title]
**Risk Priority:** [CRITICAL/HIGH/MEDIUM/LOW]
**STRIDE Category:** [S/T/R/I/D/E]

### Recommended Controls

#### Control 1: [Control Name]
**Control Type:** [Preventive/Detective/Corrective]
**Control Category:** [Technical/Operational/Administrative]

**Mitigation Approach:**
[Detailed description of how this control addresses the threat]

**Implementation Guidance:**
- **Technical Requirements:** [Specific technical specifications]
- **Integration Points:** [How control integrates with documented architecture]
- **Configuration Details:** [Specific configuration recommendations]
- **Dependencies:** [Required prerequisites or supporting controls]

**Effectiveness Assessment:**
- **Threat Reduction:** [Complete/Substantial/Partial/Minimal]
- **Residual Risk:** [Remaining risk after control implementation]
- **Effectiveness Confidence:** [HIGH/MEDIUM/LOW] - [Justification]

**Implementation Feasibility:**
- **Technical Feasibility:** [HIGH/MEDIUM/LOW] - [Assessment]
- **Implementation Complexity:** [LOW/MEDIUM/HIGH]
- **Estimated Effort:** [Qualitative estimate if quantitative data unavailable]
- **Resource Requirements:** [General requirements, specific if documented]

**Priority:** [IMMEDIATE/HIGH/MEDIUM/LOW]
**Priority Justification:** [Reasoning based on risk reduction and feasibility]

**Source References:** [Documentation supporting feasibility assessment]
**Confidence Level:** [HIGH/MEDIUM/LOW] - [Justification]

#### Control 2: [Control Name]
[Same format as above]
```

### **2. Defense-in-Depth Strategy**

**Layered Security Approach:**

```markdown
## Defense-in-Depth Framework

### Layer 1: Perimeter Security
**Controls:**
- [Control 1]: [Brief description and threat coverage]
- [Control 2]: [Brief description and threat coverage]

**Threats Addressed:** [List threat IDs]
**Overall Layer Effectiveness:** [Assessment]

### Layer 2: Network Security
**Controls:**
- [Control 1]: [Brief description and threat coverage]
- [Control 2]: [Brief description and threat coverage]

**Threats Addressed:** [List threat IDs]
**Overall Layer Effectiveness:** [Assessment]

### Layer 3: Application Security
**Controls:**
- [Control 1]: [Brief description and threat coverage]
- [Control 2]: [Brief description and threat coverage]

**Threats Addressed:** [List threat IDs]
**Overall Layer Effectiveness:** [Assessment]

### Layer 4: Data Security
**Controls:**
- [Control 1]: [Brief description and threat coverage]
- [Control 2]: [Brief description and threat coverage]

**Threats Addressed:** [List threat IDs]
**Overall Layer Effectiveness:** [Assessment]

### Layer 5: Monitoring & Response
**Controls:**
- [Control 1]: [Brief description and threat coverage]
- [Control 2]: [Brief description and threat coverage]

**Threats Addressed:** [List threat IDs]
**Overall Layer Effectiveness:** [Assessment]
```

### **3. Priority-Based Implementation Roadmap**

**Phase-Based Implementation Plan:**

```markdown
## Implementation Roadmap

### Phase 0: Immediate Actions (0-30 days)
**Priority:** CRITICAL
**Focus:** Address critical and high-risk threats with quick-win controls

#### Immediate Action 1: [Control Name]
- **Threats Addressed:** [List threat IDs and names]
- **Risk Reduction:** [Quantified risk reduction based on Stage 4 assessments]
- **Implementation Effort:** [LOW/MEDIUM/HIGH]
- **Implementation Steps:**
  1. [Step 1 with specific actions]
  2. [Step 2 with specific actions]
  3. [Step 3 with specific actions]
- **Success Criteria:** [How to verify successful implementation]
- **Dependencies:** [Prerequisites or supporting activities]

#### Immediate Action 2: [Control Name]
[Same format as above]

**Phase 0 Summary:**
- **Total Controls:** [N]
- **Threats Addressed:** [N threat IDs]
- **Risk Reduction:** [Overall risk reduction assessment]
- **Resource Requirements:** [General requirements]

### Phase 1: Short-Term Improvements (1-3 months)
**Priority:** HIGH
**Focus:** Implement high-priority controls requiring moderate effort

#### Control 1: [Control Name]
[Same detailed format as Phase 0]

#### Control 2: [Control Name]
[Same detailed format as Phase 0]

**Phase 1 Summary:**
- **Total Controls:** [N]
- **Threats Addressed:** [N threat IDs]
- **Risk Reduction:** [Overall risk reduction assessment]
- **Resource Requirements:** [General requirements]

### Phase 2: Medium-Term Enhancements (3-6 months)
**Priority:** MEDIUM
**Focus:** Address medium-risk threats and foundational security improvements

[Same format as above]

### Phase 3: Long-Term Strategic Improvements (6-12 months)
**Priority:** LOW to MEDIUM
**Focus:** Comprehensive security program maturity and advanced controls

[Same format as above]

### Phase 4: Continuous Improvement (Ongoing)
**Priority:** LOW
**Focus:** Security program maintenance and evolving threat response

[Same format as above]
```

### **4. Control Effectiveness and Residual Risk Analysis**

**Comprehensive Risk Reduction Assessment:**

```markdown
## Control Effectiveness Analysis

### Overall Risk Posture Improvement
**Current State Risk Profile:**
- CRITICAL threats: [N] ([% of total])
- HIGH threats: [N] ([% of total])
- MEDIUM threats: [N] ([% of total])
- LOW threats: [N] ([% of total])

**Post-Mitigation Risk Profile (After All Controls Implemented):**
- CRITICAL threats: [N] → [N reduced to HIGH/MEDIUM/LOW]
- HIGH threats: [N] → [N reduced to MEDIUM/LOW]
- MEDIUM threats: [N] → [N reduced to LOW/ACCEPTED]
- LOW threats: [N] → [N reduced to ACCEPTED]

**Overall Risk Reduction:** [Percentage or qualitative assessment]
**Residual Risk Acceptance Required:** [Threats that cannot be fully mitigated]

### Individual Threat Risk Reduction

#### Threat T-XXX: [Threat Name]
**Original Risk:** [CRITICAL/HIGH/MEDIUM/LOW]
**Proposed Controls:**
- [Control 1]: [Effectiveness contribution]
- [Control 2]: [Effectiveness contribution]

**Residual Risk:** [CRITICAL/HIGH/MEDIUM/LOW]
**Residual Risk Justification:** [Why this risk remains after controls]
**Risk Acceptance Decision Required:** [YES/NO]
**Acceptance Justification:** [If acceptance required, explain why]

**Confidence in Effectiveness Assessment:** [HIGH/MEDIUM/LOW]

[Repeat for each threat]
```

### **5. Quick Wins vs. Strategic Investments**

**Categorization by Effort and Impact:**

```markdown
## Quick Wins (High Impact, Low Effort)
**Recommendation:** Implement immediately to achieve rapid risk reduction

### Quick Win 1: [Control Name]
- **Threats Addressed:** [List IDs]
- **Risk Reduction:** [Impact assessment]
- **Implementation Effort:** LOW
- **Implementation Timeline:** [Days/Weeks]
- **Cost Estimate:** [LOW / Not documented - require budget data]
- **ROI Assessment:** [Qualitative or quantitative if data available]

### Quick Win 2: [Control Name]
[Same format]

**Quick Wins Summary:**
- Total controls: [N]
- Total threats addressed: [N]
- Combined risk reduction: [Assessment]
- Recommended priority: IMMEDIATE

## Strategic Investments (High Impact, High Effort)
**Recommendation:** Plan and resource appropriately for maximum security value

### Strategic Investment 1: [Control Name]
- **Threats Addressed:** [List IDs]
- **Risk Reduction:** [Impact assessment]
- **Implementation Effort:** HIGH
- **Implementation Timeline:** [Months]
- **Cost Estimate:** [Qualitative estimate or "Requires detailed budget analysis"]
- **Long-Term Value:** [Strategic security posture improvement]

### Strategic Investment 2: [Control Name]
[Same format]

**Strategic Investments Summary:**
- Total controls: [N]
- Total threats addressed: [N]
- Combined risk reduction: [Assessment]
- Recommended priority: MEDIUM to HIGH (plan appropriately)

## Operational Necessities (Medium Impact, Low-Medium Effort)
**Recommendation:** Incorporate into regular security operations

[Similar format for medium impact/effort controls]

## Low Priority Enhancements (Low Impact or High Effort)
**Recommendation:** Consider for future security program maturity

[Similar format for low priority controls]
```

### **6. Implementation Guidance**

**Detailed Technical Specifications:**

```markdown
## Implementation Guide: [Control Name]

### Technical Architecture Integration
**Affected Components:** [List components from Stage 1 analysis]
**Integration Points:** [Specific integration locations]
**Data Flows Impacted:** [Reference Stage 2 data flows]
**Trust Boundaries Affected:** [Reference Stage 2 trust boundaries]

### Technical Specifications
**Technology Requirements:** [Specific technologies if documented, generic if not]
- [Requirement 1]: [Specification]
- [Requirement 2]: [Specification]

**Configuration Requirements:**
- [Configuration 1]: [Detailed settings]
- [Configuration 2]: [Detailed settings]

**Performance Considerations:**
- [Consideration 1]: [Impact and mitigation]
- [Consideration 2]: [Impact and mitigation]

### Implementation Steps
1. **[Phase 1]:** [Detailed steps]
   - [Sub-step 1.1]
   - [Sub-step 1.2]
2. **[Phase 2]:** [Detailed steps]
   - [Sub-step 2.1]
   - [Sub-step 2.2]
3. **[Phase 3]:** [Detailed steps]
   - [Sub-step 3.1]
   - [Sub-step 3.2]

### Testing and Validation
**Test Cases:**
- [Test case 1]: [Expected outcome]
- [Test case 2]: [Expected outcome]

**Validation Criteria:**
- [Criterion 1]: [How to verify]
- [Criterion 2]: [How to verify]

### Operational Considerations
**Maintenance Requirements:** [Ongoing maintenance needs]
**Monitoring Requirements:** [What to monitor]
**Incident Response Integration:** [How control affects IR procedures]

### Dependencies and Prerequisites
**Technical Dependencies:** [Required supporting systems/controls]
**Operational Dependencies:** [Required processes/procedures]
**Training Requirements:** [Staff training needed]

**Confidence in Implementation Guidance:** [HIGH/MEDIUM/LOW]
**Basis:** [Why this confidence level appropriate]
```

### **7. Compensating Controls Analysis**

**Alternative Control Options:**

```markdown
## Compensating Controls

### Threat: T-XXX - [Threat Name]
**Primary Control:** [Recommended control]
**Primary Control Limitation:** [Why alternative may be needed]

#### Compensating Option 1: [Alternative Control]
**Approach:** [How this alternative addresses the threat]
**Effectiveness:** [Comparison to primary control]
**Trade-offs:**
- **Advantages:** [Benefits over primary control]
- **Disadvantages:** [Limitations compared to primary control]
**Use Cases:** [When this alternative is appropriate]
**Recommendation:** [Guidance on selection]

#### Compensating Option 2: [Alternative Control]
[Same format]

**Compensating Control Selection Guidance:**
[Criteria for choosing between primary and compensating controls]
```

### **8. Cost-Benefit Analysis (Data-Constrained)**

**Evidence-Based Resource Planning:**

```markdown
## Resource Planning and Cost Considerations

### CRITICAL CONSTRAINT: Cost Estimation Requirements
**Available Budget/Resource Data:** [Documented/Not Documented]

**If NO budget data available:**
❌ **PROHIBITED:** Fabricating specific cost estimates ($XX,XXX)
✅ **REQUIRED:** Qualitative cost categories (LOW/MEDIUM/HIGH) with industry benchmarks

### Qualitative Cost Assessment

#### Cost Category Definitions
**LOW Cost:** [Description based on typical implementation patterns]
- Examples: [List low-cost control types]

**MEDIUM Cost:** [Description based on typical implementation patterns]
- Examples: [List medium-cost control types]

**HIGH Cost:** [Description based on typical implementation patterns]
- Examples: [List high-cost control types]

### Control Cost Categorization

| Control | Cost Category | Effort Level | Risk Reduction | ROI Assessment |
|---------|---------------|--------------|----------------|----------------|
| [Control 1] | LOW | LOW | HIGH | Excellent |
| [Control 2] | MEDIUM | MEDIUM | HIGH | Good |
| [Control 3] | HIGH | HIGH | MEDIUM | Moderate |

**Confidence in Cost Assessment:** [LOW - Requires detailed budget analysis]
**Recommendation:** [Conduct detailed cost analysis with procurement/finance teams]

### Risk-Adjusted Prioritization
**Highest ROI Controls:** [List controls offering best risk reduction per cost/effort]
**Resource-Constrained Approach:** [Recommended control sequence if budget limited]
```

## Output File Structure

### **Required Sections:**

```markdown
# Stage 5: Mitigation Strategy
**Target System:** [System Name]
**Analysis Date:** [Date]
**Operational Mode:** [Collaborative/Automatic]

## 1. Executive Summary
- Total threats requiring mitigation: [N]
- Total controls recommended: [N]
- Immediate actions required: [N]
- Expected risk reduction: [Overall assessment]
- Key implementation challenges
- Resource requirements summary

## 2. Mitigation Methodology
- Control selection framework
- Defense-in-depth approach
- Prioritization methodology
- Feasibility assessment criteria

## 3. Threat-to-Control Mapping
[Complete mapping for all threats from Stage 3]

## 4. Defense-in-Depth Framework
[Layered security strategy]

## 5. Priority-Based Implementation Roadmap
[Phase 0-4 with detailed control implementations]

## 6. Control Effectiveness and Residual Risk Analysis
[Comprehensive risk reduction assessment]

## 7. Quick Wins vs. Strategic Investments
[Categorized control recommendations]

## 8. Detailed Implementation Guidance
[Technical specifications for each control]

## 9. Compensating Controls Analysis
[Alternative control options]

## 10. Resource Planning and Cost Considerations
[Qualitative or quantitative cost analysis based on available data]

## 11. Success Metrics and Validation
- Control implementation success criteria
- Security posture improvement metrics
- Validation and testing requirements

## 12. Assumptions and Constraints
- Implementation assumptions
- Technical constraints
- Resource constraints
- Data limitations affecting recommendations

## 13. Source Documentation References
- Complete list of source documents
- Feasibility assessment basis
- Industry standards referenced
```

## Common Pitfalls to Avoid

### **Cost Fabrication:**
```markdown
❌ INCORRECT:
**Estimated Cost:** $45,000 - $78,000
**Implementation Timeline:** 3 months requiring 2 FTE

✅ CORRECT:
**Estimated Effort:** MEDIUM (Qualitative)
**Basis:** Typical web application firewall implementations require moderate licensing and integration effort
**Cost Category:** MEDIUM - Industry benchmarks suggest mid-range investment
**Recommendation:** Obtain vendor quotes and conduct detailed resource planning before budgeting
**Confidence:** LOW - Requires organization-specific cost analysis
```

### **Infeasible Recommendations:**
```markdown
❌ INCORRECT:
Implement hardware security modules (HSMs) for all cryptographic operations
[When documentation shows cloud-based serverless architecture]

✅ CORRECT:
Implement cloud-native key management service (e.g., AWS KMS, Azure Key Vault)
**Justification:** Aligned with documented cloud deployment model
**Source:** "Serverless architecture on AWS Lambda" (architecture.md, line 67)
**Feasibility:** HIGH - Native integration with documented platform
```

### **Vague Recommendations:**
```markdown
❌ INCORRECT:
Implement better authentication security

✅ CORRECT:
**Control:** Multi-Factor Authentication (MFA) for User Accounts
**Implementation Specifications:**
- MFA required for all user roles accessing sensitive functionality
- Support TOTP (RFC 6238) and/or WebAuthn protocols
- Fallback recovery mechanism with security questions or backup codes
- Integration point: Documented authentication service (Stage 1 component inventory)
**Threats Addressed:** T-003 (Credential Stuffing), T-015 (Account Takeover), T-022 (Session Hijacking)
```

## Stage 5 Critic Validation Focus

**Critic Must Verify:**
- All controls mapped to specific threats from Stage 3
- Implementation guidance feasible within documented architecture
- No cost estimates fabricated without budget data
- Residual risk analysis complete for all proposed controls
- Priority alignment with Stage 4 risk assessments
- Technical specifications actionable for implementation teams

**Critic Must Challenge:**
- Vague recommendations without specific implementation guidance
- Controls infeasible given documented constraints
- Missing residual risk analysis
- Cost estimates without documented budget/resource data
- Controls without clear threat mapping
- Implementation guidance inconsistent with documented architecture

**Minimum Issues Requirement:**
- Critic must identify at least 2-3 genuine analytical problems
- UNLESS work demonstrably meets all quality standards after thorough critical analysis
- Must actively seek issues rather than rubber-stamping

## References

**Related Skills:**
- `stage-3-threat-identification.md` - Threat inventory requiring mitigation
- `stage-4-risk-assessment.md` - Risk prioritization input for control prioritization
- `../shared/confidence-calibration.md` - Confidence level application guidance
- `../shared/output-file-requirements.md` - Output file format specifications
- `../../modes/collaborative-mode.md` - User interaction for implementation feasibility
- `../../modes/automatic-mode.md` - Autonomous mitigation strategy development

---

**REMINDER: When modifying this skill, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

