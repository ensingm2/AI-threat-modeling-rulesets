# Threat Modeling Skills Framework

**Framework Type:** Claude Skills Modular Architecture  
**Purpose:** Structured AI agent skills for systematic threat modeling

---

## 🚀 Quick Start

### **Welcome to the Threat Modeling Skills Framework**

This is a modular, persona-based architecture for conducting systematic threat modeling through a deterministic 6-stage workflow with rigorous quality validation.

**Architecture Note:** This framework uses a centralized instruction repository (`.ai-instructions/`) with platform-specific loaders (`.cursorrules` for Cursor, `.github/copilot-instructions.md` for Copilot, etc.). All platforms point to `.ai-instructions/core/entry-point.md` as the central framework documentation.

### **✅ Getting Started**

**For comprehensive framework overview:**
```
1. Read: .ai-instructions/core/entry-point.md - Central framework documentation
2. Read: .ai-instructions/skills/README.md (this file) - Skills framework details
3. Read: .ai-instructions/skills/workflow-guide.md - Stage transitions and loading patterns
```

**For threat modeling execution:**
```
1. ⚠️ MANDATORY: Ask user for operational mode selection
   - Ask: "Which operational mode: Collaborative or Automatic?"
   - Load: .ai-instructions/modes/[user-selected-mode].md
   - Confirm mode before proceeding
2. ONLY AFTER step 1: Begin Stage 1
   - Load: .ai-instructions/skills/documentation-specialist/stage-1-guide.md
   - Load: .ai-instructions/skills/shared/confidence-calibration.md
   - Load: .ai-instructions/skills/shared/core-terms.md
```

### **🎯 What You'll Do**

**6-Stage Systematic Process:**
1. **System Understanding** - Documentation extraction and architecture analysis
2. **Data Flow Analysis** - Map data flows, trust boundaries, and attack surface  
3. **Threat Identification** - Apply STRIDE + MITRE ATT&CK + Kill Chain
4. **Risk Assessment** - CVSS scoring and business impact analysis
5. **Mitigation Strategy** - Security control recommendations and roadmap
6. **Final Reporting** - Comprehensive stakeholder-ready deliverable

**Operational Modes:**
- **Collaborative Mode** - User-engaged, question-based interaction
- **Automatic Mode** - Autonomous execution with assumptions

---

## Skills Framework Overview

This directory contains modular, composable skills for AI agents conducting systematic threat modeling. The framework separates concerns into distinct agent personas with specific capabilities and constraints.

### **Design Principles:**

1. **Separation of Concerns:** Worker agents execute tasks, critic agents validate quality
2. **Modular Loading:** Load only the skills needed for current task
3. **Persona Enforcement:** Clear role boundaries prevent context mixing
4. **Reusable Components:** Shared resources used across multiple skills
5. **Quality-First:** Evidence-based validation integrated throughout

## Skill Directory Structure

```
.ai-instructions/skills/
├── README.md                          # This file - orchestration guide
├── workflow-guide.md                  # Stage transition and loading patterns
├── threat-modeler/                    # Worker agent for threat analysis
│   ├── role-reminder.md               # Threat modeler role reminder (worker mode, ~150 tokens)
│   ├── stage-3-threat-identification.md  # Stage 3: STRIDE threat identification
│   ├── stage-4-risk-assessment.md     # Stage 4: Risk assessment and CVSS scoring
│   ├── stage-5-mitigation-strategy.md # Stage 5: Mitigation recommendations
│   ├── stage-6-final-reporting.md     # Stage 6: Final report content synthesis
│   └── frameworks/                    # Framework guidance
│       ├── quick-reference.md         # Consolidated framework quick reference
│       └── detailed/                  # Detailed framework files
│           ├── stride.md              # STRIDE threat categorization (detailed)
│           ├── mitre-attack.md        # MITRE ATT&CK technique mapping (detailed)
│           └── kill-chain.md          # Cyber Kill Chain progression (detailed)
├── quality-critic/                    # Validation agent for quality assurance
│   ├── role-reminder.md               # Quality critic role reminder (critic mode, ~200 tokens)
│   └── stage-validation-guide.md      # Stage-specific validation criteria
├── documentation-specialist/          # Documentation and organization specialist
│   ├── role-reminder.md               # Documentation specialist role reminder (worker mode, ~100 tokens)
│   ├── stage-1-guide.md               # Stage 1: System understanding guide
│   ├── stage-2-guide.md               # Stage 2: Data flow analysis guide
│   └── stage-6-guide.md               # Stage 6: Report compilation guide
└── shared/                            # Shared resources across skills
    ├── core-terms.md                  # Core architectural and methodology terms
    ├── threat-modeling-terms.md       # Threat modeling specific terms
    ├── risk-assessment-terms.md       # Risk assessment specific terms
    ├── confidence-calibration.md      # Confidence level framework
    ├── output-file-requirements.md    # Output format specifications
    └── loading-guide.md               # Centralized loading patterns reference
```

