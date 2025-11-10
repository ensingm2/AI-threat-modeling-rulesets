# Documentation Specialist: Stage 1 Guide | Output: 01-system-understanding.md

---

## ⚠️ STOP: Prerequisite Check - Operational Mode Selection

**BEFORE proceeding with Stage 1 work, verify:**

- [ ] **User has been asked which operational mode to use** (Collaborative or Automatic)
- [ ] **Mode file has been loaded** (`.ai-instructions/modes/collaborative-mode.md` OR `.ai-instructions/modes/automatic-mode.md`)
- [ ] **Mode selection has been confirmed**

**If ANY checkbox above is unchecked:**
1. **STOP Stage 1 work immediately**
2. **Go back and ask user for mode selection**
3. **Load the selected mode file**
4. **THEN return here to begin Stage 1**

**This is a hard gate - NO Stage 1 work without mode selection.**

---

## ⚠️ CRITICAL: Batched Execution Requirement

**THIS RESPONSE MUST CONTAIN ONLY THE STAGE 1 WORK PHASE**

**MANDATORY PATTERN:**
1. Complete Stage 1 analysis (all steps below)
2. Create and save `01-system-understanding.md` (see incremental building below)
3. **END THIS RESPONSE** with completion signal
4. **DO NOT proceed to critic phase in same response**

**Completion Signal Format:**
```
✅ STAGE 1 WORK PHASE COMPLETE
- Output File: 01-system-understanding.md
- Location: [target]/output/threat-model/
- Status: Ready for critic review
- Next Batch: Stage 1 Critic Phase
```

**PROHIBITED IN THIS RESPONSE:**
- ❌ Performing critic analysis
- ❌ Validating your own work
- ❌ Proceeding to Stage 2
- ❌ Combining work + validation phases

**The critic phase will happen in the NEXT batch (separate response).**

---

## ⚠️ CRITICAL: Incremental File Building to Avoid Length Limits

**PROBLEM:** Stage 1 output files can be large (10,000+ lines) and exceed tool parameter limits if created in a single `write` tool call.

**SOLUTION: Build the file incrementally using multiple tool calls**

### **Incremental Building Pattern:**

```
Step 1: Create file with header + Table of Contents
  → Use write tool to create initial structure

Step 2-N: Add each major section sequentially
  → Use search_replace to append each section
  → Append to end of file using known anchor point

Final: Verify file completeness
  → Read back sections to confirm all content present
```

### **Example Implementation:**

**Step 1 - Create Initial Structure:**
```markdown
Use write tool to create:
# Stage 1: System Understanding & Scoping
[Header info]

## Table of Contents
[TOC entries]

## 1. Executive Summary
[Placeholder - will add next]

---
END_OF_FILE
```

**Step 2 - Add Executive Summary:**
```markdown
Use search_replace:
OLD: "## 1. Executive Summary\n[Placeholder - will add next]\n\n---\nEND_OF_FILE"
NEW: "## 1. Executive Summary\n[Full content]\n\n## 2. Source Documentation Inventory\n[Placeholder]\n\n---\nEND_OF_FILE"
```

**Step 3-N - Continue Pattern:**
- Each search_replace adds one major section
- Always replace from current placeholder to END_OF_FILE marker
- Maintain END_OF_FILE marker at bottom
- Each addition is < 5000 lines to avoid tool limits

**Final Step - Remove Marker:**
```markdown
Use search_replace to remove:
OLD: "---\nEND_OF_FILE"
NEW: "" (empty string)
```

### **Sections to Build Incrementally:**

**For Stage 1, build in this order:**
1. Header + TOC (write tool)
2. Executive Summary (search_replace)
3. Source Documentation Inventory (search_replace)
4. System Description (search_replace)
5. Component Inventory (search_replace - may need multiple additions if many components)
6. Trust Boundaries (search_replace)
7. Data Asset Catalog (search_replace)
8. Analysis Scope (search_replace)
9. Assumptions & Constraints (search_replace)
10. Documentation Gaps (search_replace)
11. Confidence Assessment + References (search_replace)
12. Remove END_OF_FILE marker (search_replace)

### **Benefits:**
- ✅ Avoids tool parameter length limits
- ✅ Each tool call succeeds independently
- ✅ Progress saved incrementally (crash recovery)
- ✅ Can verify each section as added
- ✅ Easy to debug if one section fails

