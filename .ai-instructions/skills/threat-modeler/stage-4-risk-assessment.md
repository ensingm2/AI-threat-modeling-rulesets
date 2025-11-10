# Stage 4: Risk Assessment | Output: 04-risk-assessment.md

---

## Stage Objectives

### **Primary Goals:**
1. Assess risk severity for ALL threats identified in Stage 3
2. Apply CVSS v4.0 scoring when sufficient technical data available
3. Use qualitative risk assessment when CVSS inappropriate or data insufficient
4. Analyze business impact based on available data
5. Prioritize threats for mitigation planning
6. Document confidence levels and data limitations

### **Success Criteria:**
- Risk assessment appropriate for available data quality
- CVSS scoring ONLY when sufficient technical data available
- Qualitative assessment for non-CVSS threats with explicit justification
- Confidence calibration and uncertainty handling explicit
- Prioritization defensible and actionable for stakeholders

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `threat-modeler/role-reminder.md` - Your role definition (worker mode, CVSS constraints)
- `threat-modeler/stage-4-risk-assessment.md` - This file
- `shared/confidence-calibration.md` - Confidence level framework (critical for CVSS decisions)
- `shared/output-file-requirements.md` - Output format specifications

### **REQUIRED Inputs (From Previous Stages):**
- `03-threat-identification.md` - All threats to assess from Stage 3
- `01-system-understanding.md` - Business context, architecture details for impact assessment

### **OPTIONAL Files (Load if Needed):**
- None for this stage (all essential files listed as REQUIRED)

### **NOT NEEDED (Can Unload):**
- `threat-modeler/stage-3-threat-identification.md` - Stage 3 instruction work complete
- `threat-modeler/frameworks/quick-reference.md` - Framework reference (if needed for threat context)
- `shared/core-terms.md` - Core terminology internalized by this stage
- `shared/risk-assessment-terms.md` - Risk assessment specific terminology

### **Outputs for Next Stages:**
- `04-risk-assessment.md` - Risk scores, priorities, and business impact analysis
- Will be used by Stages 5-6 for prioritized mitigation and reporting

---

## CRITICAL REQUIREMENT: CVSS Scoring Constraints

### **GUIDING PRINCIPLE:**
**ALWAYS better to omit CVSS scoring than to guess, assume, or fabricate technical details.**

### **CVSS v4.0 Applicable When:**
- ✅ Technical vulnerability with documented attack vector
- ✅ ALL required technical data available for base metrics (AV, AC, AT, PR, UI, VC, VI, VA, SC, SI, SA)
- ✅ Source documentation supports each metric without assumptions
- ✅ Threat has technical exploitation vector (not business/policy risk)

### **CVSS NOT Applicable When:**
- ❌ Business process threats (discriminatory policies, unfair service allocation)
- ❌ Organizational policy violations (inadequate procedures, missing controls)
- ❌ Strategic/competitive risks (legal concerns, reputation damage)
- ❌ Regulatory compliance gaps (GDPR violations, policy non-compliance)
- ❌ Technical threats with insufficient implementation details

### **Required Base Metrics Documentation:**

Each CVSS metric MUST be justified with source documentation:

**Attack Vector (AV):** Network / Adjacent / Local / Physical
- Requires documented network architecture and access methods
- Example justification: "AV:N based on documented internet-facing API (api-spec.yaml, line 12)"

**Attack Complexity (AC):** Low / High
- Requires documented security controls and exploit prerequisites
- Example justification: "AC:L - no rate limiting documented (system-design.md analysis)"

**Privileges Required (PR):** None / Low / High
- Requires documented authentication and authorization architecture
- Example justification: "PR:N - endpoint publicly accessible without authentication (api-spec.yaml, endpoint /public/search)"

**User Interaction (UI):** None / Required
- Requires documented attack scenario and user involvement
- Example justification: "UI:N - automated exploitation possible without user action"

**Scope (S):** Unchanged / Changed
- Requires documented component boundaries and privilege contexts
- Example justification: "S:C - attack on API enables database access (architecture-diagram shows trust boundary crossing)"

