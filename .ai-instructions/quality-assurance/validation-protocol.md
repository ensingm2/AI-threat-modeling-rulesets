# Quality Validation Protocol | Load: Critic Phase | ~2,000 tokens | Prereq: core-principles.md

---

## EVIDENCE-BASED QUALITY VALIDATION PROTOCOL

### **Phase 1: Analytical Capability Demonstration (ALL REQUIRED)**

#### **Mandatory Critic Problem-Seeking Requirements**

**Required Flaw Identification (Critic Must Find Real Issues):**
- □ **Technical Fabrication Detection**: Identify specific technology claims (frameworks, databases, languages) without source documentation support
- □ **Architecture Detail Hallucinations**: Find invented system details (API patterns, schemas, deployment patterns) not documented in source materials  
- □ **Source Documentation Gaps**: Identify claims lacking adequate source documentation support with specific quote requirements
- □ **Assumption Vulnerabilities**: Challenge assumptions that could invalidate conclusions if incorrect, especially technical architecture assumptions
- □ **Methodological Inconsistencies**: Find gaps in framework application or logical inconsistencies
- □ **Analytical Depth Problems**: Identify areas with insufficient analysis depth or missing perspectives
- □ **Stakeholder Utility Gaps**: Find outputs that lack actionability or decision-making support
- □ **Evidence Quality Issues**: Identify weak evidence basis or inappropriate confidence claims
- □ **Alternative Interpretation Gaps**: Find areas where alternative explanations weren't considered

---

### **MANDATORY STAGE-SPECIFIC VALIDATIONS**

#### **STAGE 1 & General - Technical Fabrication Validation:**

**Critic Must Verify Every Technical Claim:**
- **Technology Stack Claims**: Demand source quotes for any specific framework, language, or platform mentions
- **Architecture Details**: Challenge any database, API, or deployment pattern claims not explicitly documented
- **Implementation Specifics**: Flag recommendations requiring technology details not provided in source materials
- **System Characteristics**: Verify all performance, capacity, and technical capability claims against documentation

#### **STAGE 2 ONLY - DFD Format Validation:**

**Critic Must Verify All Three DFD Output Formats:**
- **Content Equivalency**: Verify Text/Markdown, Mermaid, and Draw.io XML formats contain IDENTICAL data flows with NO missing components
- **Format Completeness**: Each format must represent complete system analysis with same trust boundaries, data elements, security considerations
- **Technical Syntax**: Verify Mermaid syntax renders correctly, Draw.io XML structure is valid and importable
- **Cross-Format Consistency**: Count data flows, components, and trust boundaries across all formats - must match exactly
- **Missing Element Detection**: Actively search for any data flows, components, or security considerations present in one format but missing in others

#### **STAGE 3 ONLY - Threat Identification Completeness:**

**Critic Must Verify Comprehensive Generic Threat Coverage:**
- **STRIDE Completeness**: Each system component must have threats identified for ALL six STRIDE categories
- **Generic Technical Threats**: Mobile apps, APIs, IoT devices, cloud services must have implementation-agnostic threats
- **Threat Count Validation**: Simple systems (3-5 components) commonly range from 15-25 threats, medium systems (5-10 components) commonly range from 25-40 threats, complex systems (10+ components) commonly range from 40+ threats - these are guidance ranges, not minimum requirements
- **Technical vs. Business Balance**: 60-70% generic technical threats, not predominantly business process threats
- **Component Coverage**: Every identified system component must have corresponding technical threat analysis

#### **STAGE 4 ONLY - CVSS Scoring Validation:**

**Critic Must Verify Appropriate CVSS Usage:**
- **Omission Over Assumption Principle**: Confirm agent OMITTED CVSS scoring when technical details insufficient, rather than making assumptions to force a score
- **Technical Data Sufficiency**: CVSS scores only applied when ALL base metrics (AV, AC, PR, UI, S, C, I, A) can be determined from source documentation WITHOUT assumptions or guesses
- **Assumption Detection**: Flag ANY CVSS score containing metric values derived from assumptions rather than documented facts (e.g., "assuming network-accessible", "assuming no security controls")
- **Threat Type Appropriateness**: CVSS NOT applied to business process threats, organizational policy violations, strategic risks, or regulatory compliance gaps without technical exploitation vectors
- **Component Justification**: Every CVSS metric must reference specific documented system characteristics from source materials with direct quotes
- **Alternative Scoring Validation**: Non-technical threats AND technical threats with insufficient documentation must use qualitative risk categories (CRITICAL/HIGH/MEDIUM/LOW) with explicit justification
- **Data Gap Documentation**: When technical details insufficient for CVSS, must explicitly document missing data required for each unavailable metric
- **Mixed Threat Validation**: Ensure threats with both technical and business dimensions receive appropriate dual assessment (CVSS for technical + qualitative for business impact), but ONLY if technical CVSS can be determined without assumptions
- **Prohibited Assumptions Examples**: Flag scores assuming network exposure, security control absence, privilege requirements, data classification, or architectural patterns not documented