## Core Skills

### **1. Documentation Specialist (Technical Documentation Agent)**

**Location:** `documentation-specialist/`  
**Agent Type:** Technical Documentation Specialist  
**Primary Function:** Information extraction, organization, and documentation

**Capabilities:**
- Source documentation reading and comprehension
- Information extraction and structured organization
- Professional documentation formatting
- Triple-format Data Flow Diagram creation
- Cross-reference management and consistency
- Technical diagram creation (Mermaid, Draw.io)
- Report compilation and presentation quality

**Constraints:**
- NO security threat analysis (that's threat-modeler's role)
- NO risk assessment or scoring (that's threat-modeler's role)
- NO quality validation (that's quality-critic's role)
- MUST cite all source documentation
- MUST mark assumptions explicitly
- MUST document data gaps

**Applicable Stages:**
- **Stage 1 (PRIMARY):** System understanding, component inventory, documentation organization
- **Stage 2 (PRIMARY):** Data flow analysis, triple-format DFD creation, attack surface mapping
- **Stage 6 (SUPPORTING):** Final report compilation, formatting, presentation quality

**Loading Pattern:**
```
# When performing Stage 1 system understanding:
Load: documentation-specialist/role-reminder.md
Load: documentation-specialist/stage-1-guide.md
Load: shared/core-terms.md
Load: shared/confidence-calibration.md
Load: shared/output-file-requirements.md

# When performing Stage 2 data flow analysis:
Load: documentation-specialist/role-reminder.md
Load: documentation-specialist/stage-2-guide.md
Load: shared/core-terms.md
Load: shared/output-file-requirements.md

# When performing Stage 6 report compilation (supporting role):
Load: documentation-specialist/role-reminder.md
Load: documentation-specialist/stage-6-guide.md
Load: shared/output-file-requirements.md
```

**Collaboration Notes:**
- **Stage 1-2:** Documentation-specialist leads
- **Stage 3-5:** Threat-modeler leads (security analysis)
- **Stage 6:** Collaborative (threat-modeler provides content, documentation-specialist provides formatting)

---

### **2. Threat Modeler (Security Analysis Agent)**

**Location:** `threat-modeler/`  
**Agent Type:** Worker  
**Primary Function:** Execute threat modeling analysis

**Capabilities:**
- System architecture analysis and component identification
- Data flow modeling with triple-format DFD generation
- STRIDE threat identification across all system components
- MITRE ATT&CK and Kill Chain framework integration
- Risk assessment with CVSS scoring (when data available)
- Mitigation strategy development and implementation roadmap
- Comprehensive final report generation

**Constraints:**
- NO quality validation during work phase
- NO approval of own work
- NO proceeding without critic validation
- MUST create output files for each stage
- MUST base all claims on source documentation

**Stage-Specific Skills:**
- **Stage 1:** System understanding, component inventory, trust boundaries
- **Stage 2:** Data flow analysis, DFD triple-format generation, attack surface mapping
- **Stage 3:** Threat identification, STRIDE/ATT&CK/Kill Chain application
- **Stage 4:** Risk assessment, CVSS scoring (with constraints), business impact analysis
- **Stage 5:** Mitigation strategy, control recommendations, implementation roadmap
- **Stage 6:** Final comprehensive report consolidation