**Confidentiality Impact (C):** None / Low / High
- Requires documented data classification and access scope
- Example justification: "C:H - documented PII exposure (data-catalog.md, user_profiles table contains SSN, DOB)"

**Integrity Impact (I):** None / Low / High
- Requires documented data modification capabilities
- Example justification: "I:H - write access to financial transaction records"

**Availability Impact (A):** None / Low / High
- Requires documented service availability requirements
- Example justification: "A:H - documented critical service with 99.9% SLA requirement"

### **CRITICAL PROHIBITION: No Assumption-Based CVSS Scoring**

**PROHIBITED Assumptions (Examples):**
- ❌ "Assuming AV:N because it's a web app" - requires documented network architecture
- ❌ "Assuming AC:L because no security controls mentioned" - requires documented security controls
- ❌ "Assuming PR:N because endpoint appears public" - requires documented authentication requirements
- ❌ "Assuming C:H because handles PII" - requires documented data classification and scope
- ❌ "Assuming S:C because different components" - requires documented trust boundaries

**If technical details are uncertain → Use qualitative risk rating with explicit data gap documentation**

## Required Analysis Activities

### **1. CVSS v4.0 Technical Scoring (When Applicable)**

**For Each Technically Exploitable Threat with Sufficient Data:**

```markdown
#### Threat: T-XXX - [Threat Title]
**CVSS v4.0 Base Score:** [0.0-10.0] ([NONE/LOW/MEDIUM/HIGH/CRITICAL])
**CVSS Vector String:** CVSS:4.0/AV:[N/A/L/P]/AC:[L/H]/AT:[N/P]/PR:[N/L/H]/UI:[N/P/A]/VC:[H/L/N]/VI:[H/L/N]/VA:[H/L/N]/SC:[H/L/N]/SI:[H/L/N]/SA:[H/L/N]

**Metric Justifications:**
- **AV (Attack Vector):** [N/A/L/P] - [Justification with source reference]
- **AC (Attack Complexity):** [L/H] - [Justification with source reference]
- **AT (Attack Requirements):** [N/P] - [Justification with source reference]
- **PR (Privileges Required):** [N/L/H] - [Justification with source reference]
- **UI (User Interaction):** [N/P/A] - [Justification with source reference]
- **VC (Confidentiality Impact on Vulnerable System):** [H/L/N] - [Justification with source reference]
- **VI (Integrity Impact on Vulnerable System):** [H/L/N] - [Justification with source reference]
- **VA (Availability Impact on Vulnerable System):** [H/L/N] - [Justification with source reference]
- **SC (Confidentiality Impact on Subsequent Systems):** [H/L/N] - [Justification with source reference]
- **SI (Integrity Impact on Subsequent Systems):** [H/L/N] - [Justification with source reference]
- **SA (Availability Impact on Subsequent Systems):** [H/L/N] - [Justification with source reference]

**Confidence in CVSS Assessment:** [HIGH/MEDIUM/LOW] - [Justification]
**Source References:** [List specific documentation supporting metric determinations]
```

### **2. Qualitative Risk Assessment (For Non-CVSS Threats)**

**For Business/Policy/Organizational Threats:**

```markdown
#### Threat: T-XXX - [Threat Title]
**Risk Rating:** [CRITICAL/HIGH/MEDIUM/LOW] (Business/Regulatory Risk)
**CVSS Score:** Not Applicable - [Reason: Business process threat / Policy violation / Insufficient technical data]

**Risk Assessment Components:**

**Threat Category:** [Business Process / Organizational Policy / Strategic Risk / Regulatory Compliance]

**Business Impact:**
- **Financial Impact:** [Qualitative description or quantitative if documented]
- **Regulatory Impact:** [Compliance violations and potential consequences]
- **Reputational Impact:** [Brand and customer trust implications]
- **Operational Impact:** [Business process disruption consequences]

**Likelihood Assessment:** [HIGH/MEDIUM/LOW]
**Likelihood Justification:** [Reasoning based on available information]

**Overall Risk Priority:** [CRITICAL/HIGH/MEDIUM/LOW]
**Prioritization Rationale:** [Why this risk level appropriate given impact and likelihood]

**Confidence Level:** [HIGH/MEDIUM/LOW/INSUFFICIENT] - [Justification]
**Data Limitations:** [What information would improve assessment confidence]
```

