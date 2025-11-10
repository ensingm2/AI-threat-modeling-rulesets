# Stage-Specific Validation Guide

**Purpose:** Detailed validation criteria for each threat modeling stage  
**Skill:** Quality Critic

---

## Stage 1: System Understanding & Scoping Validation

### **Primary Skill:** Documentation-Specialist
### **Validation Focus:** Technical accuracy, data integrity, source traceability

**NOTE:** Quality-critic focuses on TECHNICAL REVIEW - identifying gaps, hallucinations, and fabrications. Documentation readability/style is secondary to data integrity.

### **Validation Objectives:**
- Verify no fabricated technology stacks or business metrics (CRITICAL)
- Ensure all components have source documentation (CRITICAL)
- Validate assumption documentation with alternatives
- Check confidence levels appropriate for data quality
- Identify data gaps and missing information (hallucination prevention)

### **Critical Validation Checks:**

#### **1. Component Inventory Review**
**Check Each Component For:**
- [ ] Source documentation reference (file, line number)
- [ ] Technology stack clearly marked as Documented/Inferred/Unknown
- [ ] No specific frameworks (React Native, PostgreSQL, Node.js) without explicit documentation
- [ ] Data handled appropriate to documented functionality
- [ ] **Collaborative Mode Only:** User-provided information has cross-reference to clarifying questions file

**Red Flags:**
- ❌ "Backend uses Node.js with Express framework" without source quote
- ❌ "Database: PostgreSQL 13.2" when not documented
- ❌ "React Native mobile application" inferred without evidence
- ❌ **Collaborative Mode:** User clarification incorporated without reference to questions file

**Correct Patterns:**
- ✅ "Cross-platform mobile application (iOS/Android documented, framework not specified)"
- ✅ "Backend API (implementation technology not documented in source materials)"
- ✅ "Technology: Node.js" Source: "npm install command documented in README.md line 45"
- ✅ **Collaborative Mode:** "Fleet size: 5,000 bikes across 3 cities. *Source: User clarification (see Question 2 in 01_clarifying_questions.md)*"

#### **2. Trust Boundary Validation**
**Check Each Boundary For:**
- [ ] Clear separation rationale with security justification
- [ ] Components on each side identified
- [ ] Security implications documented
- [ ] Authentication/authorization requirements specified

**Challenge:**
- Are trust boundaries justified or arbitrary?
- Do boundaries align with security control needs?
- Are any boundaries missing (privilege levels, network zones)?

#### **3. Data Asset Catalog Review**
**Check Each Asset For:**
- [ ] Sensitivity classification with justification
- [ ] Regulatory applicability explicitly stated
- [ ] Storage and transmission locations from Stage 1 components
- [ ] No fabricated retention requirements

**Red Flags:**
- ❌ "10 million user records" without source
- ❌ "$500M annual transaction volume" invented
- ❌ Specific data schemas not documented

#### **4. Assumptions Documentation**
**Check Each Assumption For:**
- [ ] Explicit confidence level (HIGH/MEDIUM/LOW/INSUFFICIENT)
- [ ] Alternative interpretations provided
- [ ] Impact if assumption incorrect
- [ ] Validation recommendation

**Quality Criteria:**
- Specific assumptions (not "system uses standard security practices")
- Alternative scenarios considered
- Confidence level matches data quality
- Impact analysis shows understanding of dependencies

### **Stage 1 Quality Scoring:**

**Data Integrity (1-5):**
- **5:** No fabricated technologies/metrics, all components sourced
- **3:** Some technology inferences without clear marking
- **1:** Fabricated technology stacks or business metrics

**Source Traceability (1-5):**
- **5:** All components have specific documentation references (including user clarifications cross-referenced in Collaborative Mode)
- **3:** Most components referenced, some gaps
- **1:** Minimal source documentation

**Analytical Depth (1-5):**
- **5:** Comprehensive component coverage, thorough assumptions
- **3:** Adequate coverage with notable gaps
- **1:** Insufficient component analysis

