# Skills Framework Workflow Guide

**Purpose:** Deterministic skillset loading patterns for systematic threat modeling

---

## Overview

**Purpose:** Deterministic stage-specific loading patterns for consistent threat modeling

**Core Principles:** Deterministic loading, role separation, Work→Critic→Approval cycle, modular efficiency, explicit context management, **batched execution**

---

## ⚠️ CRITICAL: Batched Execution Protocol

### **Prevent Timeouts and Length Limits**

**MANDATORY BATCHING RULE:** Each stage MUST be executed in separate batches to prevent prompt timeouts and response length limit failures.

**Execution Pattern:**
```
Batch 1: Stage N Work Phase → Save files → STOP
Batch 2: Stage N Critic Phase → Validation → STOP
Batch 3: Stage N+1 Work Phase → Save files → STOP
[Continue pattern for all 6 stages]
```

**PROHIBITED:**
- ❌ Running multiple stages in one execution
- ❌ Combining work + critic in same response
- ❌ Attempting all 6 stages sequentially without breaks

**Each batch should:**
- Focus on ONE phase only (work OR critic, never both)
- Save all output files before ending
- Signal completion status clearly
- Stop execution after phase completes

**See automatic-mode.md for complete batching protocol.**

---

## ⚠️ CRITICAL: Incremental File Building Within Work Phases

### **The Sub-Batch Problem**

**ISSUE:** Even within a single work phase, output files can exceed tool parameter limits.

**AFFECTED STAGES:**
- **Stage 1:** Large component inventories (10,000+ lines)
- **Stage 3:** Many threats (50-200+ threats = 15,000+ lines) - MOST CRITICAL
- **Stage 6:** Comprehensive report consolidating all stages (20,000+ lines)

### **SOLUTION: Build Large Files Incrementally**

**DO NOT:**
- ❌ Attempt to write entire Stage 1/3/6 file in single `write` tool call
- ❌ Build entire file in memory then write at end
- ❌ Assume tool parameter limits won't be hit

**INSTEAD:**
```
Step 1: Create initial structure (write tool - small file)
Step 2: Add sections incrementally (search_replace - one section at a time)
Step 3: Remove END_OF_FILE marker when complete
```

### **Pattern:**

```markdown
1. write tool: Create header + first section + "---\nEND_OF_FILE"
2. search_replace: Replace "END_OF_FILE" with next section + "END_OF_FILE"
3. search_replace: Repeat for each major section
4. search_replace: Remove "---\nEND_OF_FILE" marker at end
```

### **Benefits:**
- ✅ Each tool call under parameter limits
- ✅ Progress saved incrementally (crash recovery)
- ✅ Can verify each section as added
- ✅ Debugging easier if one section fails

### **Detailed Instructions:**

**Stage 1:** See `documentation-specialist/stage-1-guide.md` - "Incremental File Building" section
**Stage 3:** See `threat-modeler/stage-3-threat-identification.md` - "MANDATORY FOR STAGE 3" section  
**Stage 6:** See `threat-modeler/stage-6-final-reporting.md` - "MANDATORY FOR STAGE 6" section

### **When to Use:**

| Stage | Incremental Building Required? | Why |
|-------|-------------------------------|-----|
| **Stage 1** | **ALWAYS** | Component inventory can be large |
| Stage 2 | Optional (use if many data flows) | Usually smaller files |
| **Stage 3** | **MANDATORY** | 50-200+ threats = largest file |
| Stage 4 | Optional | Usually smaller files |
| Stage 5 | Optional | Usually smaller files |
| **Stage 6** | **MANDATORY** | Consolidates all previous stages |

---

## ⚠️ MANDATORY PREREQUISITE: Operational Mode Selection

### **CRITICAL: Mode Selection Required Before Stage 1**

**MANDATORY:** Select mode before any stage work

**Protocol:**
1. Ask user: "Collaborative Mode (active engagement) or Automatic Mode (autonomous)?"
2. Load mode file: `modes/collaborative-mode.md` OR `modes/automatic-mode.md`
3. Confirm and proceed to Stage 1

**PROHIBITED:** Starting work without mode selection, assuming mode, skipping mode file