### **3. Technical Threats with Insufficient CVSS Data**

**For Technical Threats Lacking Complete Implementation Details:**

```markdown
#### Threat: T-XXX - [Threat Title]
**Risk Rating:** [CRITICAL/HIGH/MEDIUM/LOW] (Technical Threat - Insufficient Data for CVSS)
**CVSS Score:** Not Determined - Insufficient technical documentation

**Missing Technical Data Required for CVSS:**
- [Metric 1 - e.g., Authentication mechanism not specified (affects PR, AC)]
- [Metric 2 - e.g., Network exposure/API architecture undocumented (affects AV)]
- [Metric 3 - e.g., Data classification not documented (affects C, I)]

**Qualitative Risk Assessment:**
- **Threat Category:** Technical vulnerability ([specific type])
- **Potential Impact:** [CRITICAL/HIGH/MEDIUM/LOW] - [Impact description]
- **Likelihood:** [HIGH/MEDIUM/LOW] - [Likelihood reasoning]
- **Overall Risk Priority:** [CRITICAL/HIGH/MEDIUM/LOW]
- **Rationale:** [Why this priority appropriate despite incomplete CVSS data]

**Confidence Level:** [MEDIUM/LOW] - [Justification]
**Recommendation:** [What documentation needed to enable quantitative CVSS scoring]
```

### **4. Hybrid Threats (Technical + Business Impact)**

**For Threats Combining Technical Exploitation with Significant Business Consequences:**

```markdown
#### Threat: T-XXX - [Threat Title]

**Technical Risk Assessment:**
**CVSS v4.0 Score:** [0.0-10.0] ([NONE/LOW/MEDIUM/HIGH/CRITICAL])
**CVSS Vector:** CVSS:4.0/AV:[...]/AC:[...]/AT:[...]/PR:[...]/UI:[...]/VC:[...]/VI:[...]/VA:[...]/SC:[...]/SI:[...]/SA:[...]
**Technical Justification:** [Technical exploitation severity explanation]

**Business Impact Rating:** [CRITICAL/HIGH/MEDIUM/LOW]
**Business Impact Components:**
- **Regulatory Violations:** [Specific regulations and articles violated]
- **Financial Consequences:** [Financial impact description based on available data]
- **Reputational Damage:** [Brand and trust implications]
- **Operational Disruption:** [Business process impacts]

**Combined Risk Priority:** [CRITICAL/HIGH/MEDIUM/LOW]
**Combined Risk Rationale:** [How technical and business factors combine]
**Prioritization Recommendation:** [Immediate/High/Medium/Low priority with justification]

**Confidence Level:** [HIGH/MEDIUM/LOW] - [Justification]
```

### **5. Business Impact Analysis**

**Data-Driven Impact Assessment (When Business Data Available):**

```markdown
## Business Impact Categories

### Financial Impact
**Data Availability:** [Documented/Inferred/Unavailable]
**Sources:** [Specific documentation references or "Industry standards"]

**Impact Tiers:**
- **CRITICAL:** [Description based on documented data]
- **HIGH:** [Description based on documented data]
- **MEDIUM:** [Description based on documented data]
- **LOW:** [Description based on documented data]

### Regulatory Impact
**Applicable Regulations:** [List with source references]
- [Regulation 1]: [Specific requirements and documented applicability]
- [Regulation 2]: [Specific requirements and documented applicability]

**Compliance Violation Consequences:** [Based on documented regulatory requirements]

### Reputational Impact
**Assessment Basis:** [Documented brand positioning, market position, or industry standards]
**Impact Categories:** [Description of reputational impact tiers]

### Operational Impact
**Critical Business Processes:** [From documented business requirements]
**Impact Assessment:** [Disruption consequences based on documented dependencies]
```

**Qualitative Impact Assessment (When Quantitative Data Unavailable):**