**Critical Questions to Challenge:**
1. How do you know this technology is used? (Demand source quote)
2. What alternative architectures could explain the documented functionality?
3. Are there missing components not identified?
4. Are assumptions documented with sufficient specificity?
5. Do confidence levels match available data quality?

### **Mandatory Challenge Questions (MUST Address ALL)**

**For Stage 1, critic MUST explicitly address:**

1. **Data Integrity Challenge:**
   - Are ANY technology specifics (frameworks, versions, languages) not directly quoted from source?
   - Could confidence levels be MORE conservative given limited documentation?
   - What if a source quote is misinterpreted - what alternative meaning could it have?
   - Are there any business metrics or numbers that lack explicit source quotes?

2. **Completeness Challenge:**
   - What is the MOST SIGNIFICANT component or system element that might be missing?
   - What edge cases or unusual scenarios weren't explored?
   - What alternative system architectures weren't considered?
   - What trust boundaries might exist but weren't documented?

3. **Methodology Challenge:**
   - Could a different component categorization approach be superior?
   - Are there unstated methodological limitations in the analysis?
   - What implicit assumptions underlie the analytical approach itself?
   - Could assumptions be stated more conservatively?

4. **Stakeholder Utility Challenge:**
   - Would a CISO find this component inventory actionable for security decisions?
   - What critical security information is missing that executives would need?
   - Could trust boundary analysis be more specific?
   - Are data asset classifications defensible to auditors?

**Failure to address all 4 challenges = Incomplete critic analysis = Automatic rejection**

---

## Stage 2: Data Flow Analysis Validation

### **Primary Skill:** Documentation-Specialist
### **Validation Focus:** DFD content equivalency, data integrity, technical gaps

**NOTE:** Quality-critic focuses on TECHNICAL REVIEW - verifying triple-format equivalency, identifying fabricated protocols, catching missing flows. Diagram aesthetics/layout are secondary.

### **Validation Objectives:**
- Verify triple-format DFD content equivalency (CRITICAL - count verification)
- Validate trust boundary crossing logic and justification
- Ensure attack surface mapping comprehensive (no missing entry points)
- Check data flow accuracy against Stage 1 architecture
- Identify protocol/technical detail fabrications (hallucination prevention)

### **Critical Validation Checks:**

#### **1. Triple-Format DFD Equivalency**
**MANDATORY:** Verify all three DFD formats contain IDENTICAL content

- [ ] Same number of data flows across Text/Mermaid/Draw.io
- [ ] Identical trust boundary definitions in all formats
- [ ] Complete component coverage in each representation
- [ ] Consistent data element identification
- [ ] All security considerations documented in markdown format

**Validation Process:**
1. Count data flows in markdown table → [N] flows
2. Count flows in Mermaid diagram → [N] flows (must match)
3. Count flows in Draw.io XML → [N] flows (must match)
4. Spot-check 5-10 flows for content consistency across formats

**Red Flag:**
- ❌ Mermaid diagram missing flows present in markdown
- ❌ Draw.io XML shows different trust boundaries than text description
- ❌ Security considerations only in one format

#### **2. Data Flow Documentation Quality**
**Check Each Flow For:**
- [ ] Source and destination components from Stage 1
- [ ] Data elements transmitted specified
- [ ] Protocol documented if available, marked unknown if not
- [ ] Trust boundary crossing identified and justified
- [ ] Security considerations specific to flow

**Red Flags:**
- ❌ Vague data elements ("user data" without specifics)
- ❌ Assumed protocols not documented (e.g., assuming HTTPS)
- ❌ Missing trust boundary crossing notation
- ❌ Generic security considerations not flow-specific

#### **3. Trust Boundary Logic Validation**
**Challenge Boundary Placements:**
- Does boundary placement make security sense?
- Are boundaries consistent with Stage 1 analysis?
- Is security control enforcement at boundary documented?
- Are any critical boundaries missing?