### **When to Use Incremental Building:**
- **ALWAYS for Stage 1** (large component inventories)
- **ALWAYS for Stage 3** (many threats)
- **ALWAYS for Stage 6** (comprehensive report)
- **Optional for Stage 2, 4, 5** (typically smaller, but use if needed)

---

## Stage 1 Purpose

As the lead documentation specialist for Stage 1, your primary responsibility is **information extraction and organization** from source documentation. You are NOT performing security analysis - that comes later with the threat-modeler.

**Your Mission:**
- Read and comprehend all provided documentation
- Extract factual architectural information
- Organize information systematically
- Document what is known vs. unknown
- Create professional, well-structured output

**⚠️ COLLABORATIVE MODE CRITICAL REQUIREMENT:**
- **In Collaborative Mode, ALWAYS ask user for clarification BEFORE making assumptions**
- **NEVER proceed with assumptions, estimations, or inferences without first checking if user has additional context**
- **This applies to:**
  - Technology details not explicitly documented
  - Security controls not specified
  - Architecture patterns inferred from partial information
  - Scope boundaries where documentation is ambiguous
  - Any inference about system characteristics
- **Process:** Identify gap → Ask user → If user has no context → THEN document as assumption
- **See:** `.ai-instructions/modes/collaborative-mode.md` for complete clarifying question protocol

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `documentation-specialist/role-reminder.md` - Your role definition (worker mode, no fabrication)
- `documentation-specialist/stage-1-guide.md` - This file
- `shared/core-terms.md` - Component, Trust Boundary, Attack Surface definitions
- `shared/confidence-calibration.md` - HIGH/MEDIUM/LOW/INSUFFICIENT confidence levels
- `shared/output-file-requirements.md` - Output format specifications

### **OPTIONAL Files (Load if Needed):**
- `.ai-instructions/modes/collaborative-mode.md` or `.ai-instructions/modes/automatic-mode.md` - If operational guidance needed

### **NOT NEEDED (Can Unload/Skip):**
- Threat-modeler files (security analysis comes in Stage 3+)
- Framework files (STRIDE, ATT&CK, Kill Chain not needed yet)
- Stage 2+ documentation-specialist guides (focus only on Stage 1)

### **Inputs from Previous Stages:**
- None (this is Stage 1)

### **Outputs for Next Stages:**
- `01-system-understanding.md` - Will be used by Stages 2-6

---

## Step-by-Step Workflow

### **Step 1: Initial Documentation Survey**

**Action:** Quickly scan all provided files to understand scope and content types

**Look For:**
- README files (high-level overview)
- Architecture documentation (system design)
- API specifications (interfaces and data)
- Code comments or inline documentation
- Configuration files (deployment hints)
- User guides (functionality description)

**Document Your Survey:**
```markdown
## Source Documentation Inventory
**Total Files Provided:** [N] files
**File Types:**
- [N] README/overview files
- [N] architecture/design documents
- [N] API specifications
- [N] code files with documentation
- [N] configuration files
- [N] other documentation

**Documentation Quality Assessment:**
- Comprehensive architectural documentation: [YES/NO/PARTIAL]
- Technical specifications available: [YES/NO/PARTIAL]
- Business context provided: [YES/NO/PARTIAL]
```

---

### **Step 2: System Description Extraction**

**Action:** Read documentation to understand business purpose and functionality

**Extract:**
- **Business Purpose:** What problem does this system solve?
- **Primary Users:** Who uses the system?
- **Key Functionality:** What are the main features?
- **Operational Context:** How/where does it operate?

**Documentation Pattern:**
```markdown
## System Description

### Business Purpose
**Description:** [What the system does and why it exists]
**Source:** "[Direct quote]" ([filename], line [number])
**Confidence:** HIGH - Explicitly documented

### Primary Users
**User Type 1:** [Description]
- **Source:** "[Quote]" ([filename], line [number])

**User Type 2:** [Description]  
- **Source:** "[Quote]" ([filename], line [number])

### Key Functionality
1. **[Feature 1]:** [Description]
   - **Source:** "[Quote]" ([filename], line [number])

2. **[Feature 2]:** [Description]
   - **Source:** "[Quote]" ([filename], line [number])
```