```markdown
## Qualitative Business Impact Framework

**CRITICAL Impact:**
- [Criteria for critical impact based on documented system criticality]
- Examples: [Specific threat scenarios meeting this threshold]

**HIGH Impact:**
- [Criteria for high impact]
- Examples: [Specific threat scenarios]

**MEDIUM Impact:**
- [Criteria for medium impact]
- Examples: [Specific threat scenarios]

**LOW Impact:**
- [Criteria for low impact]
- Examples: [Specific threat scenarios]

**Confidence in Impact Assessment:** [HIGH/MEDIUM/LOW/INSUFFICIENT]
**Data Limitations:** [Specific business data gaps affecting assessment]
```

### **6. Risk Prioritization Matrix**

**Comprehensive Risk Ranking:**

```markdown
## Risk Prioritization Matrix

| Priority | Threat ID | Threat Name | CVSS/Risk Rating | Impact | Likelihood | Business Impact | Confidence |
|----------|-----------|-------------|------------------|---------|------------|-----------------|-----------|
| 1        | T-XXX     | [Name]      | [Score/Rating]   | [H/M/L] | [H/M/L]    | [Description]   | [H/M/L]   |
| 2        | T-XXX     | [Name]      | [Score/Rating]   | [H/M/L] | [H/M/L]    | [Description]   | [H/M/L]   |
| ...      | ...       | ...         | ...              | ...     | ...        | ...             | ...       |

### Priority Categories

**CRITICAL Priority (Immediate Action Required):**
- [List threat IDs and brief descriptions]
- [Rationale for critical prioritization]

**HIGH Priority (Near-Term Remediation):**
- [List threat IDs and brief descriptions]
- [Rationale for high prioritization]

**MEDIUM Priority (Planned Remediation):**
- [List threat IDs and brief descriptions]
- [Rationale for medium prioritization]

**LOW Priority (Monitoring/Future Consideration):**
- [List threat IDs and brief descriptions]
- [Rationale for low prioritization]
```

### **7. Likelihood Assessment**

**For Each Threat Document:**

```markdown
**Likelihood:** [HIGH/MEDIUM/LOW]

**Likelihood Factors:**
- **Attack Complexity:** [Assessment based on documented technical details]
- **Attacker Motivation:** [Assessment based on asset value and threat landscape]
- **Existing Controls:** [Assessment based on documented security controls]
- **Attack Surface Exposure:** [Assessment based on documented architecture]
- **Historical Precedent:** [Industry data on similar threat exploitation]

**Likelihood Justification:** [Comprehensive reasoning for likelihood assessment]
**Confidence in Likelihood:** [HIGH/MEDIUM/LOW] - [Justification]
```

### **8. Confidence and Data Limitations Documentation**

**Overall Assessment Quality:**

```markdown
## Risk Assessment Confidence & Limitations

**Overall Confidence Level:** [HIGH/MEDIUM/LOW]

**High Confidence Assessments ([N] threats):**
- [List threat IDs with brief reasoning for high confidence]

**Medium Confidence Assessments ([N] threats):**
- [List threat IDs with brief reasoning for medium confidence]
- [Data gaps affecting confidence]

**Low Confidence Assessments ([N] threats):**
- [List threat IDs with brief reasoning for low confidence]
- [Significant data limitations]

**Insufficient Data for Quantitative Assessment ([N] threats):**
- [List threat IDs requiring additional information]
- [Specific data needed to improve assessment]

### Critical Data Gaps
1. [Data Gap 1]: [How this affects risk assessment]
2. [Data Gap 2]: [How this affects risk assessment]
3. [Data Gap 3]: [How this affects risk assessment]

### Recommendations for Improved Assessment
- [Recommendation 1]: [What documentation/information needed]
- [Recommendation 2]: [What documentation/information needed]
- [Recommendation 3]: [What documentation/information needed]
```

## Output File Structure

### **Required Sections:**

