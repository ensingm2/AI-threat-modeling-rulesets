# Stage 3: Threat Identification | Output: 03-threat-identification.md

---

## ⚠️ CRITICAL: Batched Execution Requirement

**THIS RESPONSE MUST CONTAIN ONLY THE STAGE 3 WORK PHASE**

**MANDATORY PATTERN:**
1. Complete Stage 3 analysis (threat identification for all components)
2. Create and save `03-threat-identification.md` using INCREMENTAL BUILDING (see below)
3. **END THIS RESPONSE** with completion signal
4. **DO NOT proceed to critic phase in same response**

**Completion Signal Format:**
```
✅ STAGE 3 WORK PHASE COMPLETE
- Output File: 03-threat-identification.md
- Total Threats Identified: [N]
- Location: [target]/output/threat-model/
- Status: Ready for critic review
- Next Batch: Stage 3 Critic Phase
```

**PROHIBITED IN THIS RESPONSE:**
- ❌ Performing critic analysis
- ❌ Validating your own work
- ❌ Proceeding to Stage 4
- ❌ Combining work + validation phases

---

## ⚠️ CRITICAL: Incremental File Building - MANDATORY FOR STAGE 3

**PROBLEM:** Stage 3 produces the LARGEST output file (often 50-200+ threats, 15,000+ lines) and WILL exceed tool parameter limits if created in a single `write` tool call.

**SOLUTION: ALWAYS build Stage 3 incrementally - this is NOT optional**

### **Incremental Building Pattern for Stage 3:**

```
Step 1: Create initial structure with header + summary sections
  → Use write tool (keeps file small)

Step 2: Add threats component-by-component
  → Use search_replace to add each component's threats
  → Process one component at a time

Step 3: Add cross-cutting threats and summaries
  → Use search_replace to add remaining sections

Final: Remove END_OF_FILE marker and verify
```

### **Detailed Implementation:**

**Step 1 - Create Initial Structure:**
```markdown
Use write tool to create:
# Stage 3: Threat Identification
[Header info + metadata]

## 1. Executive Summary
[Summary will be completed after threats identified]
TBD - Will complete after all threats documented

## 2. Threat Summary Statistics
TBD - Will calculate after threat inventory complete

## 3. Threats by Component
[Components will be added below]

---
END_OF_FILE
```

**Step 2 - Add Each Component's Threats:**
```markdown
For Component 1, use search_replace:
OLD: "## 3. Threats by Component\n[Components will be added below]\n\n---\nEND_OF_FILE"
NEW: "## 3. Threats by Component\n\n### Component 1: [Name]\n[All STRIDE threats for Component 1]\n\n[Next component placeholder]\n\n---\nEND_OF_FILE"

For Component 2, use search_replace:
OLD: "[Next component placeholder]\n\n---\nEND_OF_FILE"
NEW: "### Component 2: [Name]\n[All STRIDE threats for Component 2]\n\n[Next component placeholder]\n\n---\nEND_OF_FILE"

Continue for ALL components...
```

**Step 3 - Add Remaining Sections:**
```markdown
After all components added, replace placeholder with:
- Trust Boundary-Specific Threats (search_replace)
- Cross-Cutting Threats (search_replace)
- MITRE ATT&CK Summary (search_replace)
- Kill Chain Analysis (search_replace)
- Confidence Assessment (search_replace)
```

**Step 4 - Complete Executive Summary:**
```markdown
Use search_replace to update:
OLD: "## 1. Executive Summary\n[Summary will be completed...]\nTBD - Will complete..."
NEW: "## 1. Executive Summary\n[Complete summary with actual threat counts]"

Same for Summary Statistics section
```

**Step 5 - Remove END_OF_FILE marker:**
```markdown
Use search_replace:
OLD: "---\nEND_OF_FILE"
NEW: "" (empty string)
```

### **Stage 3 Specific Tips:**

- **One component at a time:** Don't try to add multiple components in one search_replace
- **Threat template consistency:** Use consistent threat format for easier building
- **Count as you go:** Track threat counts to populate summary later
- **Section size management:** If one component has >20 threats, consider adding in 2-3 batches
- **Verify incrementally:** After adding 3-4 components, read back to verify format

### **Why This is MANDATORY for Stage 3:**