**CRITICAL:** Every statement must have a source reference!

---

### **Step 3: Component Inventory Creation**

**Action:** Identify ALL system components mentioned in documentation

**Component Types to Look For:**
- User-facing interfaces (web apps, mobile apps, CLIs)
- Backend services and APIs
- Databases and data stores
- Authentication/authorization services
- External integrations (payment processors, APIs, cloud services)
- Infrastructure components (load balancers, message queues)
- IoT devices or embedded systems

**For Each Component Document:**

```markdown
### Component: [Component Name]
**Type:** [Application/Database/API/Service/Device/External Integration]
**Primary Function:** [What this component does]
**Source:** "[Direct quote describing this component]" ([filename], lines [X-Y])

#### Technology Stack
- **Documented:** [ONLY explicitly mentioned technologies]
  - Example: "Uses PostgreSQL database" (config.yaml, line 23)
- **Inferred:** [Reasonable inferences with clear basis]
  - Example: "Likely Node.js based on package.json presence"
  - **Basis:** package.json file exists with npm dependencies
  - **Confidence:** MEDIUM
- **Unknown:** [Technology categories not specified]
  - Example: Backend programming language not documented

#### Data Handled
- **Data Type 1:** [Description from documentation]
  - **Source:** "[Quote]" ([filename], line [number])
- **Data Type 2:** [Description from documentation]
  - **Source:** "[Quote]" ([filename], line [number])

#### Interactions (Preliminary)
[Note: Detailed data flows in Stage 2]
- Interacts with: [List other components mentioned]
- **Source:** "[Quote showing interaction]" ([filename], line [number])

**Confidence Assessment:**
- **Component Existence:** HIGH - Explicitly documented
- **Technology Details:** [HIGH/MEDIUM/LOW/INSUFFICIENT] - [Justification]
- **Functionality Understanding:** [HIGH/MEDIUM/LOW/INSUFFICIENT] - [Justification]
```

**Common Pitfalls to Avoid:**

❌ **WRONG:**
```markdown
### Backend API
**Technology:** Node.js with Express framework
**Database:** MongoDB with Redis caching
```

✅ **CORRECT:**
```markdown
### Backend API
**Technology:**
- **Documented:** API endpoints specified in swagger.yaml
- **Inferred:** None - implementation technology not documented
- **Unknown:** Programming language, framework, database technology

**Confidence:** MEDIUM - API functionality documented, implementation unknown
**Analysis Approach:** Will apply generic API security controls in later stages
```

---

### **Step 4: Trust Boundary Identification**

**Action:** Identify boundaries where trust level changes

**Trust Boundary Types:**
1. **Network Boundaries:** Internet ↔ DMZ ↔ Internal Network
2. **Process Boundaries:** Different application execution contexts
3. **Privilege Boundaries:** User ↔ Admin, Authenticated ↔ Unauthenticated
4. **Organizational Boundaries:** Internal Systems ↔ Third-Party Services

**How to Identify From Documentation:**
- Look for authentication/authorization mentions
- Network topology descriptions
- User role descriptions
- External service integrations
- Data sensitivity classifications

**Documentation Pattern:**
```markdown
### Trust Boundary: [Boundary Name]
**Type:** [Network/Process/Privilege/Organizational]
**Separates:** [Component/Zone A] ↔ [Component/Zone B]

**Identification Basis:**
**Source:** "[Quote indicating this boundary]" ([filename], line [number])
**Confidence:** [HIGH/MEDIUM/LOW] - [Justification]

**Security Implications:**
- **Authentication Required:** [YES/NO/UNKNOWN]
  - **Source:** [Reference if documented]
- **Data Validation Required:** [YES/NO/UNKNOWN]
  - **Source:** [Reference if documented]
- **Encryption Required:** [YES/NO/UNKNOWN]
  - **Source:** [Reference if documented]

**Alternative Interpretations:**
[If boundary placement ambiguous, list alternatives]
- **Interpretation 1:** [Description]
- **Interpretation 2:** [Description]
```

---

### **Step 5: Data Asset Cataloging**

**Action:** Identify and classify all data types mentioned in documentation