```markdown
# Stage 4: Risk Assessment
**Target System:** [System Name]
**Analysis Date:** [Date]
**Operational Mode:** [Collaborative/Automatic]

## 1. Executive Summary
- Total threats assessed: [N]
- CVSS-scored threats: [N]
- Qualitative risk assessments: [N]
- Critical priority threats: [N]
- High priority threats: [N]
- Overall confidence in assessment: [HIGH/MEDIUM/LOW]
- Key data limitations affecting assessment

## 2. Risk Assessment Methodology
- CVSS v4.0 application criteria
- Qualitative risk assessment framework
- Business impact analysis approach
- Likelihood assessment methodology
- Confidence calibration approach

## 3. Business Impact Analysis
[Complete business impact framework and categories]

## 4. Individual Threat Risk Assessments

### CRITICAL Priority Threats
[Complete risk assessment for each critical threat]

### HIGH Priority Threats
[Complete risk assessment for each high priority threat]

### MEDIUM Priority Threats
[Complete risk assessment for each medium priority threat]

### LOW Priority Threats
[Complete risk assessment for each low priority threat]

## 5. Risk Prioritization Matrix
[Complete prioritization table and category summaries]

## 6. Confidence Assessment & Data Limitations
[Complete confidence documentation and data gaps]

## 7. Recommendations for Risk Assessment Improvement
[Specific recommendations for obtaining missing information]

## 8. Source Documentation References
- Complete list of all source documents used
- Key sections referenced for risk metrics
- Business data sources (if available)
```

## Common Pitfalls to Avoid

### **CVSS Assumption Fabrication:**
```markdown
❌ INCORRECT:
**CVSS v4.0 Score:** 8.1 (High)
**Vector:** CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:N/VA:N/SC:N/SI:N/SA:N
**Justification:** Assumes network-accessible API with no authentication

✅ CORRECT:
**Risk Rating:** HIGH (Technical Threat - Insufficient Data for CVSS)
**CVSS Score:** Not Determined - Insufficient technical documentation
**Missing Technical Data:**
- API network architecture not documented (affects AV)
- Authentication requirements not specified (affects PR, AC)
- Data classification not documented (affects C)
**Qualitative Assessment:** HIGH risk based on generic API security patterns
**Recommendation:** Obtain API architecture and authentication documentation
```

### **Business Metric Fabrication:**
```markdown
❌ INCORRECT:
**Financial Impact:** $2.5M - $8.7M based on estimated 10,000 customer records at $250-$870 per record

✅ CORRECT:
**Financial Impact:** HIGH (Qualitative)
**Basis:** Industry research indicates data breach costs average $150-$350 per record
**Data Limitation:** Customer count not documented, financial impact cannot be quantified
**Qualitative Assessment:** Significant financial impact likely given documented PII exposure
```

### **Unjustified Likelihood:**
```markdown
❌ INCORRECT:
**Likelihood:** HIGH - This type of attack is common

✅ CORRECT:
**Likelihood:** MEDIUM
**Justification:**
- Attack complexity: LOW (based on generic mobile app vulnerabilities)
- Attacker motivation: MEDIUM (documented user data has market value)
- Existing controls: UNKNOWN (security controls not documented)
- Industry precedent: HIGH (similar attacks documented in OWASP Mobile Top 10)
**Confidence:** LOW - Lacks system-specific security control documentation
```

## Stage 4 Critic Validation Focus

**Critic Must Verify:**
- CVSS scores used ONLY when ALL base metrics have documented justification
- No business metrics fabricated (revenue, costs, user counts)
- Qualitative assessments used appropriately when quantitative data unavailable
- All risk ratings have explicit justification and reasoning
- Confidence levels accurately reflect data quality
- Data limitations explicitly documented

**Critic Must Challenge:**
- Any CVSS metric without specific source documentation
- Quantitative business impact without documented financial/operational data
- Likelihood assessments without explicit reasoning
- High confidence ratings with insufficient source support
- Missing acknowledgment of data gaps and limitations
- Assumption-based CVSS components

**Minimum Issues Requirement:**
- Critic must identify at least 2-3 genuine analytical problems
- UNLESS work demonstrably meets all quality standards after thorough critical analysis
- Must actively seek issues rather than rubber-stamping

## References

**Related Skills:**
- `stage-3-threat-identification.md` - Threat inventory input for risk assessment
- `../shared/confidence-calibration.md` - Confidence level application guidance
- `../shared/output-file-requirements.md` - Output file format specifications
- `../../modes/collaborative-mode.md` - User interaction for clarifying business impact
- `../../modes/automatic-mode.md` - Autonomous risk assessment with limited data

---

**REMINDER: When modifying this skill, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