- ❌ Single write tool call: WILL FAIL - file too large
- ❌ Building entire file in memory: WILL FAIL - exceeds limits
- ✅ Incremental building: Each component addition is manageable size
- ✅ Crash recovery: If interrupted, partial progress saved
- ✅ Verification possible: Can check each component after adding

---

## Stage Objectives

### **Primary Goals:**
1. Apply STRIDE framework systematically across ALL system components
2. Map threats to MITRE ATT&CK techniques
3. Associate threats with Kill Chain stages
4. Include both generic technical threats AND system-specific threats
5. Document attack scenarios with feasibility assessments

### **Success Criteria:**
- Comprehensive STRIDE coverage for each component (all 6 categories)
- Generic technical threat coverage (60-70% implementation-agnostic)
- MITRE ATT&CK and Kill Chain mappings complete for all threats
- Threat feasibility validated against documented capabilities
- Typical threat count achieved based on system complexity

## Threat Identification Methodology

### **Three-Framework Integration:**

**STRIDE:** Threat categorization by security property violated  
**MITRE ATT&CK:** Adversary tactics and techniques mapping  
**Kill Chain:** Attack progression stage identification

### **Threat Balance Requirements:**
- **60-70%** Generic Technical Threats (implementation-agnostic)
- **20-30%** System-Specific Threats (based on documented functionality)
- **10-20%** Operational Threats (business process and operational security)

---

## Context Requirements for This Stage

### **REQUIRED Files (Must Load):**
- `threat-modeler/role-reminder.md` - Your role definition (worker mode, prohibitions)
- `threat-modeler/stage-3-threat-identification.md` - This file
- `threat-modeler/frameworks/quick-reference.md` - Consolidated framework quick reference (recommended starting point)
- OR load detailed versions: `threat-modeler/frameworks/detailed/stride.md`, `detailed/mitre-attack.md`, `detailed/kill-chain.md`
- `shared/confidence-calibration.md` - Confidence level framework
- `shared/core-terms.md` - Core architectural terminology
- `shared/threat-modeling-terms.md` - Threat modeling specific terminology
- `shared/output-file-requirements.md` - Output format specifications

### **REQUIRED Inputs (From Previous Stages):**
- `01-system-understanding.md` - Component inventory, trust boundaries, architecture
- `02-data-flow-analysis.md` + DFD files - Data flows and trust boundary crossings

### **OPTIONAL Files (Load if Needed):**
- None for this stage (all essential files listed as REQUIRED)

### **NOT NEEDED (Can Unload):**
- `documentation-specialist/stage-1-guide.md` - Documentation work complete
- `documentation-specialist/stage-2-guide.md` - Documentation work complete
- `documentation-specialist/role-reminder.md` - Switched to threat-modeler persona

### **Outputs for Next Stages:**
- `03-threat-identification.md` - Comprehensive threat inventory with STRIDE/ATT&CK/Kill Chain mappings
- Will be used by Stages 4-6 for risk assessment, mitigation, and reporting

---

## Expected Threat Count Guidelines

**PURPOSE:** Quality check indicators, NOT minimum requirements forcing artificial threat creation

### **Component-Based Guidelines:**
- **Simple System (3-5 major components):** Typically 15-25 genuine threats
- **Medium System (5-10 major components):** Typically 25-40 genuine threats
- **Complex System (10+ major components):** Typically 40+ genuine threats

**CRITICAL:** Never fabricate threats to meet count guidelines. If legitimate count below typical range, document why system has fewer threats (focused scope, minimal attack surface, limited external interfaces).

## STRIDE Application Requirements

### **Mandatory: ALL Six Categories Per Component**

Each system component MUST be analyzed for ALL six STRIDE categories:

1. **Spoofing:** User identity, device identity, service identity, API endpoints
2. **Tampering:** Data in transit, data at rest, configuration files, application binaries
3. **Repudiation:** Transaction logging, audit trails, non-repudiation mechanisms
4. **Information Disclosure:** Database exposure, API data leaks, client-side storage, network traffic
5. **Denial of Service:** Resource exhaustion, application crashes, network flooding, database locks
6. **Elevation of Privilege:** Authentication bypass, authorization flaws, admin interface access