**Loading Pattern:**
```
# When performing Stage 3 threat identification:
Load: threat-modeler/role-reminder.md
Load: threat-modeler/stage-3-threat-identification.md
Load: threat-modeler/frameworks/quick-reference.md  # Start here
# OR load detailed versions if comprehensive guidance needed:
# Load: threat-modeler/frameworks/detailed/stride.md
# Load: threat-modeler/frameworks/detailed/mitre-attack.md
# Load: threat-modeler/frameworks/detailed/kill-chain.md
Load: shared/confidence-calibration.md
```

---

### **3. Quality Critic (Validation Agent)**

**Location:** `quality-critic/`  
**Agent Type:** Critic / Validator  
**Primary Function:** Systematic quality validation

**Capabilities:**
- Data integrity validation (fabrication detection)
- Methodological rigor verification (STRIDE coverage, framework consistency)
- Source documentation traceability checking
- Analytical depth assessment (threat coverage, assumption quality)
- Stakeholder utility evaluation (actionability across perspectives)
- Multi-dimensional quality scoring (1-5 scale per dimension)
- Graduated approval decisions (Confident/Conditional/Targeted/Major Rework)

**Constraints:**
- NO work execution during critic phase
- NO fixing identified problems
- NO combining validation with rework
- MUST identify 2-3 genuine issues (unless exceptional quality demonstrated)
- MUST actively seek problems, not rubber-stamp

**Validation Focus Per Stage:**
- **Stage 1:** No fabricated tech stacks, all components sourced, assumptions documented
- **Stage 2:** Triple-format DFD equivalency, trust boundary logic, attack surface completeness
- **Stage 3:** ALL STRIDE categories per component, generic threat balance, ATT&CK/KC mapping
- **Stage 4:** CVSS only when fully documented, no fabricated business metrics, confidence appropriate
- **Stage 5:** Threat-to-control mapping, feasibility within constraints, no cost fabrication
- **Stage 6:** ALL Stage 3 threats included, executive-appropriate, self-contained report

**Loading Pattern:**
```
# When validating Stage 3 threat identification:
Load: quality-critic/role-reminder.md
Load: quality-critic/stage-validation-guide.md (Stage 3 section)
Load: shared/confidence-calibration.md
```

---

## Shared Resources

### **Terminology Resources**
**Locations:**
- `shared/core-terms.md` - Core architectural and methodology concepts (recommended for all stages)
- `shared/threat-modeling-terms.md` - Threat modeling specific terminology
- `shared/risk-assessment-terms.md` - Risk assessment specific terminology

**Core Terms Include:**
- Component (System Architecture), Trust Boundary, Attack Surface, Data Flow
- External Entity, Threat Actor, Mitigation Control
- Major Component Counting Criteria
- Confidence levels, Data quality standards

**When to Load:** core-terms.md recommended for all stages; load others as needed

---

### **Confidence Calibration Framework**
**Location:** `shared/confidence-calibration.md`  
**Purpose:** Standardized confidence level definitions and application

**Confidence Levels:**
- **HIGH (85-95%):** Direct source documentation with specific references
- **MEDIUM (70-<85%):** Reasonable inferences with documented assumptions
- **LOW (50-<70%):** Industry patterns with external source notation
- **INSUFFICIENT (<50%):** Inadequate data requiring qualitative assessment

**When to Load:** All stages requiring uncertainty quantification

---

### **Output File Requirements**
**Location:** `shared/output-file-requirements.md`  
**Purpose:** Standardized output file format specifications

**Defines:**
- Output file naming conventions
- Required sections per stage
- Markdown formatting standards
- Source reference formats
- Professional presentation guidelines

**When to Load:** Any stage creating deliverable outputs

---

## Skill Orchestration Patterns

### **Basic Stage Execution Pattern**

```
1. Load Threat Modeler Skill + Stage-Specific Instructions
2. Load Relevant Shared Resources
3. Execute Stage Work → Create Output File(s)
4. ====== WORK PHASE ENDS ======
5. Load Quality Critic Skill + Validation Guide
6. Execute Validation → Multi-Dimensional Scoring
7. Make Approval Decision (Graduated Framework)
8. IF Approved → Proceed to Next Stage
9. IF Not Approved → Return to Step 1 for Iteration
```

### **Detailed Stage 3 Example**

