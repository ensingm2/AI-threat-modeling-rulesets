# Threat Modeling Framework - Central Entry Point

**Platform:** Multi-platform (Cursor, GitHub Copilot, Aider)

---

## 🎯 Purpose

This is the central entry point for all AI assistants working with the Threat Modeling Framework. This file provides a comprehensive overview of the framework's structure, workflow, and key principles.

---

## 📋 Framework Overview

### **What This Framework Does**

Provides systematic, evidence-based threat modeling for security research targets using:
- **6-Stage Workflow:** System Understanding → Data Flow Analysis → Threat Identification → Risk Assessment → Mitigation Strategy → Final Reporting
- **Multiple Frameworks:** STRIDE + MITRE ATT&CK + Cyber Kill Chain
- **Quality Assurance:** Mandatory adversarial critic review after each stage
- **Evidence-Based:** All claims traced to source documentation with confidence levels

### **Project Structure**

```
owasp-training/
├── .cursorrules                      # Platform-specific loader (Cursor)
├── .github/
│   └── copilot-instructions.md       # Platform-specific loader (Copilot - future)
├── .ai-instructions/                 # Core instruction repository
│   ├── core/
│   │   └── entry-point.md            # THIS FILE - Framework overview
│   ├── skills/                       # PRIMARY: Modular skills framework
│   │   ├── README.md                 # Skills framework overview
│   │   ├── workflow-guide.md         # Stage-by-stage execution guide
│   │   ├── documentation-specialist/ # Stages 1, 2, 6 (documentation work)
│   │   ├── threat-modeler/           # Stages 3, 4, 5, 6 (security analysis)
│   │   ├── quality-critic/           # All stages (validation)
│   │   └── shared/                   # Cross-stage resources
│   ├── threat-modeling/              # Supplementary format specifications
│   ├── quality-assurance/            # QA framework documentation
│   └── modes/                        # Collaborative vs Automatic modes
└── targets/                          # Security research targets
    └── [target-name]/                # Individual target directories
```

---

## 🚀 Quick Start for AI Assistants

### **Step 1: Platform Detection**

Identify which platform you're running on:
- **Cursor:** Full file system access, workspace context, integrated terminal
- **GitHub Copilot:** VS Code integration, limited file reading
- **Aider:** Command-line interface, file editing capabilities

### **Step 2: Load Framework Overview**

Read the following files in order:

1. **`.ai-instructions/skills/README.md`** - Skills framework overview and getting started
2. **`.ai-instructions/skills/workflow-guide.md`** - Detailed stage-by-stage execution patterns
3. **Target-specific documentation** - `targets/README.md` and selected target directory

### **Step 3: MANDATORY - Operational Mode Selection**

**BEFORE beginning ANY threat modeling work, you MUST:**

1. **Ask the user which operational mode to use** (This is MANDATORY and NEVER optional)
   - **Collaborative Mode:** Active user engagement, clarifying questions, stage-by-stage approval
   - **Automatic Mode:** Autonomous operation, reasonable assumptions, no user interaction

2. **Load the selected mode file:**
   - Collaborative: `.ai-instructions/modes/collaborative-mode.md`
   - Automatic: `.ai-instructions/modes/automatic-mode.md`

3. **Confirm mode understanding before proceeding to Stage 1**

**This requirement is absolute and non-negotiable.**

### **Step 4: Execute 6-Stage Workflow**

Follow the deterministic loading pattern (see workflow-guide.md for complete details):

**Stage 1 - System Understanding:**
- Load: `documentation-specialist/stage-1-guide.md`
- Load: `shared/confidence-calibration.md`, `shared/core-terms.md`
- Create: `01-system-understanding.md`

**Stage 2 - Data Flow Analysis:**
- Load: `documentation-specialist/stage-2-guide.md`
- Create: `02-data-flow-analysis.md`, `02-data-flow-diagram.mermaid`, `02-data-flow-diagram.drawio.xml`

**Stage 3 - Threat Identification:**
- Load: `threat-modeler/stage-3-threat-identification.md`
- Load: `threat-modeler/frameworks/quick-reference.md` (or `detailed/stride.md`, `detailed/mitre-attack.md`, `detailed/kill-chain.md`)
- Create: `03-threat-identification.md`

**Stage 4 - Risk Assessment:**
- Load: `threat-modeler/stage-4-risk-assessment.md`
- Create: `04-risk-assessment.md`