### **STRIDE Application Format:**

```markdown
## Component: [Component Name]

### S - Spoofing Threats

#### T-001: [Threat Title]
**Category:** Spoofing
**Description:** [Detailed threat description]
**Attack Scenario:** [Step-by-step attack description]
**MITRE ATT&CK:** [Technique ID] - [Technique Name]
**Kill Chain Stage:** [Stage Name]
**Affected Assets:** [Data/Components affected]
**Prerequisites:** [What attacker needs]
**Impact:** [Consequences if exploited]
**Likelihood:** [Initial assessment - refined in Stage 4]
**Risk Rating:** [CRITICAL/HIGH/MEDIUM/LOW - refined in Stage 4]

### T - Tampering Threats

#### T-002: [Threat Title]
[Same format as above]

### R - Repudiation Threats

#### T-003: [Threat Title]
[Same format]

### I - Information Disclosure Threats

#### T-004: [Threat Title]
[Same format]

### D - Denial of Service Threats

#### T-005: [Threat Title]
[Same format]

### E - Elevation of Privilege Threats

#### T-006: [Threat Title]
[Same format]
```

## Generic Technical Threats (Implementation-Agnostic)

### **Mobile Application Generic Threats:**
- Client-side data storage vulnerabilities (credentials, tokens, sensitive data)
- Reverse engineering and intellectual property extraction
- Man-in-the-middle attacks on API communication
- Certificate pinning bypass and insecure communications
- Application tampering and repackaging attacks
- Local authentication bypass vulnerabilities
- Insecure inter-process communication (IPC)
- Insufficient jailbreak/root detection

### **API/Backend Generic Threats:**
- Injection attacks (SQL, NoSQL, command injection, LDAP)
- Authentication and authorization bypass vulnerabilities
- API rate limiting bypass and resource exhaustion
- Server-side request forgery (SSRF) vulnerabilities
- Cross-site scripting (XSS) in web interfaces
- Privilege escalation and lateral movement attacks
- Insecure direct object references (IDOR)
- Business logic manipulation attacks
- API endpoint enumeration and information disclosure

### **IoT Device Generic Threats:**
- Firmware vulnerabilities and reverse engineering
- Physical device tampering and hardware extraction attacks
- Wireless communication interception and replay attacks
- Device identity spoofing and authentication bypass
- Remote code execution via communication protocols
- Side-channel attacks (power analysis, timing attacks)
- Insecure firmware update mechanisms
- Physical access exploitation

### **Cloud Infrastructure Generic Threats:**
- Container escape and serverless function vulnerabilities
- Misconfigured cloud storage and database exposure
- Identity and Access Management (IAM) privilege escalation
- Network segmentation bypass and lateral movement
- Supply chain attacks on dependencies and libraries
- Logging and monitoring evasion techniques
- Cloud API authentication and authorization flaws
- Resource exhaustion and cost manipulation attacks

### **Database Generic Threats:**
- SQL/NoSQL injection vulnerabilities
- Privilege escalation within database
- Backup exposure and data exfiltration
- Encryption at rest bypass
- Connection string exposure
- Stored procedure/function exploitation
- Database denial of service attacks

## System-Specific Threats

### **Based on Documented Functionality:**

Analyze specific business logic and features documented in source materials:

```markdown
### T-XXX: [System-Specific Threat]
**Category:** [STRIDE Category]
**Description:** Threat specific to [documented feature/functionality]
**Business Logic Flaw:** [Explanation of how documented business process vulnerable]
**Source Reference:** "[Documentation describing vulnerable functionality]" ([file], line [number])
**Attack Scenario:** [Specific attack leveraging documented system behavior]
**MITRE ATT&CK:** [Technique ID] - [Technique Name]
**Kill Chain Stage:** [Stage]
**Confidence:** [HIGH/MEDIUM/LOW] - [Justification based on documentation]
```

**Examples of System-Specific Threats:**
- Pricing algorithm manipulation (if pricing logic documented)
- Account privilege escalation via documented role system
- Data export functionality abuse
- Workflow bypass in documented approval processes
- Payment/transaction manipulation based on documented payment flow

## MITRE ATT&CK Mapping

### **Required Elements:**

For each threat, map to appropriate MITRE ATT&CK technique(s):