**Hard gate:** No Stage 1 until mode selected and loaded

---

## Stage Transition Protocol

**Purpose:** Explicit context management between stages

**Rules:**
- **UNLOAD:** Previous stage guides, unused role reminders, stage-specific frameworks
- **RETAIN:** All stage outputs, shared resources, quality-critic guide
- **LOAD:** New stage guide, new role reminder (if role changes), stage-specific frameworks

### **Stage Transitions - Quick Reference**

| Transition | Unload | Load | Key Outputs Retained |
|------------|--------|------|----------------------|
| **1→2** | None (first) | stage-2-guide | 01-system-understanding.md |
| **2→3** | Stage 1-2 guides, doc-specialist role | Stage-3 guide, threat-modeler role, frameworks | 01, 02 + DFDs |
| **3→4** | Stage-3 guide, frameworks | Stage-4 guide | 01, 03 |
| **4→5** | Stage-4 guide | Stage-5 guide | 01, 03, 04 |
| **5→6** | Stage-5 guide | Stage-6 guide, doc-specialist role/guide | ALL (01-05) |

**Always Retained:** Shared resources (confidence-calibration, output-requirements), quality-critic files, stage outputs

**Context Tips:** Aggressive unload of stage guides, lazy load frameworks (Stage 3), always retain output files, internalize terminology after Stage 2

**For detailed loading patterns, see:** `shared/loading-guide.md`

---

## Complete 6-Stage Workflow Summary

**For detailed loading patterns, see:** `shared/loading-guide.md`

### **Compact Workflow**

**Prerequisite:** Mode Selection → Load `modes/collaborative-mode.md` OR `modes/automatic-mode.md`

**Each Stage Pattern:** Work Phase → Critic Phase → Approval → Next Stage

| Stage | Lead | Key Files | Output |
|-------|------|-----------|--------|
| **1** | Doc Specialist | stage-1-guide, core-terms, confidence-calibration | 01-system-understanding.md |
| **2** | Doc Specialist | stage-2-guide, output-requirements | 02-data-flow-analysis.md + DFDs (3) |
| **3** | Threat Modeler | stage-3-guide, frameworks/quick-reference | 03-threat-identification.md |
| **4** | Threat Modeler | stage-4-guide, risk-assessment-terms | 04-risk-assessment.md |
| **5** | Threat Modeler | stage-5-guide, confidence-calibration | 05-mitigation-strategy.md |
| **6** | Both (collaborative) | stage-6-guides (both), output-requirements | 06-final-comprehensive-report.md |

**Critic Phase (All Stages):** Load quality-critic/role-reminder.md, stage-validation-guide.md, quality-assurance/core-principles.md, validation-protocol.md, approval-criteria.md

**Detailed patterns:** See `shared/loading-guide.md`

---

## Skill Assignment Matrix

| Stage | Primary Skill | Supporting Skill | Focus |
|-------|--------------|------------------|-------|
| **1** | Documentation Specialist | - | Information extraction & organization |
| **2** | Documentation Specialist | - | Data flow mapping & DFD creation |
| **3** | Threat Modeler | - | Security threat identification |
| **4** | Threat Modeler | - | Risk assessment & prioritization |
| **5** | Threat Modeler | - | Mitigation control recommendations |
| **6** | Threat Modeler | Documentation Specialist | Content + formatting |

**Quality Critic:** Validates ALL stages (no exceptions)

---

## Operational Mode Integration

**⚠️ CRITICAL:** Mode selection MUST occur BEFORE Stage 1

| Mode | File | Use Case |
|------|------|----------|
| **Collaborative** | `modes/collaborative-mode.md` | Active engagement, domain expertise available |
| **Automatic** | `modes/automatic-mode.md` | Autonomous operation, well-documented systems |

**Execution Order:**
1. **Ask user** for mode → Load mode file
2. Load workflow-guide.md
3. Begin Stage 1

**Patterns:**
- **Collaborative:** Work → Critic → **User Review** → User Approval → Next Stage
- **Automatic:** Work → Critic → Agent Decision → Next Stage (no user interaction)

**Mode controls:** User interaction patterns | **Skills control:** Work execution