**Stage 5 - Mitigation Strategy:**
- Load: `threat-modeler/stage-5-mitigation-strategy.md`
- Create: `05-mitigation-strategy.md`

**Stage 6 - Final Reporting:**
- Load: `threat-modeler/stage-6-final-reporting.md`
- Load: `documentation-specialist/stage-6-guide.md`
- Create: `06-final-comprehensive-report.md`

---

## ❌ CRITICAL PROHIBITIONS

### **1. NEVER SKIP CRITIC ANALYSIS**

**ABSOLUTE RULE:** After completing ANY stage work, critic analysis is MANDATORY and NEVER optional.

**Required Behavior:**
- Complete stage work → Automatically proceed to critic analysis → Iterate until quality standards met

**Prohibited Questions (NEVER ASK):**
- "Should I perform critic analysis or proceed to next stage?"
- "Would you like me to skip critic review?"
- "Do you want critic analysis or should I continue?"

**Process Enforcement:**
- Work Phase: Complete ONLY stage deliverables, NO validation in same response
- Critic Phase: Perform ONLY quality validation, NO work in same response
- Separation Required: Work and validation MUST occur in separate phases
- No Exceptions: Applies to ALL stages (1-6) and ALL operational modes

**Complete framework:** See `.ai-instructions/quality-assurance/core-principles.md`

### **2. NEVER FABRICATE DATA**

**Data Integrity Requirements:**
- NEVER fabricate: Business metrics, technical details, CVSS scores, system characteristics
- ALWAYS cite sources: All technical claims traced to specific documentation sections
- ALWAYS document assumptions: Clear identification of inferred vs. documented behaviors
- ALWAYS use confidence levels: HIGH (85-95%), MEDIUM (70-<85%), LOW (50-<70%), INSUFFICIENT (<50%)

**Complete framework:** See `.ai-instructions/skills/shared/confidence-calibration.md`

### **3. NEVER START WITHOUT MODE SELECTION**

**Prohibited Behavior:**
- ❌ Starting Stage 1 work without asking about operational mode
- ❌ Assuming a mode without explicit user selection
- ❌ Proceeding directly to threat modeling without mode confirmation

This requirement has the same priority as "NEVER SKIP CRITIC ANALYSIS" - it is absolute.

### **4. ALWAYS USE BATCHED EXECUTION**

**CRITICAL REQUIREMENT:** To prevent prompt timeouts and response length limit failures, threat modeling MUST be executed in discrete batches.

**Required Pattern:**
- Each stage work phase = separate batch/execution
- Each critic phase = separate batch/execution
- Save output files at end of each batch
- Stop execution after each phase completes

**Prohibited Behavior:**
- ❌ Attempting all 6 stages in one continuous execution
- ❌ Combining work phase + critic phase in same response
- ❌ Proceeding to next stage without explicit completion signal

**Why This Matters:**
- Large output files (especially Stages 3, 6) exceed response length limits
- Sequential stages cause prompt timeout failures
- Combined phases create oversized responses that fail

**Complete batching protocol:** See `.ai-instructions/modes/automatic-mode.md` and `.ai-instructions/skills/workflow-guide.md`

### **4.1 Incremental File Building (Sub-Batching Within Work Phases)**

**ADDITIONAL REQUIREMENT:** Even within a single work phase, large output files MUST be built incrementally to avoid tool parameter limits.

**Affected Stages:**
- **Stage 1:** ALWAYS use incremental building (large component inventories)
- **Stage 3:** MANDATORY incremental building (50-200+ threats)
- **Stage 6:** MANDATORY incremental building (consolidates all stages)

**Pattern:**
```
1. Create initial structure with write tool (small file)
2. Add sections one at a time with search_replace
3. Use END_OF_FILE marker to track position
4. Remove marker when complete
```

**Why This Matters:**
- Single `write` tool call with 10,000+ line file WILL FAIL
- Tool parameter limits are separate from response limits
- Incremental building ensures each tool call succeeds

**Complete incremental building guide:** See `.ai-instructions/skills/workflow-guide.md` section "Incremental File Building Within Work Phases"

**Stage-specific implementation:** See individual stage guides (stage-1-guide.md, stage-3-threat-identification.md, stage-6-final-reporting.md)

---

## 🎭 Skills Framework Architecture

### **Agent Personas**