**Data Asset Categories:**
- User credentials and authentication data
- Personal identifiable information (PII)
- Financial/payment data
- Business-critical data
- System configuration and secrets
- Audit logs and monitoring data

**For Each Data Asset:**
```markdown
### Data Asset: [Asset Name]
**Type:** [Credentials/PII/Financial/Business/Configuration/Logs]
**Description:** [What data this includes]
**Source:** "[Documentation describing this data]" ([filename], line [number])

**Sensitivity Classification:**
- **Classification:** [PUBLIC/INTERNAL/CONFIDENTIAL/RESTRICTED]
- **Basis:** [Why this classification - regulatory requirements, business criticality]
- **Confidence:** [HIGH/MEDIUM/LOW]

**Regulatory Considerations:**
- **GDPR:** [Applicable/Not Applicable/Unknown]
  - **Justification:** [Why GDPR applies or doesn't]
- **PCI-DSS:** [Applicable/Not Applicable/Unknown]
  - **Justification:** [Based on payment data presence]
- **HIPAA:** [Applicable/Not Applicable/Unknown]
  - **Justification:** [Based on health data presence]
- **Other:** [Specify if applicable - CCPA, SOX, etc.]

**Storage Locations:**
[List components from inventory storing this data]
- **Component 1:** [How data stored here]
  - **Source:** "[Quote]" ([filename], line [number])

**Transmission Paths:**
[Preliminary - detailed in Stage 2]
- Transmitted between: [Component A] → [Component B]
  - **Source:** "[Quote]" ([filename], line [number])

**Retention Requirements:**
- **Documented:** [Retention period if specified]
- **Unknown:** [Flag if not documented]
```

---

### **Step 6: Scope Definition**

**Action:** Define what is in-scope vs. out-of-scope for threat modeling

**In-Scope Components:**
Include components that:
- Are part of the system being analyzed
- Have security relevance
- Handle sensitive data
- Cross trust boundaries
- Are documented sufficiently for analysis