**Look For:**
- Network perimeter boundaries (internet ↔ DMZ ↔ internal)
- Process boundaries (different execution contexts)
- Privilege boundaries (user ↔ admin)
- Organizational boundaries (internal ↔ third-party)

#### **4. Attack Surface Mapping**
**Validate Completeness:**
- [ ] All external entry points identified
- [ ] Authentication requirements per entry point
- [ ] Input validation approaches documented or flagged as unknown
- [ ] Mapping to specific data flows (DF-XXX references)

### **Stage 2 Quality Scoring:**

**Methodological Rigor (1-5):**
- **5:** Triple-format equivalency perfect, systematic flow coverage
- **3:** Minor format inconsistencies, generally systematic
- **1:** Missing formats or major content discrepancies

**Analytical Depth (1-5):**
- **5:** Comprehensive data flow coverage, thorough security analysis
- **3:** Adequate flows with some gaps
- **1:** Incomplete flow analysis

**Critical Questions to Challenge:**
1. Is content IDENTICAL across all three DFD formats?
2. Are trust boundary placements justified with security reasoning?
3. Can you explain alternative boundary configurations?
4. Are all component interactions from Stage 1 captured as data flows?
5. Are security considerations specific or generic?

### **Mandatory Challenge Questions (MUST Address ALL)**

**For Stage 2, critic MUST explicitly address:**

1. **Data Integrity Challenge:**
   - Are ANY communication protocols specified without direct source documentation?
   - Could protocol inferences be marked more conservatively?
   - Are there flows where data elements are too vague or generic?
   - Could authentication requirements be stated with less certainty?

2. **Completeness Challenge:**
   - What is the MOST SIGNIFICANT data flow that might be missing?
   - What error/exception flows weren't considered?
   - What administrative or maintenance flows are absent?
   - What data flows occur during system failures?

3. **Methodology Challenge:**
   - Could trust boundaries be placed differently with valid justification?
   - Are there unstated limitations in the DFD representation?
   - Could attack surface mapping be more granular?
   - What implicit assumptions about system behavior are embedded?

4. **Stakeholder Utility Challenge:**
   - Would a security engineer find these DFDs sufficient for threat identification?
   - What flow details are missing that penetration testers would need?
   - Are critical paths clearly enough identified for risk prioritization?
   - Could security considerations be more actionable?

**Failure to address all 4 challenges = Incomplete critic analysis = Automatic rejection**

---

## Stage 3: Threat Identification Validation

### **Validation Objectives:**
- Verify ALL six STRIDE categories per component
- Ensure 60-70% generic implementation-agnostic threats
- Validate MITRE ATT&CK and Kill Chain mappings
- Check threat count appropriate for system complexity
- Confirm no technology-specific threats when tech unknown

### **Critical Validation Checks:**

#### **1. STRIDE Coverage Validation**
**MANDATORY:** ALL six categories per component

**Validation Matrix:**
| Component | Spoofing | Tampering | Repudiation | Info Disclosure | DoS | Elevation |
|-----------|----------|-----------|-------------|-----------------|-----|-----------|
| Component 1 | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] |
| Component 2 | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] | ✓ [N threats] |

**Red Flags:**
- ❌ Any component missing ANY STRIDE category
- ❌ "No applicable threats for this category" without strong justification
- ❌ Uneven distribution suggesting selective coverage

#### **2. Generic vs. Specific Threat Balance**
**Expected Distribution:**
- **60-70%** Generic/Implementation-Agnostic threats
- **20-30%** System-Specific threats (based on documented features)
- **10-20%** Operational/Business Process threats

**Validation:**
- [ ] Count threats by type → Calculate percentages
- [ ] Verify generic threats don't require knowledge of undocumented tech
- [ ] Confirm specific threats reference documented functionality
- [ ] Check operational threats address business processes, not technical