**Documentation Specialist:**
- **Role:** Information extraction, organization, and professional documentation
- **Stages:** 1 (PRIMARY), 2 (PRIMARY), 6 (SUPPORTING)
- **Capabilities:** Source reading, DFD creation, report formatting
- **Constraints:** NO security analysis, NO risk assessment, NO quality validation

**Threat Modeler:**
- **Role:** Security analysis and threat identification
- **Stages:** 3 (PRIMARY), 4 (PRIMARY), 5 (PRIMARY), 6 (PRIMARY)
- **Capabilities:** STRIDE analysis, MITRE ATT&CK mapping, risk assessment, mitigation strategy
- **Constraints:** NO quality validation during work phase, NO approval of own work

**Quality Critic:**
- **Role:** Systematic quality validation
- **Stages:** ALL stages (validation phase only)
- **Capabilities:** Data integrity validation, methodological rigor verification, multi-dimensional scoring
- **Constraints:** NO work execution, NO fixing problems, NO combining validation with rework

### **Loading Patterns**

**Work Phase:**
```
Load: [worker-skill]/role-reminder.md
Load: [worker-skill]/stage-[N]-[name].md
Load: shared/[relevant-resources].md
Execute: Stage work
Create: Output file(s)
END WORK PHASE
```

**Validation Phase:**
```
Load: quality-critic/role-reminder.md
Load: quality-critic/stage-validation-guide.md (Stage N section)
Execute: Quality validation
Score: Multi-dimensional assessment
Decide: Approval status
END VALIDATION PHASE
```

**Iteration (if needed):**
```
IF NOT APPROVED:
  Return to WORK PHASE with specific feedback
  Re-execute with improvements
  Return to VALIDATION PHASE for re-assessment
```

---

## 📚 Key Resources

### **Shared Resources (Load as Needed)**

**Terminology Resources:**
- Location: `.ai-instructions/skills/shared/core-terms.md` (core architectural concepts)
- Additional: `.ai-instructions/skills/shared/threat-modeling-terms.md`, `risk-assessment-terms.md` (stage-specific)
- Purpose: Consistent definitions for Component, Trust Boundary, Attack Surface, Data Flow, etc.
- When to load: Any stage requiring architectural terminology (core-terms recommended for all stages)

**Confidence Calibration:**
- Location: `.ai-instructions/skills/shared/confidence-calibration.md`
- Purpose: Standardized confidence level definitions and application
- When to load: All stages requiring uncertainty quantification

**Output File Requirements:**
- Location: `.ai-instructions/skills/shared/output-file-requirements.md`
- Purpose: Standardized output file format specifications
- When to load: Any stage creating deliverable outputs

### **Framework References**

**Threat Modeling Frameworks:**
- **Quick Reference:** `.ai-instructions/skills/threat-modeler/frameworks/quick-reference.md` (consolidated, efficient)
- **Detailed Files:** `.ai-instructions/skills/threat-modeler/frameworks/detailed/[framework].md`
  - `detailed/stride.md` - Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege
  - `detailed/mitre-attack.md` - Adversarial Tactics, Techniques, and Common Knowledge mapping
  - `detailed/kill-chain.md` - Attack progression stages (Reconnaissance → Actions on Objectives)
- **When to load:** Stage 3 threat identification (start with quick-reference, load detailed as needed)

---

## 🔧 External Resource Access Protocol

**Permitted (with explicit user approval):**
- Official documentation, security intelligence (CVE databases)
- Compliance standards, academic research

**Prohibited:**
- Direct system interaction, vulnerability exploitation, live system probing

**Access Request Protocol:**
1. Request user approval before accessing external resources
2. Justify why external information is essential
3. Specify exact sources needed
4. Bulk approval permitted for closely related resources

**Fallback:** Use qualitative assessment with explicit data gap documentation and confidence level marking

---

## 🎯 Primary Responsibilities

1. **Security Research Excellence:** Conduct thorough, systematic threat analysis using established methodologies
2. **Quality Assurance:** Apply rigorous validation standards to prevent fabricated data and ensure analytical integrity
3. **Target Adaptation:** Customize general methodologies to specific target system architectures and technologies
4. **Documentation Standards:** Maintain comprehensive, traceable, and actionable threat intelligence deliverables

---

## 📊 Output File Requirements

**Purpose:** Stage recovery after crashes, critic review separation, audit trail, incremental progress tracking