```markdown
**MITRE ATT&CK Mapping:**
- **Tactic:** [e.g., Initial Access, Persistence, Privilege Escalation]
- **Technique:** [Technique ID] - [Technique Name]
- **Sub-Technique:** [Sub-Technique ID] - [Sub-Technique Name] (if applicable)
- **Reference:** https://attack.mitre.org/techniques/[Technique-ID]/
```

**Common ATT&CK Techniques for Threat Modeling:**
- T1078: Valid Accounts
- T1190: Exploit Public-Facing Application
- T1566: Phishing
- T1059: Command and Scripting Interpreter
- T1110: Brute Force
- T1212: Exploitation for Credential Access
- T1087: Account Discovery
- T1530: Data from Cloud Storage Object
- T1213: Data from Information Repositories

### **ATT&CK Mapping Best Practices:**
- Use most specific technique/sub-technique applicable
- Map to multiple techniques if threat enables multiple tactics
- Include tactic context for each technique
- Reference ATT&CK documentation for accuracy

## Kill Chain Mapping

### **Required Elements:**

Associate each threat with Kill Chain stage(s):

```markdown
**Kill Chain Stage:** [Stage Name]
**Stage Description:** [How this threat fits within attack progression]
**Prerequisite Stages:** [Earlier stages required before this threat exploitable]
**Enables Following Stages:** [Later stages this threat enables access to]
```

**Kill Chain Stages:**
1. **Reconnaissance:** Information gathering about target
2. **Weaponization:** Preparing attack tools and exploits
3. **Delivery:** Transmitting attack to target
4. **Exploitation:** Executing attack code/action
5. **Installation:** Establishing persistent access
6. **Command & Control:** Maintaining communication with compromised system
7. **Actions on Objectives:** Achieving attacker goals (data theft, disruption, etc.)

### **Kill Chain Context Examples:**

```markdown
### T-015: SQL Injection in API Endpoint
**Kill Chain Stage:** Exploitation
**Stage Description:** Attacker exploits vulnerability to execute unauthorized database queries
**Prerequisite Stages:**
- Reconnaissance: API endpoint enumeration and parameter discovery
- Weaponization: Crafting SQL injection payload
- Delivery: Submitting malicious input to vulnerable parameter
**Enables Following Stages:**
- Installation: Potential web shell deployment via SQL commands
- Command & Control: Database-based command channel
- Actions on Objectives: Data exfiltration, data manipulation, credential theft
```

## Threat Documentation Format

### **Complete Threat Entry Template:**

```markdown
## Threat ID: T-XXX
**Threat Title:** [Concise descriptive title]
**STRIDE Category:** [S/T/R/I/D/E]
**Component:** [Affected component name]
**Threat Type:** [Generic Technical / System-Specific / Operational]

### Description
[Detailed explanation of the threat - 2-4 sentences]

### Attack Scenario
**Attacker Profile:** [Skills/access required]
**Attack Steps:**
1. [Step 1]
2. [Step 2]
3. [Step 3]
[Continue as needed]

**Attack Outcome:** [Result of successful attack]

### Technical Analysis
**Attack Vector:** [How attack is delivered]
**Attack Complexity:** [Low/Medium/High - initial assessment]
**Privileges Required:** [None/Low/High - initial assessment]
**Source Reference:** [Documentation describing vulnerable component/functionality]
**Confidence:** [HIGH/MEDIUM/LOW] - [Justification]

### Framework Mappings
**MITRE ATT&CK:**
- Tactic: [Tactic Name]
- Technique: [TID] - [Technique Name]
- Sub-Technique: [STID] - [Sub-Technique Name] (if applicable)

**Kill Chain Stage:** [Stage Name]
**Stage Context:** [How threat fits in attack progression]

### Impact Analysis
**Affected Assets:**
- [Data Asset 1]: [Impact description]
- [Data Asset 2]: [Impact description]

**Potential Consequences:**
- **Confidentiality:** [Impact level and description]
- **Integrity:** [Impact level and description]
- **Availability:** [Impact level and description]
- **Business Impact:** [Qualitative description based on available information]

### Preliminary Risk Assessment
**Initial Risk Rating:** [CRITICAL/HIGH/MEDIUM/LOW]
**Justification:** [Why this rating - refined in Stage 4]
**Factors:**
- Likelihood: [Initial assessment]
- Impact: [Initial assessment]
- Exploitability: [Initial assessment]
```

