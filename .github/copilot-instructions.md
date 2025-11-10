# GitHub Copilot Instructions - Threat Modeling Framework

**Platform:** GitHub Copilot (VS Code)  
**Framework Version:** 2.1.0  
**Last Updated:** 2025-11-07

---

**Attribution:** Threat modeling instruction files created by Mike Ensing (ensingm2@gmail.com). Initial implementation developed during Adam Shostack's Threat Modeling Intensive with AI training at OWASP 2025 Global AppSec USA.

---

## 🚀 Framework Entry Point

**For complete framework documentation, read:**
- **`.ai-instructions/core/entry-point.md`** - Central framework overview (START HERE)
- **`.ai-instructions/skills/README.md`** - Skills framework details
- **`.ai-instructions/skills/workflow-guide.md`** - Stage-by-stage execution guide

**Note:** This is a platform-specific loader. The core instruction repository is in `.ai-instructions/` directory and is platform-agnostic.

---

## Platform: GitHub Copilot

**Capabilities:**
- VS Code integration with inline suggestions
- Workspace file reading (limited compared to Cursor)
- Conversation-based interaction
- Git integration

**Limitations:**
- Cannot dynamically load instruction files during conversation
- Limited workspace context compared to Cursor
- May require more inline instructions for complex workflows

---

## ⚠️ MANDATORY FIRST STEP: Operational Mode Selection

**BEFORE beginning ANY threat modeling work, you MUST:**

1. **Ask the user which operational mode to use** (MANDATORY - NEVER skip this)
   - **Collaborative Mode:** Active user engagement, clarifying questions, stage approvals
     - Agent asks clarifying questions when documentation is ambiguous
     - User reviews and approves each stage before progression
     - Best for: Complex systems, user has domain knowledge
   - **Automatic Mode:** Autonomous operation from start to finish
     - Agent works through all 6 stages without user interaction
     - Agent makes reasonable assumptions when unclear
     - Best for: Well-documented systems, hands-off completion

2. **Read the selected mode file:**
   - Collaborative: `.ai-instructions/modes/collaborative-mode.md`
   - Automatic: `.ai-instructions/modes/automatic-mode.md`

3. **Confirm mode understanding BEFORE proceeding to Stage 1**

**PROHIBITED BEHAVIOR:**
- ❌ Starting Stage 1 without asking about operational mode
- ❌ Assuming a mode without explicit user selection
- ❌ Proceeding to threat modeling without mode confirmation

**This is absolute and non-negotiable.**

---

## 6-Stage Workflow Overview

**Complete details in:** `.ai-instructions/skills/workflow-guide.md`

| Stage | Primary Guide | Output File |
|-------|---------------|-------------|
| **1. System Understanding** | `documentation-specialist/stage-1-guide.md` | `01-system-understanding.md` |
| **2. Data Flow Analysis** | `documentation-specialist/stage-2-guide.md` | `02-data-flow-analysis.md`, `02-data-flow-diagram.mermaid`, `02-data-flow-diagram.drawio.xml` |
| **3. Threat Identification** | `threat-modeler/stage-3-threat-identification.md` | `03-threat-identification.md` |
| **4. Risk Assessment** | `threat-modeler/stage-4-risk-assessment.md` | `04-risk-assessment.md` |
| **5. Mitigation Strategy** | `threat-modeler/stage-5-mitigation-strategy.md` | `05-mitigation-strategy.md` |
| **6. Final Reporting** | `threat-modeler/stage-6-final-reporting.md` | `06-final-comprehensive-report.md` |

**All paths relative to:** `.ai-instructions/skills/`

**Output location:** `[target-directory]/output/threat-model/`

---

## ❌ CRITICAL PROHIBITIONS

### **1. NEVER SKIP CRITIC ANALYSIS**

**ABSOLUTE RULE:** After completing ANY stage work, critic analysis is MANDATORY and NEVER optional.

**Required Process:**
1. Complete stage work → Create output file(s)
2. **END WORK PHASE** (no validation in same response)
3. Read critic validation guide → Perform quality validation
4. **END CRITIC PHASE** (no rework in same response)
5. If not approved → Return to step 1 with feedback

**NEVER ASK:**
- "Should I perform critic analysis or proceed to next stage?"
- "Would you like me to skip critic review?"
- "Do you want critic analysis or should I continue?"

**Applies to:** ALL stages (1-6), ALL operational modes, NO exceptions

**Critic guide:** `.ai-instructions/quality-assurance/quality-assurance-framework.md`

### **2. NEVER FABRICATE DATA**