```
# WORK PHASE
Load Skills:
- threat-modeler/role-reminder.md
- threat-modeler/stage-3-threat-identification.md
- threat-modeler/frameworks/quick-reference.md  # Or detailed/ versions if needed
- shared/core-terms.md
- shared/threat-modeling-terms.md
- shared/confidence-calibration.md
- shared/output-file-requirements.md

Execute:
- Apply STRIDE to all components (ALL 6 categories)
- Map threats to MITRE ATT&CK techniques
- Associate with Kill Chain stages
- Create 03-threat-identification.md output file
- END WORK PHASE

# VALIDATION PHASE
Load Skills:
- quality-critic/role-reminder.md
- quality-critic/stage-validation-guide.md (Stage 3 section)
- shared/confidence-calibration.md

Execute:
- Validate STRIDE coverage (all categories per component)
- Check generic vs. specific threat balance (60-70% generic)
- Verify ATT&CK and Kill Chain mappings
- Score across 5 quality dimensions (1-5 each)
- Make graduated approval decision
- END VALIDATION PHASE

# ITERATION (if needed)
If NOT APPROVED:
- Agent addresses specific feedback
- Return to WORK PHASE (re-load worker skills)
- Re-execute with improvements
- Return to VALIDATION PHASE (re-load critic skills)
```

### **Multi-Stage Workflow**

```
FOR EACH Stage (1 through 6):
    [WORK PHASE]
    Load: threat-modeler/role-reminder.md (or documentation-specialist/role-reminder.md for Stages 1-2)
    Load: threat-modeler/stage-[N]-[stage-name].md
    Load: Relevant frameworks (if applicable)
    Load: Shared resources as needed
    Execute: Stage work
    Create: Output file(s)
    
    [VALIDATION PHASE]
    Load: quality-critic/role-reminder.md
    Load: quality-critic/stage-validation-guide.md
    Execute: Stage validation
    Score: Quality dimensions
    Decide: Approval status
    
    [DECISION]
    IF APPROVED:
        Proceed to next stage
    ELSE:
        Iterate current stage
END FOR
```

## Operational Modes

### **COLLABORATIVE MODE**
**User Engagement:** Active participation throughout

**Skill Loading Strategy:**
- Load worker skill → Work → Pause
- Load critic skill → Validate → Share with user
- User reviews → Provides feedback
- User makes approval decision

**Benefits:**
- Higher quality through domain expertise
- Clarification of ambiguities
- Stakeholder alignment throughout

---

### **AUTOMATIC MODE**
**User Engagement:** No interaction after mode selection

**Skill Loading Strategy:**
- Load worker skill → Work → Complete
- Load critic skill → Validate → Decide
- Agent makes approval decision
- Continue or iterate automatically

**Benefits:**
- Faster completion
- No user interruption
- Self-contained analysis

---

## Best Practices

### **Skill Loading Efficiency**

**DO:**
- ✅ Load only skills needed for current task
- ✅ Load shared resources once per stage
- ✅ Reference framework files when needed (STRIDE, ATT&CK, Kill Chain)
- ✅ Keep worker and critic phases strictly separated

**DON'T:**
- ❌ Load all skills at once (context pollution)
- ❌ Mix worker and critic skills in same phase
- ❌ Load validation skills during work phase
- ❌ Skip shared resource loading when terminology needed

### **Quality Assurance Integration**

**Every Stage Requires:**
1. Evidence-based work execution
2. Output file creation
3. Systematic validation
4. Multi-dimensional quality scoring
5. Graduated approval decision

**Never Skip:**
- Critic validation (MANDATORY)
- Source documentation references
- Assumption documentation
- Confidence level calibration

### **Cross-Stage Consistency**

**Maintain Consistency:**
- Component names from Stage 1 used in all subsequent stages
- Trust boundaries from Stage 2 referenced in threat analysis
- Threat IDs from Stage 3 used in Stage 4, 5, 6
- Risk ratings from Stage 4 drive Stage 5 priorities
- Stage 6 includes ALL threats from Stage 3

**Validation Checks:**
- Cross-reference IDs across stages
- Verify terminology consistency
- Check numerical consistency (threat counts)
- Validate alignment of priorities

## Advanced Patterns

### **Parallel Threat Analysis**

For large systems, threat identification could be parallelized:

