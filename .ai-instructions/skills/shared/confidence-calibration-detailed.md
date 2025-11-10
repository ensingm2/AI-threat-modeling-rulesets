# Confidence Calibration Framework

**Purpose:** Standardized confidence level definitions and application guidelines  
**Scope:** All threat modeling analyses and assessments requiring uncertainty quantification  

---

## Confidence Level Definitions

### **HIGH CONFIDENCE (85-95%, inclusive)**

**Criteria:**
- Direct source documentation available with specific references
- Technical claims validated with explicit documentation quotes
- Minimal inference required beyond documented facts
- Alternative interpretations considered and reasonably excluded

**Example Applications:**
- System component identification explicitly listed in architecture documentation
- Technology stack specified with version numbers in source materials
- Data flows documented with protocols and data elements specified
- Security controls explicitly described in design documents

**Documentation Format:**
```markdown
**Component:** Authentication Service
**Source:** "Authentication is handled by Auth0 OAuth 2.0 implementation" (architecture.md, line 123)
**Confidence Level:** HIGH (95%) - Directly documented with specific technology and protocol
```

### **MEDIUM CONFIDENCE (70% to <85%)**

**Criteria:**
- Reasonable inferences based on partial documentation
- Assumptions documented with clear justification
- Alternative interpretations identified and evaluated
- Supporting evidence from multiple sources or contexts

**Example Applications:**
- Technology stack inferred from partial clues (e.g., "npm packages" suggests Node.js)
- Trust boundaries derived from documented component interactions
- Data sensitivity classification based on documented regulatory requirements
- Attack complexity assessment based on typical implementation patterns

**Documentation Format:**
```markdown
**Component:** Backend API
**Source:** Documentation mentions "npm packages" and "JavaScript linting" (contributing.md, line 45)
**Inference:** Likely Node.js-based backend implementation
**Confidence Level:** MEDIUM (75%) - Reasonable inference from development tooling references
**Alternative Possibilities:** Could be browser-side JavaScript only; backend technology not conclusively proven
**Impact if Incorrect:** Server-side Node.js-specific vulnerabilities may not apply
```

### **LOW CONFIDENCE (50% to <70%)**

**Criteria:**
- Industry pattern analysis without system-specific documentation
- Significant assumptions required for assessment
- Limited source documentation supporting claim
- Multiple alternative interpretations equally plausible

**Example Applications:**
- Generic technology threats when implementation unknown
- Business impact categories without financial data
- Risk likelihood based on industry statistics rather than system specifics
- Mitigation effectiveness estimates based on general security research

**Documentation Format:**
```markdown
**Threat:** SQL Injection vulnerabilities
**Basis:** Industry pattern - web applications commonly use SQL databases
**Source:** No database technology specified in documentation
**Confidence Level:** LOW (60%) - Generic threat applicable IF SQL database used
**Alternative Possibilities:** May use NoSQL, ORM with parameterized queries, or no database
**Impact if Incorrect:** Specific SQL injection mitigations may not apply; NoSQL injection threats may be relevant instead
**Recommendation:** Confirm database technology and query construction methods for targeted threat analysis
```

### **INSUFFICIENT CONFIDENCE (<50%)**

**Criteria:**
- Inadequate data for defensible assessment
- Speculation would be required to reach conclusion
- No reasonable inference path from available documentation
- Explicit data gap preventing analysis

**Example Applications:**
- Technical architecture details completely undocumented
- Business impact quantification with no financial or operational data
- CVSS scoring with unknown attack vector or privilege requirements
- Mitigation feasibility when technical constraints unknown

**Documentation Format:**
```markdown
**Assessment:** Authentication mechanism security analysis
**Data Gap:** Authentication implementation not documented in source materials
**Confidence Level:** INSUFFICIENT (<50%) - Cannot analyze authentication security without implementation details
**Qualitative Assessment:** Authentication is critical security component requiring verification
**Required Information:**
- Authentication protocol (OAuth, SAML, custom)
- Credential storage mechanism
- Session management approach
- Multi-factor authentication implementation
**Recommendation:** Obtain authentication architecture documentation before detailed security analysis
```

## Confidence Application Guidelines

### **Technical Assessments**

**HIGH Confidence Required For:**
- Specific technology stack claims (frameworks, languages, platforms)
- Database schema or API pattern descriptions
- Network architecture and communication protocols
- Security control specifications (encryption algorithms, authentication methods)

**MEDIUM Confidence Acceptable For:**
- Trust boundary placements based on documented component interactions
- Data sensitivity classification derived from regulatory requirements
- Generic threat identification applicable across technology variations
- Control effectiveness estimates based on security research

**LOW Confidence Acceptable For:**
- Industry-standard threat patterns when implementation unknown
- Generic mitigation recommendations applicable broadly
- Threat likelihood based on attack statistics rather than system specifics
- Order-of-magnitude impact estimates using industry benchmarks

**INSUFFICIENT Data Requires:**
- Explicit data gap documentation
- Qualitative assessment approach instead of quantitative
- Recommendations for obtaining missing information
- Clear statement of analysis limitations

### **Business Impact Analysis**

**HIGH Confidence Required For:**
- Quantitative financial impact calculations (requires documented revenue, cost data)
- Specific regulatory penalty amounts (requires legal precedent sources)
- Customer count or transaction volume impacts (requires documented metrics)

**MEDIUM Confidence Acceptable For:**
- Qualitative impact categories (HIGH/MEDIUM/LOW) with justification
- Industry-standard impact estimates based on similar organizations
- Regulatory violation identification (without specific penalty amounts)