**Out-of-Scope Components:**
Exclude components that:
- Are external dependencies (unless integration point is in-scope)
- Are infrastructure platform (unless platform security is analysis focus)
- Are monitoring/logging (unless that's the analysis target)
- Lack sufficient documentation for meaningful analysis

**Documentation Pattern:**
```markdown
## Analysis Scope

### In-Scope Components
1. **[Component Name]**
   - **Justification:** [Why included in analysis]
   - **Security Relevance:** [Why security analysis needed]
   - **Documentation Quality:** [Sufficient/Limited/Excellent]

2. **[Component Name]**
   [Same pattern]

### Out-of-Scope Components
1. **[Component Name]**
   - **Justification:** [Why excluded - e.g., external dependency, insufficient docs]
   - **Impact on Analysis:** [How exclusion affects threat modeling]
   - **Dependencies:** [How in-scope components depend on this]

2. **[Component Name]**
   [Same pattern]

### Scope Boundaries Rationale
[Explain overall scope decisions]
- **Included:** [Summary of inclusion criteria applied]
- **Excluded:** [Summary of exclusion criteria applied]
- **Gray Areas:** [Components where scope decision was difficult]
```

---

### **Step 7: Assumption Documentation**

**Action:** Document ALL assumptions made during Stage 1 analysis

**Assumption Categories:**
- Technology stack assumptions
- Architectural pattern assumptions
- Operational scale assumptions
- Business context assumptions
- Security control assumptions
- User behavior assumptions

**For Each Assumption:**
```markdown
### Assumption: [Clear Assumption Statement]
**Category:** [Technology/Architecture/Business/Operational/Security]

**Basis for Assumption:**
[Why this assumption is reasonable given available evidence]
- **Evidence:** "[Quote or observation from docs]" ([filename], line [number])
- **Reasoning:** [Logical basis for assumption]

**Confidence Level:** [MEDIUM/LOW/INSUFFICIENT]
[Note: Cannot be HIGH - HIGH requires documentation, not assumption]

**Alternative Interpretations:**
1. **[Alternative 1]:** [Different way to interpret available information]
   - **Implications:** [How this changes analysis]

2. **[Alternative 2]:** [Another interpretation]
   - **Implications:** [How this changes analysis]

**Impact if Assumption Incorrect:**
- **Technical Impact:** [How incorrect assumption affects technical analysis]
- **Risk Impact:** [How it affects risk assessment]
- **Mitigation Impact:** [How it affects control recommendations]

**Validation Recommendation:**
[How to confirm or refute this assumption]
- **Recommended Action:** [Specific steps to validate]
- **Information Needed:** [What documentation would resolve this]
- **Stakeholder to Contact:** [Who could provide clarification - if in Collaborative mode]
```

**Example:**
```markdown
### Assumption: Mobile application uses HTTPS for all API communications

**Basis for Assumption:**
- **Evidence:** "API endpoints shown in examples use https:// protocol" (api-docs.md, line 78)
- **Reasoning:** Modern mobile apps typically default to HTTPS; examples suggest this pattern

**Confidence Level:** MEDIUM - Reasonable inference from API documentation examples, but not explicitly stated as requirement

**Alternative Interpretations:**
1. **HTTP also supported:** Examples show HTTPS but HTTP might also be allowed
   - **Implications:** Unencrypted data transmission vulnerability

2. **Mixed protocol use:** Different endpoints might use different protocols
   - **Implications:** Some data flows encrypted, others not

**Impact if Assumption Incorrect:**
- **Technical Impact:** Data transmission vulnerability if HTTP used
- **Risk Impact:** Information disclosure and tampering threats significantly elevated
- **Mitigation Impact:** TLS/HTTPS enforcement controls would be critical priority

**Validation Recommendation:**
- **Recommended Action:** Review mobile app network configuration, API gateway settings
- **Information Needed:** API security specifications, mobile app transport security config
- **Stakeholder to Contact:** API development team, mobile app lead (Collaborative mode)
```

---

### **Step 8: Gap Analysis**

**Action:** Systematically identify missing information

**Gap Categories:**
- **Critical Gaps:** Blocking or severely limiting threat modeling
- **Significant Gaps:** Limiting analysis quality and depth
- **Minor Gaps:** Would enhance analysis but not blocking

**Documentation Pattern:**
```markdown
## Documentation Gaps

### Critical Gaps (Blocking Analysis)
1. **[Gap Description]**
   - **Missing Information:** [What's not documented]
   - **Impact:** [How this affects threat modeling stages]
   - **Blocks:** [Which stages cannot proceed effectively]
   - **Workaround:** [How to proceed despite gap - if possible]
   - **Recommendation:** [How to obtain missing information]

### Significant Gaps (Limiting Analysis Quality)
2. **[Gap Description]**
   - **Missing Information:** [What's not documented]
   - **Impact:** [How this limits analysis depth]
   - **Affects:** [Which analysis areas are weakened]
   - **Workaround:** [Generic approach to use instead]
   - **Recommendation:** [How to enhance documentation]

### Minor Gaps (Documentation Enhancements)
3. **[Gap Description]**
   - **Missing Information:** [What's not documented]
   - **Impact:** [Minor effect on completeness]
   - **Enhancement:** [How this would improve analysis]
   - **Priority:** [LOW - nice to have]
```

---

### **Step 9: Confidence Assessment**

**Action:** Provide overall confidence assessment for Stage 1 outputs

```markdown
## Stage 1 Confidence Assessment

### Overall Confidence: [HIGH/MEDIUM/LOW]

**Confidence Breakdown by Category:**

#### Component Inventory: [HIGH/MEDIUM/LOW]
- **HIGH Confidence Elements:** [N] components with explicit documentation
- **MEDIUM Confidence Elements:** [N] components with inferred details
- **LOW Confidence Elements:** [N] components with significant unknowns
- **Rationale:** [Why this overall confidence level]

#### Trust Boundaries: [HIGH/MEDIUM/LOW]
- **Well-Documented Boundaries:** [N] boundaries
- **Inferred Boundaries:** [N] boundaries
- **Ambiguous Boundaries:** [N] boundaries
- **Rationale:** [Why this overall confidence level]

#### Data Assets: [HIGH/MEDIUM/LOW]
- **Explicitly Documented:** [N] assets
- **Inferred from Context:** [N] assets  
- **Unknown Sensitivity:** [N] assets
- **Rationale:** [Why this overall confidence level]

### Factors Limiting Confidence
1. **[Limiting Factor 1]:** [Description and impact]
2. **[Limiting Factor 2]:** [Description and impact]
3. **[Limiting Factor 3]:** [Description and impact]

### Recommendations for Improving Confidence
1. **[Recommendation 1]:** [Specific action to obtain better information]
2. **[Recommendation 2]:** [Specific action to clarify ambiguities]
3. **[Recommendation 3]:** [Specific action to validate assumptions]
```

---

### **Step 10: Output File Creation**

**Action:** Compile all information into `01-system-understanding.md`

**Required Output Structure:**
```markdown
# Stage 1: System Understanding & Scoping
**Target System:** [System Name]
**Analysis Date:** [YYYY-MM-DD]
**Operational Mode:** [Collaborative/Automatic]
**Documentation Specialist:** [Version]

## 1. Executive Summary
[2-3 paragraph overview of system, key findings, critical assumptions]

## 2. Source Documentation Inventory
[List of all source files analyzed]

## 3. System Description
- Business purpose
- Primary users
- Key functionality
- Operational context

## 4. Component Inventory
[Complete documentation for each component]

## 5. Trust Boundaries
[Complete documentation for each boundary]

## 6. Data Asset Catalog
[Complete documentation for each data asset]

## 7. Analysis Scope
- In-scope components with justifications
- Out-of-scope components with justifications

## 8. Assumptions & Constraints
[Complete documentation for each assumption]

## 9. Documentation Gaps
[Complete gap analysis]

## 10. Confidence Assessment
[Overall confidence breakdown]

## 11. Source Documentation References
[Complete bibliography of all sources]

## Appendices (if needed)
- Appendix A: Technology Stack Summary
- Appendix B: Regulatory Requirements Summary
- Appendix C: Glossary of Terms
```

---

## Quality Checklist

Before considering Stage 1 complete, verify:

- [ ] **Every component has source documentation reference**
- [ ] **Technology details marked as Documented/Inferred/Unknown**
- [ ] **No fabricated technologies** (React Native, PostgreSQL, Node.js without docs)
- [ ] **No fabricated business metrics** (user counts, revenue, transaction volumes)
- [ ] **All assumptions have confidence levels**
- [ ] **Alternative interpretations provided for ambiguous items**
- [ ] **Documentation gaps systematically identified**
- [ ] **Professional formatting throughout**
- [ ] **Cross-references are accurate**
- [ ] **Output file follows required structure**

---

## Common Mistakes to Avoid

### ❌ Mistake 1: Technology Fabrication
```markdown
WRONG:
**Backend:** Node.js v16 with Express framework
**Database:** PostgreSQL 13.2 with Redis caching
```

```markdown
CORRECT:
**Backend:**
- **Documented:** RESTful API with JSON responses (api-spec.yaml)
- **Inferred:** None
- **Unknown:** Programming language, framework, hosting platform
- **Confidence:** MEDIUM (functionality clear, implementation unknown)
```

### ❌ Mistake 2: Vague Source References
```markdown
WRONG:
**Source:** Mentioned in the README
```

```markdown
CORRECT:
**Source:** "The system processes bike reservations in real-time" (README.md, lines 23-24)
```

### ❌ Mistake 3: Assumptions Without Confidence
```markdown
WRONG:
**Assumption:** System uses HTTPS for all communications
```

```markdown
CORRECT:
**Assumption:** System uses HTTPS for all communications
**Confidence:** MEDIUM
**Basis:** API examples show https:// URLs (api-docs.md, line 78)
**Alternative:** HTTP might also be supported
**Validation:** Confirm with network configuration documentation
```

### ❌ Mistake 4: Missing Gap Documentation
```markdown
WRONG:
[Proceeding without noting missing information]
```

```markdown
CORRECT:
## Documentation Gaps

### Critical Gap: Authentication Mechanism Not Specified
- **Missing:** How users authenticate to the system
- **Impact:** Cannot assess authentication threats accurately in Stage 3
- **Workaround:** Will apply generic authentication threats
- **Recommendation:** Obtain authentication architecture documentation
```

---

## Output Handoff

**After Stage 1 Complete:**
1. Save `01-system-understanding.md` to target output directory
2. Signal work phase complete (do NOT proceed to validation)
3. Quality-critic will review for data integrity and source traceability
4. After critic approval, Stage 2 documentation-specialist continues with data flow analysis

---