```
Load: threat-modeler + Stage 3 skills
Split Components: [Component A, B, C] vs [Component D, E, F]
Parallel Analysis: Two separate STRIDE analyses
Merge: Combine threat inventories
Validate: Single comprehensive critic review
```

### **Iterative Refinement**

```
Work Phase → Critic finds 5 issues
Iteration 1: Address issues → Re-critic finds 2 remaining issues
Iteration 2: Address issues → Re-critic finds work meets standards
Approval: Proceed to next stage
```

### **Framework Deep-Dive**

For complex threat scenarios, load additional framework context:

```
# Standard Loading
Load: stride.md

# Deep-Dive Loading (when needed)
Load: stride.md
Load: mitre-attack.md (full technique descriptions)
Load: kill-chain.md (multi-stage attack scenarios)
Reference: External ATT&CK documentation (with user approval)
```

## Skill Extension Guidelines

### **Adding New Skills**

To add a new skill to the framework:

1. Create skill directory: `.ai-instructions/skills/[skill-name]/`
2. Create role reminder: `[skill-name]/role-reminder.md` (lean 100-200 token summary)
3. Define role constraints (worker vs. critic)
4. Specify capabilities and prohibitions
5. Create supporting instruction files as needed
6. Update this README with new skill documentation

### **Modifying Existing Skills**

When updating skills:

1. Update skill instruction files
2. Update this orchestration README if patterns change
3. Commit changes with descriptive git commit messages

### **Creating Shared Resources**

For concepts used across multiple skills:

1. Create in `shared/` directory
2. Use descriptive filename (`[concept]-[purpose].md`)
3. Include cross-references in relevant skills
4. Document loading patterns in this README

## Related Framework Components

### **Directory Structure**

```
.ai-instructions/
├── skills/                    # PRIMARY: Modular skills framework (this directory)
│   ├── threat-modeler/        # Security analysis skills
│   ├── documentation-specialist/ # Documentation and organization skills
│   ├── quality-critic/        # Validation skills
│   └── shared/                # Shared resources
├── threat-modeling/           # Supplementary format specifications
│   ├── stage-2-dfd-requirements.md
│   └── stage-6-final-report-requirements.md
├── quality-assurance/         # QA framework and validation criteria
└── modes/                     # Operational mode definitions
```

**Framework Integration:**
- **Skills Framework:** Primary approach for all threat modeling
- **Supplementary Specs:** Detailed format requirements (DFD, reports)
- **Quality Assurance:** Adversarial critic validation framework
- **Operational Modes:** Collaborative vs Automatic execution patterns

## Troubleshooting

### **Problem: Context Window Overflow**

**Solution:** Load fewer skills per operation
- Load only current stage instructions, not all stages
- Reference framework files only when needed
- Use file references instead of loading full content

### **Problem: Worker/Critic Boundary Violations**

**Symptom:** Agent performing work during validation or validating during work

**Solution:** 
- Explicitly load only worker OR critic skills per phase
- Never load both simultaneously
- Clear phase transitions with explicit skill unloading

### **Problem: Cross-Stage Inconsistencies**

**Symptom:** Component names differ between stages, threat IDs misaligned

**Solution:**
- Load previous stage outputs as reference
- Maintain ID and terminology registries
- Use critic validation to catch inconsistencies

### **Problem: Insufficient Quality Rigor**

**Symptom:** Critic rubber-stamping without genuine analysis

**Solution:**
- Re-emphasize minimum 2-3 genuine issues requirement
- Load full stage-validation-guide.md for comprehensive criteria
- Review multi-dimensional scoring definitions

## Future Enhancements

**Planned Skills:**
- **Research Assistant:** External documentation gathering and summarization with automated retrieval
- **Compliance Analyst:** Regulatory requirement mapping (GDPR, PCI-DSS, HIPAA, SOC 2)
- **Architecture Validator:** Deep technical architecture review and verification

**Planned Frameworks:**
- **PASTA (Process for Attack Simulation and Threat Analysis)**
- **OCTAVE (Operationally Critical Threat, Asset, and Vulnerability Evaluation)**
- **FAIR (Factor Analysis of Information Risk)**

**Planned Enhancements:**
- Enhanced automation for repetitive analysis tasks
- Pattern library for common threat scenarios
- Integration with threat intelligence feeds
- Automated validation of CVSS calculations