**LOW Confidence Acceptable For:**
- Order-of-magnitude estimates using public industry data
- Comparative assessments ("likely more impactful than...")
- Sensitivity analysis with multiple scenarios

**INSUFFICIENT Data Requires:**
- Qualitative risk categories only
- Explicit acknowledgment: "Financial impact cannot be quantified - no business data available"
- Recommendations for business context gathering

### **Risk Prioritization**

**Confidence Impact on Prioritization:**
- **HIGH confidence threats:** Prioritize based on documented risk factors
- **MEDIUM confidence threats:** Prioritize conservatively, noting uncertainty
- **LOW confidence threats:** Flag as requiring validation before major investment
- **INSUFFICIENT data threats:** Document as requiring further investigation

**Risk Communication Format:**
```markdown
**Threat:** T015 - Privilege Escalation via API
**CVSS:** 8.1 (HIGH)
**Confidence in Assessment:** MEDIUM (75%)
**Rationale:** API architecture documented, but specific authorization implementation unknown
**Impact of Uncertainty:** Actual exploitability may be higher or lower depending on authorization framework
**Prioritization Recommendation:** Treat as HIGH priority given documented API surface, but validate authorization implementation before finalizing remediation approach
```

## Anti-Fabrication Controls

### **CRITICAL PROHIBITION: NEVER Fabricate to Increase Confidence**

**Prohibited Actions:**
- ❌ Inventing technical details to justify HIGH confidence
- ❌ Assuming specific technologies to enable quantitative assessment
- ❌ Fabricating business metrics to calculate financial impact
- ❌ Creating precise numbers when only ranges or categories appropriate

**Required Actions:**
- ✅ Use lower confidence level appropriate to available data
- ✅ Document data gaps explicitly
- ✅ Provide qualitative assessment when quantitative infeasible
- ✅ Recommend information gathering to improve confidence

### **Confidence Inflation Red Flags**

**Critic Must Challenge:**
- HIGH confidence claims without specific source quotes
- Quantitative assessments (CVSS, financial impact) with MEDIUM or lower confidence
- Precise technical descriptions (specific frameworks, versions) without documentation
- Business metrics (user counts, revenue) with confidence level below HIGH

## Confidence-Driven Quality Standards

### **Stage 1-2: System Understanding & Data Flow**
- **Component identification:** HIGH confidence required (or explicit ASSUMPTION marking)
- **Trust boundaries:** MEDIUM confidence acceptable with clear justification
- **Data flows:** HIGH confidence for documented flows, MEDIUM for inferred

### **Stage 3: Threat Identification**
- **Generic technical threats:** LOW confidence acceptable (implementation-agnostic)
- **System-specific threats:** MEDIUM confidence minimum (requires documented functionality)
- **Attack scenarios:** MEDIUM confidence for feasibility assessment

### **Stage 4: Risk Assessment**
- **CVSS scoring:** HIGH confidence in ALL base metrics required (otherwise use qualitative)
- **Business impact:** HIGH confidence for quantitative, MEDIUM for qualitative
- **Likelihood:** MEDIUM confidence acceptable with documented reasoning

### **Stage 5: Mitigation Strategy**
- **Control recommendations:** MEDIUM confidence minimum (must be technically feasible)
- **Implementation guidance:** Confidence varies - generic (LOW) to specific (HIGH required)
- **Cost estimates:** HIGH confidence required or omit entirely

### **Stage 6: Final Report**
- **Executive summary:** Clearly communicate overall analysis confidence
- **Recommendations:** Flag low-confidence items requiring further investigation
- **Limitations:** Explicitly document confidence constraints on conclusions

## Calibration Validation

### **Critic Responsibilities:**

**Verify Confidence Levels:**
- Check that HIGH confidence claims have specific source documentation
- Ensure MEDIUM confidence claims have documented assumptions and alternatives
- Validate that LOW confidence items acknowledge limitations
- Confirm INSUFFICIENT data gaps explicitly documented

**Challenge Under-Calibrated Confidence:**
- HIGH confidence without adequate source support → Should be MEDIUM or LOW
- Quantitative assessments with LOW confidence → Should use qualitative approach
- Missing uncertainty acknowledgment → Confidence level likely too high

**Challenge Over-Calibrated Conservatism:**
- LOW confidence when direct documentation available → Should be HIGH
- INSUFFICIENT marking when reasonable inferences possible → Should be MEDIUM or LOW
- Excessive hedging undermining stakeholder utility → Balance caution with usefulness

## Documentation Templates

### **Technical Claim Template:**
```markdown
**Claim:** [Technical assertion]
**Source:** "[Direct quote]" ([file], line [number])
**Confidence:** [HIGH/MEDIUM/LOW/INSUFFICIENT] ([percentage])
**Justification:** [Why this confidence level appropriate]
[If MEDIUM or LOW: **Alternatives:** [Other possibilities]]
[If MEDIUM or LOW: **Impact if Incorrect:** [Consequences of wrong assumption]]
```

### **Assessment Template:**
```markdown
**Assessment:** [Risk rating, impact estimate, or other judgment]
**Confidence:** [HIGH/MEDIUM/LOW/INSUFFICIENT] ([percentage])
**Basis:** [Evidence supporting assessment]
**Limitations:** [Factors constraining confidence]
[If <HIGH: **Required for Higher Confidence:** [Missing information]]
```

---

**REMINDER: When modifying this framework, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