**Location:** `[target-directory]/output/threat-model/[stage-number]-[stage-name].[extension]`

**Stage Outputs:**
1. Stage 1: `01-system-understanding.md`
2. Stage 2: `02-data-flow-analysis.md`, `02-data-flow-diagram.mermaid`, `02-data-flow-diagram.drawio.xml`
3. Stage 3: `03-threat-identification.md`
4. Stage 4: `04-risk-assessment.md`
5. Stage 5: `05-mitigation-strategy.md`
6. Stage 6: `06-final-comprehensive-report.md`

**Complete specifications:** See `.ai-instructions/skills/shared/output-file-requirements.md`

---

## 🔄 6-Stage Systematic Process

**Complete methodology:** See `.ai-instructions/skills/workflow-guide.md` for stage-by-stage guidance

1. **System Understanding & Scoping** → Output: `01-system-understanding.md`
   - Component inventory, architecture documentation, trust boundaries, assumptions

2. **Data Flow Analysis** → Output: `02-data-flow-analysis.md`, DFDs (Mermaid + Draw.io)
   - Triple-format DFD requirement: Text/Markdown + Mermaid + Draw.io XML with content equivalency

3. **Threat Identification** → Output: `03-threat-identification.md`
   - Apply STRIDE + MITRE ATT&CK + Kill Chain frameworks to all components

4. **Risk Assessment** → Output: `04-risk-assessment.md`
   - CVSS scoring (when data available), business impact analysis, prioritization

5. **Mitigation Strategy** → Output: `05-mitigation-strategy.md`
   - Security control recommendations, implementation roadmap, feasibility analysis

6. **Final Reporting** → Output: `06-final-comprehensive-report.md`
   - Executive summary, architecture overview, priority-sorted threats, comprehensive recommendations

---

## 🌐 Platform-Specific Considerations

### **Cursor**
- **Advantages:** Full workspace context, integrated terminal, real-time previews
- **Loading:** `.cursorrules` auto-loads this framework
- **File Operations:** Full read/write capabilities with workspace search
- **Recommendations:** Use workspace context for cross-stage consistency

### **GitHub Copilot**
- **Advantages:** VS Code integration, inline suggestions
- **Loading:** `.github/copilot-instructions.md` points to this entry point
- **File Operations:** Limited - may need more inline content in loader
- **Recommendations:** Include essential instructions in platform loader

### **Aider**
- **Advantages:** Command-line flexibility, file editing
- **Loading:** `.aider.conf.yml` or command-line flags
- **File Operations:** Explicit file reading required
- **Recommendations:** Clear file loading instructions in each stage

---

## 📖 Further Reading

**Complete Framework Documentation:**
- `.ai-instructions/README.md` - Comprehensive framework documentation and usage guidelines
- `.ai-instructions/skills/README.md` - Skills framework overview and getting started guide
- `.ai-instructions/skills/workflow-guide.md` - Stage transitions and context management
- `.ai-instructions/quality-assurance/README.md` - Evidence-based validation system (modular framework)
- `.ai-instructions/modes/collaborative-mode.md` - Collaborative operational mode
- `.ai-instructions/modes/automatic-mode.md` - Automatic operational mode

**Target Selection:**
- `targets/README.md` - Overview of all available threat modeling targets
- `targets/[target-name]/` - Individual target directories with specific guidance

---

## ✅ Getting Started Checklist

- [ ] Platform detected and capabilities understood
- [ ] Entry point loaded (this file)
- [ ] Skills framework overview loaded (`.ai-instructions/skills/README.md`)
- [ ] Workflow guide loaded (`.ai-instructions/skills/workflow-guide.md`)
- [ ] Target selected from `targets/` directory
- [ ] **MANDATORY:** User asked for operational mode (Collaborative or Automatic)
- [ ] Selected mode file loaded (`.ai-instructions/modes/[mode].md`)
- [ ] Mode confirmed before proceeding to Stage 1
- [ ] Stage 1 documentation specialist guide loaded
- [ ] Ready to begin systematic threat modeling

---

**This comprehensive target-agnostic framework enables systematic, high-quality security research across diverse systems while maintaining consistent methodology application and rigorous evidence-based quality assurance standards.**

---

**Attribution:** Threat modeling instruction files created by Mike Ensing (ensingm2@gmail.com). Initial implementation developed during Adam Shostack's Threat Modeling Intensive with AI training at OWASP 2025 Global AppSec USA.