#### **STAGE 6 ONLY - Comprehensive Final Report Validation:**

**Critic Must Verify Complete Report Structure and Content:**

**For complete Stage 6 requirements, see:** `../threat-modeling/stage-6-final-report-requirements.md`

- **7-Section Structure**: Executive Summary, Service Overview, Architecture Summary (with DFD), Major Assumptions, Priority-Sorted Threats, Recommendations, Conclusion
- **Threat Inventory Completeness**: ALL threats documented in Stage 3 output file (03-threat-identification.md) must appear in priority-sorted list with risk ratings and mitigation summaries
- **Cross-Stage Consistency**: Information consolidated from previous stages must be accurate with no contradictions or omissions
- **Self-Contained Validation**: Report must be comprehensible as standalone document without requiring reference to stage outputs
- **Executive Quality**: Professional formatting, appropriate detail level, executive-actionable language and recommendations
- **Visual Integration**: Data Flow Diagram properly integrated and rendering correctly in architecture section
- **Assumption Documentation**: Major assumptions clearly identified with proper references to complete assumption lists in stage outputs

---

### **Critic Performance Standards**

**Minimum Issues Required:** Must identify at least 2-3 legitimate analytical problems per stage (more than 3 is acceptable and encouraged), UNLESS the work demonstrably meets all quality standards after thorough critical analysis, in which case explicit justification is required explaining why fewer issues exist

**Problem Specificity:** Issues must be specific, actionable, and require meaningful rework  
**Alternative Thinking:** Must propose alternative interpretations or approaches for key decisions  
**Quality Justification:** Must explain why identified issues represent genuine quality concerns

#### **Exception Criteria for Fewer Than 2-3 Issues:**

Critic may identify fewer than 2-3 issues ONLY when ALL of the following are demonstrated:

**1. Comprehensive Review Performed:**
- Explicitly addressed each quality dimension (Data Integrity, Methodological Rigor, Source Traceability, Analytical Depth, Stakeholder Utility)
- Checked all stage-specific requirements systematically (e.g., for Stage 3: verified STRIDE coverage, ATT&CK mapping, Kill Chain analysis)
- Verified source documentation for random sample of claims (minimum 3-5 spot checks with specific examples)

**2. Active Challenge Attempted:**
- Document at least 3 major assumptions challenged with alternative interpretations
- Explain why alternatives were ultimately not superior to worker's approach
- Example: "Challenged assumption that API uses JWT tokens - considered session cookies alternative, but JWT approach consistent with documented stateless design"

**3. Explicit Quality Confirmation:**
- State specific examples demonstrating each quality dimension meets standards
- Provide objective evidence using quantifiable metrics:
  - Data Integrity: "All 23 threats have source references; no fabricated business metrics detected"
  - Methodological Rigor: "STRIDE coverage verified across all 6 major components; consistent risk rating approach"
  - Source Traceability: "Spot-checked 5 technical claims - all trace to specific documentation sections with quotes"
  - Analytical Depth: "15 assumptions documented with confidence levels; 8 data gaps explicitly acknowledged"
  - Stakeholder Utility: "Mitigation strategies include specific controls, implementation guidance, and cost estimates"

**4. Justification for Fewer Issues:**
- Explicit statement: "Only [N] issues identified because [specific quality evidence demonstrating exceptional work]"
- Must include objective metrics supporting quality claim
- Example: "Only 1 issue identified (minor formatting inconsistency) because work demonstrates: 28 threats with comprehensive STRIDE coverage, all source-documented, systematic ATT&CK mapping for each threat, and clear business impact justification"

---

### **Multi-Dimensional Quality Scoring**

#### **Quality Dimension Assessment (Each Scored 1-5):**
- **Data Integrity**: No fabricated claims, appropriate uncertainty handling
- **Methodological Rigor**: Systematic framework application, consistency across components  
- **Source Traceability**: Claims properly documented and referenced to source materials
- **Analytical Depth**: Appropriate scope coverage, assumption identification and handling
- **Stakeholder Utility**: Actionable outputs, appropriate detail level for decision-making

#### **Progression Criteria:**
- **All dimensions ≥4**: Immediate approval, proceed to next stage
- **Any dimension ≤2**: Major revision required with specific guidance
- **Dimensions 3-4 mix**: Conditional approval with targeted improvements