**NEVER start Stage 1 before mode selection**

---

## Detailed Loading Instructions

**All stage-specific loading patterns are documented in:** `shared/loading-guide.md`

**Quick Summary:** Each stage requires role reminder + stage guide + shared resources (confidence-calibration, output-requirements, terminology). Critic phase requires quality-critic role + stage-validation-guide + QA framework files (core-principles, validation-protocol, approval-criteria).

**Use loading-guide.md for:** Complete file lists, path aliases, context management strategies, stage-specific examples

---

## Loading Pattern Mnemonics

**For Quick Reference:**

**Stages 1-2 (Documentation):**
```
DOC-SPEC + Stage Guide + Shared Resources → CRITIC
```

**Stages 3-5 (Security):**
```
THREAT-MODELER + Stage Guide + [Frameworks for S3] + Shared → CRITIC
```

**Stage 6 (Combined):**
```
THREAT-MODELER + DOC-SPEC + Stage 6 Guides + Shared → CRITIC
```

**All Stages:**
```
WORK PHASE → CRITIC PHASE → APPROVAL DECISION
```

---

## Common Loading Mistakes

| Mistake | Wrong | Correct |
|---------|-------|---------|
| **0. No Mode Selection (CRITICAL)** | Start Stage 1 immediately | Ask user → Load mode file → Confirm → Begin |
| **1. Wrong Skill** | Threat-modeler for Stage 1 | Doc-specialist for Stages 1-2, Threat-modeler for 3-5 |
| **2. Skip Critic** | Work → Next Stage | Work → Critic → Approval → Next Stage |
| **3. Missing Inputs** | Stage 3 without prior outputs | Always load prior stage outputs |
| **4. Unnecessary Files** | Load all frameworks for Stage 1 | Lazy load: frameworks only for Stage 3 |
| **5. Mixed Roles** | Doc-specialist does security analysis | Strict role separation |

---

## Workflow Verification Checklist

**Pre-Stage 1 (CRITICAL):** Mode selected by user → Mode file loaded → Confirmed

**Before Stage:** Correct skill + Stage guide + Shared resources + Prior outputs (if needed)

**After Work:** Output created → Work ended → NO self-validation → Ready for critic

**Critic Phase:** QC skills loaded → Validation performed → Issues identified → Decision made

**Before Next Stage:** Critic approval → User approval (if Collaborative) → Files saved

---

## Troubleshooting

### **Problem: "Which skill should I use for Stage X?"**
**Solution:** Consult Skill Assignment Matrix above
- Stages 1-2: Documentation Specialist
- Stages 3-5: Threat Modeler
- Stage 6: Both (collaborative)

### **Problem: "Do I need to load all framework files?"**
**Solution:** Only for Stage 3
- STRIDE, MITRE ATT&CK, Kill Chain → Stage 3 only
- Other stages don't need framework files

### **Problem: "Can I skip loading prior stage outputs?"**
**Solution:** NO - stages build on previous work
- Stage 3 requires Stage 1-2 outputs
- Stage 4 requires Stage 3 output
- Stage 5 requires Stage 3-4 outputs
- Stage 6 requires ALL prior outputs (1-5)

### **Problem: "Should I load skills for both work and critic phases at once?"**
**Solution:** NO - strict phase separation
- Work phase: Load worker skills only
- Critic phase: Load critic skills only
- Never mix worker and critic skills in same loading

---

## Complete Loading Example: Stage 1 (Collaborative)

```
1. MODE SELECTION (⚠️ MANDATORY)
   Ask user → Load modes/collaborative-mode.md → Confirm

2. WORK PHASE
   Load: doc-specialist/role-reminder + stage-1-guide + shared resources
   Execute: Documentation analysis → Output: 01-system-understanding.md

3. CRITIC PHASE
   Load: quality-critic/role-reminder + stage-validation-guide + QA framework
   Validate: Data integrity, source traceability → Present findings → User approval

4. IF APPROVED → Stage 2 (repeat pattern with stage-2 skillset)
```

**Key:** Mode loaded ONCE (controls HOW), Skills loaded PER STAGE (controls WHAT)