**Red Flags:**
- ❌ 90% system-specific threats when implementation unknown
- ❌ Technology-specific threats ("React Native-specific XSS") when framework undocumented
- ❌ All threats generic with no documented system characteristics used

#### **3. Threat Count Validation**
**Guidelines (Quality Indicators, NOT Requirements):**
- Simple system (3-5 components): Typically 15-25 genuine threats
- Medium system (5-10 components): Typically 25-40 genuine threats
- Complex system (10+ components): Typically 40+ genuine threats

**If Below Typical Range:** Check for:
- Skipped STRIDE categories
- Missing generic threat patterns
- Insufficient threat depth per component

**If Above Typical Range:** Check for:
- Duplicate threats with different wording
- Overly granular threat decomposition
- Fabricated threats to inflate count

**CRITICAL:** Never force artificial threats to meet count guidelines

#### **4. MITRE ATT&CK Mapping Validation**
**Check Each Threat:**
- [ ] ATT&CK technique ID valid (T#### format)
- [ ] Technique appropriate for threat description
- [ ] Tactic aligns with threat category
- [ ] Matrix selection appropriate (Enterprise/Mobile/ICS)

**Red Flags:**
- ❌ All threats mapped to T1190 (Exploit Public-Facing Application)
- ❌ Technique IDs invalid or outdated
- ❌ Mapping doesn't enhance threat understanding
- ❌ Mobile threats using Enterprise ATT&CK

#### **5. Kill Chain Mapping Validation**
**Check Each Threat:**
- [ ] Kill Chain stage(s) appropriate for threat
- [ ] Multi-stage threats identify all relevant stages
- [ ] Attack progression context explains stage selection

**Validate Consistency:**
- Early-stage threats (Reconnaissance, Delivery) should exist
- Not all threats in Stage 7 (Actions on Objectives)
- Multi-stage attack scenarios make logical sense

### **Stage 3 Quality Scoring:**

**Methodological Rigor (1-5):**
- **5:** Perfect STRIDE coverage, systematic ATT&CK/KC mapping
- **3:** Minor STRIDE gaps, generally systematic
- **1:** Missing STRIDE categories, inconsistent framework application

**Analytical Depth (1-5):**
- **5:** Appropriate threat count, excellent generic/specific balance
- **3:** Adequate threats with distribution issues
- **1:** Insufficient threats or poor balance

**Critical Questions to Challenge:**
1. Why is [STRIDE category] missing for [component]?
2. How is this threat feasible without knowing specific technology?
3. Are there generic threats missing for this component type?
4. Does ATT&CK technique accurately describe attack method?
5. Why is this threat in Kill Chain stage [X] and not [Y]?

---

## Stage 4: Risk Assessment Validation

### **Validation Objectives:**
- Ensure CVSS used ONLY when ALL metrics have documentation
- Verify no CVSS for business/policy/organizational threats
- Validate qualitative assessment when data insufficient
- Check no fabricated business impact metrics
- Confirm appropriate confidence levels

### **Critical Validation Checks:**

#### **1. CVSS Application Validation**
**For Each CVSS-Scored Threat:**

**Validate EACH Metric Has Documentation:**
- [ ] **AV (Attack Vector):** Network architecture documented
- [ ] **AC (Attack Complexity):** Security controls documented
- [ ] **PR (Privileges Required):** Authentication requirements documented
- [ ] **UI (User Interaction):** Attack scenario documented
- [ ] **S (Scope):** Trust boundaries documented
- [ ] **C (Confidentiality):** Data classification documented
- [ ] **I (Integrity):** Data modification scope documented
- [ ] **A (Availability):** Service criticality documented

**Red Flags - CVSS Fabrication:**
- ❌ "AV:N assumed because it's a web application"
- ❌ "PR:N assumed as endpoint appears public"
- ❌ "C:H because PII involved" without scope documentation
- ❌ Any metric value marked as "assumed" or "inferred"

**CRITICAL:** If ANY metric cannot be determined from documentation → NO CVSS, use qualitative instead

#### **2. CVSS Applicability Validation**
**CVSS NOT APPLICABLE For:**
- ❌ Business process threats (discriminatory policies)
- ❌ Organizational policy violations (inadequate procedures)
- ❌ Strategic/competitive risks (legal concerns)
- ❌ Regulatory compliance gaps (GDPR violations)
- ❌ Technical threats with insufficient implementation details

**Validation:**
For each non-CVSS threat, verify:
- [ ] Explicit justification why CVSS not applicable
- [ ] Qualitative risk rating provided (CRITICAL/HIGH/MEDIUM/LOW)
- [ ] Business impact components documented
- [ ] Likelihood assessment with reasoning

#### **3. Business Impact Validation**
**CRITICAL PROHIBITION:** No fabricated business metrics

**Check For Fabrication:**
- ❌ "$2.5M financial impact" without source
- ❌ "100,000 affected users" invented
- ❌ "15% revenue impact" calculated without revenue data
- ❌ "$45K - $78K remediation cost" without budget data

**Correct Approaches:**
- ✅ Qualitative impact categories with industry benchmarks
- ✅ "HIGH financial impact based on GDPR Article 83 penalties (up to 4% annual revenue)"
- ✅ "Potential impact: Regulatory penalties, legal costs, reputational damage (specific figures require business data)"

#### **4. Confidence Level Validation**
**Check Each Assessment:**
- [ ] Confidence level explicitly stated
- [ ] Confidence justified with data quality explanation
- [ ] Low confidence assessments acknowledge limitations
- [ ] High confidence has strong documentation basis

**Red Flags:**
- ❌ HIGH confidence with assumption-based CVSS
- ❌ Missing confidence levels
- ❌ Confidence inconsistent with data gaps

### **Stage 4 Quality Scoring:**

**Data Integrity (1-5):**
- **5:** No fabricated business metrics, CVSS only when fully supported
- **3:** Some questionable CVSS metrics, generally sound
- **1:** Fabricated financial data or assumption-based CVSS

**Analytical Depth (1-5):**
- **5:** All threats assessed appropriately, excellent justifications
- **3:** Most threats assessed adequately, some gaps
- **1:** Incomplete or superficial risk assessments

**Critical Questions to Challenge:**
1. What source documentation supports each CVSS metric value?
2. Why is CVSS used for this non-technical threat?
3. Where did this business impact figure come from?
4. What assumptions underlie this risk assessment?
5. Is confidence level appropriate for data quality?

---

## Stage 5: Mitigation Strategy Validation

### **Validation Objectives:**
- Verify controls mapped to specific threats
- Ensure implementation guidance feasible within documented constraints
- Check no fabricated cost estimates
- Validate residual risk analysis present
- Confirm priority alignment with Stage 4

### **Critical Validation Checks:**

#### **1. Threat-to-Control Mapping**
**For Each Threat from Stage 3:**
- [ ] At least one control recommendation
- [ ] Control explicitly references threat ID(s)
- [ ] Control addresses root cause, not just symptoms
- [ ] Multiple controls provide defense-in-depth

**Red Flags:**
- ❌ Threats from Stage 3 with no mitigation controls
- ❌ Controls not mapped to specific threats
- ❌ Vague controls ("improve security") without specifics

#### **2. Implementation Feasibility Validation**
**Check Each Control Against Stage 1/2 Architecture:**
- [ ] Control compatible with documented architecture
- [ ] Integration points identified from documented components
- [ ] No controls requiring undocumented technology
- [ ] Technical requirements realistic

**Red Flags:**
- ❌ "Implement HSMs" when cloud serverless architecture documented
- ❌ "Deploy on-premises firewall" for cloud-native system
- ❌ Technology-specific controls when technology unknown
- ❌ Controls requiring capabilities not documented

#### **3. Cost Estimation Validation**
**CRITICAL PROHIBITION:** No cost fabrication

**Prohibited:**
- ❌ "$45,000 - $78,000 implementation cost"
- ❌ "2 FTE for 3 months"
- ❌ "$15K annual licensing"
- ❌ Any specific dollar amounts or resource figures without budget data

**Acceptable:**
- ✅ Qualitative cost categories (LOW/MEDIUM/HIGH)
- ✅ "Industry benchmarks suggest mid-range investment"
- ✅ "Requires detailed vendor quotes and resource planning"

#### **4. Residual Risk Analysis**
**For Each Control:**
- [ ] Residual risk after implementation stated
- [ ] Effectiveness assessment (Complete/Substantial/Partial/Minimal)
- [ ] Risk acceptance decision documented if residual risk remains HIGH/CRITICAL
- [ ] Limitations of control acknowledged

**Red Flags:**
- ❌ All controls marked "Complete mitigation"
- ❌ No residual risk analysis provided
- ❌ Unrealistic effectiveness claims

#### **5. Priority Alignment Validation**
**Cross-Reference Stage 4 Risk Assessment:**
- [ ] CRITICAL threats have immediate action recommendations
- [ ] HIGH threats in short-term phase (1-3 months)
- [ ] Control priority matches threat priority
- [ ] Quick wins identified and prioritized

**Red Flags:**
- ❌ CRITICAL threats in long-term roadmap
- ❌ LOW threats prioritized over HIGH threats
- ❌ Implementation timeline inconsistent with risk severity

### **Stage 5 Quality Scoring:**

**Data Integrity (1-5):**
- **5:** No cost fabrication, feasible within documented constraints
- **3:** Some questionable feasibility, minor issues
- **1:** Fabricated costs or infeasible recommendations

**Stakeholder Utility (1-5):**
- **5:** Highly actionable, specific implementation guidance
- **3:** Partially actionable, some vague recommendations
- **1:** Not actionable, unclear or impractical guidance

**Critical Questions to Challenge:**
1. Where does this cost estimate come from?
2. How is this control feasible given documented architecture?
3. Why isn't this CRITICAL threat in immediate actions?
4. What's the residual risk after this control?
5. Can an implementation team act on this guidance?

---

## Stage 6: Final Report Validation

### **Primary Skills:** Threat-Modeler (content) + Documentation-Specialist (formatting)
### **Validation Focus:** Completeness, technical accuracy, self-containment

**NOTE:** Quality-critic focuses on TECHNICAL REVIEW - verifying ALL threats included (count matching), identifying inconsistencies across stages, checking for fabricated content. Report formatting/aesthetics are secondary to completeness and accuracy.

### **Validation Objectives:**
- Ensure ALL threats from Stage 3 included in report (CRITICAL - count verification)
- Verify executive summary non-technical and actionable
- Confirm report self-contained and comprehensible
- Validate transparent assumption documentation  
- Check cross-stage consistency (no contradictions)
- Identify any new/fabricated content not in Stage 1-5 outputs

### **Critical Validation Checks:**

#### **1. Threat Inventory Completeness**
**MANDATORY:** ALL threats from Stage 3 must appear in final report

**Validation Process:**
1. Count threats in Stage 3 output file → [N] threats
2. Count threats in Stage 6 Priority-Sorted Inventory → [N] threats (MUST MATCH)
3. Spot-check 10-15 random threat IDs from Stage 3 present in Stage 6
4. Verify threat descriptions consistent between Stage 3 and Stage 6

**Red Flags:**
- ❌ Stage 6 threat count < Stage 3 threat count
- ❌ Missing threat IDs from Stage 3 inventory
- ❌ Only CRITICAL/HIGH threats included (MEDIUM/LOW missing)

#### **2. Executive Summary Validation**
**Check For Non-Technical Language:**
- [ ] No jargon or technical acronyms without explanation
- [ ] Business impact focus, not technical details
- [ ] Actionable for C-level decision-making
- [ ] Key findings summarized in 1-2 pages

**Red Flags:**
- ❌ "CVSS 8.1 SQL injection in /api/users/{id} endpoint"
- ❌ Technical vulnerability details in executive summary
- ❌ Requires technical knowledge to understand

**Correct Style:**
- ✅ "Critical security vulnerabilities could enable unauthorized customer data access"
- ✅ Business consequences emphasized
- ✅ Strategic recommendations, not technical implementations

#### **3. Self-Contained Report Validation**
**Test:** Can executive understand report without reading Stage 1-5 files?

**Check:**
- [ ] Sufficient context provided for each section
- [ ] Threat descriptions include enough detail
- [ ] Architecture explained adequately
- [ ] References to stage files are supplementary, not required

**Red Flags:**
- ❌ "See Stage 3 for details" without providing context
- ❌ Assuming reader has read previous stage outputs
- ❌ Incomplete threat descriptions requiring Stage 3 lookup

#### **4. Cross-Stage Consistency Validation**
**Verify Consistency:**
- [ ] Architecture summary matches Stage 1/2
- [ ] Risk ratings match Stage 4
- [ ] Recommendations align with Stage 5
- [ ] No new threats introduced (all from Stage 3)
- [ ] Assumptions consistent across stages

**Red Flags:**
- ❌ Different risk ratings for same threat
- ❌ Recommendations contradicting Stage 5
- ❌ Architecture discrepancies
- ❌ New assumptions not in Stage 1

#### **5. Limitation Acknowledgment Validation**
**Check Conclusion Section:**
- [ ] Data gaps explicitly documented
- [ ] Analysis limitations acknowledged
- [ ] Confidence levels clearly communicated
- [ ] Recommendations for improving analysis

**Red Flags:**
- ❌ Presenting analysis as definitive when data gaps exist
- ❌ No acknowledgment of assumptions or limitations
- ❌ Overconfident conclusions not supported by data quality

### **Stage 6 Quality Scoring:**

**Methodological Rigor (1-5):**
- **5:** All threats included, perfect cross-stage consistency
- **3:** Minor omissions or inconsistencies
- **1:** Significant threats missing or major inconsistencies

**Stakeholder Utility (1-5):**
- **5:** Highly actionable for all stakeholders, professional presentation
- **3:** Partially actionable, some clarity issues
- **1:** Not actionable, poor presentation quality

**Critical Questions to Challenge:**
1. Are ALL threats from Stage 3 present in the final report?
2. Can a non-technical executive understand and act on this?
3. Is the report comprehensible without reading stage files?
4. Are limitations and assumptions transparently communicated?
5. Is presentation quality professional and polished?

---

## Universal Validation Principles

### **Across All Stages:**

**Always Challenge:**
1. **Fabricated Data:** Any specific technologies, metrics, or costs without sources
2. **Vague Assumptions:** General statements without specific confidence levels
3. **Methodological Gaps:** Skipped framework elements (STRIDE categories, etc.)
4. **Alternative Interpretations:** Could documented evidence support different conclusions?
5. **Stakeholder Utility:** Would executives/technical teams find this actionable?

**Always Verify:**
1. **Source Traceability:** Can claims be traced to specific documentation?
2. **Confidence Calibration:** Do confidence levels match data quality?
3. **Systematic Coverage:** Are frameworks applied consistently?
4. **Cross-Stage Consistency:** Are stages aligned and coherent?
5. **Data Integrity:** Are all metrics and claims evidence-based?
6. **Clarifying Questions Documentation (Collaborative Mode Only):**
   - Does `{stage-number}_clarifying_questions.md` file exist if questions were asked?
   - Are all user clarifications cross-referenced in main output file?
   - Format: `*Source: User clarification (see Question [N] in {stage-number}_clarifying_questions.md)*`
   - Are questions logged with context, response, and usage documentation?

---

**REMINDER: When modifying this validation guide, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