**Data Integrity Rules:**
- ❌ NEVER fabricate: Business metrics, technical details, CVSS scores, system characteristics
- ✅ ALWAYS cite sources: Trace all claims to specific documentation sections
- ✅ ALWAYS document assumptions: Clearly identify inferred vs. documented behaviors
- ✅ ALWAYS use confidence levels: HIGH (85-95%), MEDIUM (70-<85%), LOW (50-<70%), INSUFFICIENT (<50%)

**Confidence framework:** `.ai-instructions/skills/shared/confidence-calibration.md`

### **3. NEVER START WITHOUT MODE SELECTION**

See "MANDATORY FIRST STEP" section above. This is absolute.

---

## External Resource Access Protocol

**Permitted (with explicit user approval):**
- Official documentation, CVE databases, compliance standards, academic research

**Prohibited:**
- Direct system interaction, vulnerability exploitation, live system probing

**Request Protocol:**
1. Ask user approval before accessing external resources
2. Justify why information is essential
3. Specify exact sources needed
4. Proceed only after explicit approval

---

## Key Framework Resources

### **Shared Resources (Read as Needed)**

**Terminology Glossary:**
- Location: `.ai-instructions/skills/shared/terminology-glossary.md`
- Defines: Component, Trust Boundary, Attack Surface, Data Flow, etc.

**Confidence Calibration:**
- Location: `.ai-instructions/skills/shared/confidence-calibration.md`
- Defines: HIGH/MEDIUM/LOW/INSUFFICIENT confidence levels

**Output File Requirements:**
- Location: `.ai-instructions/skills/shared/output-file-requirements.md`
- Defines: Output format specifications for all stages

### **Security Frameworks**

**STRIDE Framework:**
- Location: `.ai-instructions/skills/threat-modeler/frameworks/stride.md`
- Used in: Stage 3 (Threat Identification)

**MITRE ATT&CK:**
- Location: `.ai-instructions/skills/threat-modeler/frameworks/mitre-attack.md`
- Used in: Stage 3 (Threat Identification)

**Cyber Kill Chain:**
- Location: `.ai-instructions/skills/threat-modeler/frameworks/kill-chain.md`
- Used in: Stage 3 (Threat Identification)

---

## Copilot-Specific Notes

### **File Reading Strategy**

Since Copilot has limited dynamic file loading, consider:
1. Read all necessary instruction files at the start of each stage
2. Reference the entry-point file for comprehensive overview
3. Use explicit file reading for stage guides rather than assuming content

### **Context Management**

- Copilot maintains conversation context across turns
- Use this to track progress through stages
- Refer back to previous stage outputs for consistency

### **Workspace Integration**

- Use VS Code's file explorer to navigate instruction files
- Leverage Git integration to track threat model iterations
- Use markdown preview for reviewing outputs

---

## Quick Start Checklist

**Before starting threat modeling:**

- [ ] Read `.ai-instructions/core/entry-point.md` - Framework overview
- [ ] Read `.ai-instructions/skills/README.md` - Skills framework details
- [ ] Select target from `targets/` directory
- [ ] **MANDATORY:** Ask user for operational mode (Collaborative or Automatic)
- [ ] Read selected mode file (`.ai-instructions/modes/[mode].md`)
- [ ] Confirm mode understanding
- [ ] Read Stage 1 guide (`.ai-instructions/skills/documentation-specialist/stage-1-guide.md`)
- [ ] Read terminology glossary (`.ai-instructions/skills/shared/terminology-glossary.md`)
- [ ] Read confidence calibration (`.ai-instructions/skills/shared/confidence-calibration.md`)
- [ ] Begin Stage 1 work

---

## Stage Execution Pattern

**For each stage:**

1. **Read stage guide** (from `.ai-instructions/skills/[specialist]/stage-[N]-guide.md`)
2. **Read relevant frameworks** (e.g., STRIDE, MITRE ATT&CK for Stage 3)
3. **Execute stage work** → Create output file(s)
4. **END WORK PHASE**
5. **Read critic validation guide** (`.ai-instructions/quality-assurance/quality-assurance-framework.md`)
6. **Perform quality validation** → Multi-dimensional scoring
7. **Make approval decision**
8. **If approved:** Proceed to next stage
9. **If not approved:** Iterate with improvements

---

## Platform Comparison

**GitHub Copilot vs Cursor:**
- **Copilot:** Better for inline code suggestions, VS Code integration
- **Cursor:** Better for multi-file context, dynamic instruction loading, integrated terminal

**Both platforms:**
- Use the same core instruction repository (`.ai-instructions/` directory)
- Follow the same 6-stage workflow
- Apply the same quality assurance framework
- Enforce the same critical prohibitions

---

**For complete framework documentation and detailed stage guides, always refer to `.ai-instructions/core/entry-point.md` as the central source of truth.**

---

**This framework enables systematic, high-quality security research with consistent methodology and rigorous evidence-based quality assurance.**