---

### **Adversarial Question Framework**

#### **Mandatory Adversarial Validation Questions (Critic Must Answer):**
1. **"What would a security expert challenge about this methodology application?"**
2. **"What critical information gaps could change the conclusions?"**
3. **"Which assumptions, if incorrect, would invalidate major findings?"**  
4. **"How would executives evaluate the actionability of these recommendations?"**
5. **"What would an auditor question about the evidence basis for key claims?"**

#### **Validation Logic:**
Quality of adversarial analysis demonstrates thorough review without artificial problem generation.

---

### **Phase 2: Multi-Perspective Validation**

#### **Simulated Expert Review Perspectives**

**Required Perspective Validations:**
- **Security Architect Perspective**: "Does this analysis support secure system design decisions?"
- **CISO Perspective**: "Are risk assessments actionable for business decision-making?"
- **Incident Responder Perspective**: "Would this intelligence be useful during actual security incidents?"
- **Auditor Perspective**: "Is the methodology application defensible and well-documented?"
- **Implementation Perspective**: "Are security recommendations technically feasible and specific?"

**Approval Logic:** Work approved if it satisfies majority of expert perspectives with documented reasoning.

#### **Context-Aware Quality Standards**

**Dynamic Quality Thresholds Based on Project Stakes:**

**High-Stakes Projects** (regulatory compliance, critical infrastructure):
- All quality dimensions must score ≥4
- Extensive source validation and conservative uncertainty handling required

**Standard Projects** (internal risk assessment, operational planning):  
- Quality dimensions average ≥3.5 with no dimension <3
- Moderate validation with balanced uncertainty acknowledgment

**Exploratory Projects** (research, proof-of-concept, training):
- Quality dimensions average ≥3.0 focusing on methodological learning
- Emphasis on educational value and process improvement

---

### **Phase 3: Data Integrity and Precision Validation**

#### **Enhanced Anti-Fabrication Controls**

**AUTOMATIC QUALITY FAILURES (IMMEDIATE REJECTION):**
- **Technical Stack Fabrication**: Specific technology claims (React Native, Node.js, PostgreSQL) without source documentation
- **Architecture Details Invention**: Database schemas, API patterns, cloud providers not specified in source materials
- **Quantitative Business Claims**: Financial data, user metrics, transaction volumes without documented basis
- **Precise Technical Metrics**: Response times, capacity numbers, availability percentages not supported by documentation  
- **Regulatory Status Assumptions**: Compliance requirements or penalty amounts without legal precedent sources
- **Operational Scale Fabrication**: Fleet sizes, geographic scope, deployment scale without source specification

#### **MANDATORY TECHNICAL CLAIM VALIDATION CHECKLIST:**
- □ **Every technology mentioned has source documentation reference or explicit "ASSUMPTION" marking**
- □ **No specific frameworks/languages claimed without direct source quotes**
- □ **All architecture details either documented or marked as "typical patterns - actual implementation unknown"**
- □ **Technical recommendations generic enough to apply across technology variations**
- □ **Implementation guidance includes technology specification requirements for detailed controls**

#### **SOURCE TRACEABILITY REQUIREMENTS:**
- **Direct Quote Requirement**: All technical claims must include exact text from source documentation
- **Reference Specificity**: Document name, section, and line references for all factual assertions
- **Assumption Flagging**: Clear visual marking (⚠️ ASSUMPTION) for any inferred technical details
- **Confidence Calibration**: Explicit confidence levels for all technical architectural claims

#### **ENHANCED UNCERTAINTY DOCUMENTATION:**
- **HIGH CONFIDENCE**: Direct source documentation with specific quotes and references
- **MEDIUM CONFIDENCE**: Reasonable inference with documented assumptions, limitations, and alternative possibilities
- **LOW CONFIDENCE**: Industry patterns with explicit external source notation and significant uncertainty acknowledgment
- **INSUFFICIENT DATA**: Explicit gap acknowledgment with qualitative assessment approach and specification requirements

---

## Related Resources

**Load for specific needs:**
- **`approval-criteria.md`** - Graduated approval system and progression criteria
- **`critic-review-template.md`** - Structured template for critic responses
- **`examples/fabrication-detection.md`** - Examples of catching fabricated data
- **`examples/cvss-validation.md`** - Examples of proper CVSS validation (Stage 4 only)
- **`examples/mode-specific-processes.md`** - Collaborative vs Automatic mode examples

---

**This protocol provides the core validation procedures. Load approval-criteria.md for decision-making framework.**