## Output File Structure

```markdown
# Stage 3: Threat Identification
**Target System:** [System Name]
**Analysis Date:** [Date]
**Operational Mode:** [Collaborative/Automatic]
**Total Threats Identified:** [N]

## 1. Executive Summary
- Total threats by STRIDE category
- Total threats by risk rating
- Key threat patterns identified
- Critical threats requiring immediate attention

## 2. Threat Summary Statistics

### By STRIDE Category
- Spoofing (S): [count]
- Tampering (T): [count]
- Repudiation (R): [count]
- Information Disclosure (I): [count]
- Denial of Service (D): [count]
- Elevation of Privilege (E): [count]

### By Threat Type
- Generic Technical: [count] ([percentage]%)
- System-Specific: [count] ([percentage]%)
- Operational: [count] ([percentage]%)

### By Initial Risk Rating
- CRITICAL: [count]
- HIGH: [count]
- MEDIUM: [count]
- LOW: [count]

## 3. Threats by Component

### Component 1: [Component Name]
[All STRIDE categories with threat entries]

### Component 2: [Component Name]
[All STRIDE categories with threat entries]

[Continue for all components]

## 4. Trust Boundary-Specific Threats

### Trust Boundary: [Boundary Name]
[Threats specifically related to crossing this trust boundary]

## 5. Cross-Cutting Threats
[Threats affecting multiple components or system-wide concerns]

## 6. MITRE ATT&CK Summary
**Tactics Represented:** [List]
**Most Common Techniques:** [Top 5 with counts]
**ATT&CK Coverage Assessment:** [Analysis of adversary technique coverage]

## 7. Kill Chain Analysis
**Threats by Stage:**
- Reconnaissance: [count]
- Weaponization: [count]
- Delivery: [count]
- Exploitation: [count]
- Installation: [count]
- Command & Control: [count]
- Actions on Objectives: [count]

## 8. Threat Identification Confidence Assessment
**Overall Confidence:** [HIGH/MEDIUM/LOW]
**High Confidence Threats:** [count] - [Based on documented functionality]
**Medium Confidence Threats:** [count] - [Reasonable inferences]
**Low Confidence Threats:** [count] - [Generic industry patterns]
**Assumptions Impacting Threat Analysis:** [List key assumptions]

## 9. Recommendations for Stage 4
- Priority threats for detailed risk assessment
- Threats requiring additional validation
- Areas needing clarification for accurate CVSS scoring
```

## Stage 3 Critic Validation Focus

**Critic Must Verify:**
- **STRIDE Completeness:** ALL six categories addressed for each component
- **Generic Threat Coverage:** 60-70% implementation-agnostic threats included
- **Threat Count Reasonableness:** Count appropriate for system complexity (not fabricated to meet guidelines)
- **MITRE ATT&CK Accuracy:** Technique mappings correct and specific
- **Kill Chain Logic:** Stage associations logical within attack progression
- **Feasibility:** Attack scenarios validated against documented system capabilities
- **No Fabrication:** Threats based on documented functionality or generic patterns, not invented details

**Critic Must Challenge:**
- Predominantly system-specific threats without generic technical coverage
- Missing STRIDE categories for major components
- Threat counts significantly below typical range without justification
- MITRE ATT&CK mappings too vague or incorrect
- Attack scenarios requiring undocumented technical capabilities
- Threats based on assumed rather than documented system behavior

## References

**Related Skills:**
- `stage-1-system-understanding.md` - Component inventory
- `stage-2-data-flow-analysis.md` - Attack surface and trust boundaries
- `frameworks/quick-reference.md` - Consolidated framework quick reference (recommended)
- OR `frameworks/detailed/stride.md`, `detailed/mitre-attack.md`, `detailed/kill-chain.md` for comprehensive guidance
- `../shared/core-terms.md` - Core architectural terminology
- `../shared/threat-modeling-terms.md` - Threat modeling specific terminology
- `../shared/confidence-calibration.md` - Confidence levels for threat assessments

---

**REMINDER: When modifying this skill, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

