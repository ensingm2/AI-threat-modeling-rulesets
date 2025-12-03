# Skills Framework Workflow Guide

**Purpose:** Deterministic skillset loading patterns for systematic threat modeling

---

## Overview

**Purpose:** Deterministic stage-specific loading patterns for consistent threat modeling

**Core Principles:** Deterministic loading, role separation, Work→Critic→Approval cycle, modular efficiency, explicit context management, **batched execution**

---

## ⚠️ CRITICAL: Concise From The Start

**Stages 1-5 are working documents. DO NOT create verbose files then trim - create concise files from the start.**

| Stage | Output Style | Self-Check |
|-------|-------------|------------|
| 1-5 | Concise tables, brief notes | No exec summary? No TOC? ≤3 sentences per item? |
| 6 | Comprehensive report | Full narratives, executive summary, stakeholder-ready |

**Why:** Verbose-then-trim wastes 40%+ tokens and creates inconsistency. See `shared/critical-rules.md` Rule #3.

---

## ⚠️ CRITICAL: Execution Protocol (Mode-Dependent)

### **Automatic Mode: ALWAYS Continuous Execution**

**In Automatic mode (with OR without Critic Review), the agent MUST:**
- Execute ALL 6 stages continuously in a single session
- NOT stop or wait for user input between stages
- Save output files after each stage, then immediately proceed to the next
- If Critic Review is enabled: perform critic analysis inline, then continue
- Continue until the final report (Stage 6) is complete

**Execution Pattern (Automatic WITHOUT Critic):**
```
Stage 1 Work → Save → Stage 2 Work → Save → ... → Stage 6 Work → Save → DONE
```

**Execution Pattern (Automatic WITH Critic):**
```
Stage 1 Work → Critic → Save → Stage 2 Work → Critic → Save → ... → Stage 6 Work → Critic → Save → DONE
```

**This is fully autonomous - NO user interaction until completion.**

---

### **Collaborative Mode: Batched Execution**

**Only Collaborative mode requires user involvement between stages:**

**Execution Pattern (Collaborative WITHOUT Critic):**
```
Batch 1: Stage N Work Phase → Save files → STOP (wait for user review)
[User reviews and approves]
Batch 2: Stage N+1 Work Phase → Save files → STOP
[Continue pattern]
```

**Execution Pattern (Collaborative WITH Critic):**
```
Batch 1: Stage N Work Phase → Save files → STOP (wait for user)
[User continues]
Batch 2: Stage N Critic Phase → Validation → STOP (wait for user)
[User reviews and approves]
Batch 3: Stage N+1 Work Phase → Save files → STOP
[Continue pattern]
```

**PROHIBITED (in Collaborative mode only):**
- ❌ Combining work + critic in same response
- ❌ Skipping user review between stages

**Each batch should:**
- Focus on ONE phase only (work OR critic, never both)
- Save all output files before ending
- Signal completion status clearly

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

**Stage 1:** See `documentation-specialist/references/stage-1-system-understanding.md` - "Incremental File Building" section
**Stage 3:** See `threat-modeler/references/stage-3-threat-identification.md` - "MANDATORY FOR STAGE 3" section  
**Stage 6:** See `threat-modeler/references/stage-6-final-reporting.md` - "MANDATORY FOR STAGE 6" section

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

## ⚠️ MANDATORY PREREQUISITE: Startup Selections

### **CRITICAL: Mode & Critic Selection Required Before Stage 1**

**MANDATORY:** BOTH selections must be asked in a SINGLE prompt before any stage work.

**📋 AUTHORITATIVE PROMPT:** See `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section for the exact script to use verbatim.

**After user responds:**
1. Load mode file: `modes/collaborative-mode.md` OR `modes/automatic-mode.md`
2. Confirm BOTH selections and proceed to Stage 1

**PROHIBITED:** 
- ❌ Starting work without BOTH selections
- ❌ Assuming preferences
- ❌ Asking questions in separate prompts (MUST be combined in single prompt)
- ❌ Asking about mode but forgetting critic review
- ❌ Using your own wording instead of the exact script from `.cursorrules`

**Hard gate:** No Stage 1 until BOTH mode AND critic preference explicitly selected

---

## Stage Transition Protocol

**Purpose:** Explicit context management between stages

**Rules:**
- **UNLOAD:** Previous stage guides, stage-specific frameworks
- **RETAIN:** All stage outputs, shared resources, quality-critic guide
- **LOAD:** New stage guide (with embedded role constraints), stage-specific frameworks

### **Stage Transitions - Quick Reference**

| Transition | Unload | Load | Key Outputs Retained |
|------------|--------|------|----------------------|
| **1→2** | None (first) | stage-2-guide | 01-system-understanding.md |
| **2→3** | Stage 1-2 guides | Stage-3 guide + frameworks | 01, 02 + JSON |
| **3→4** | Stage-3 guide, frameworks | Stage-4 guide | 01, 02, 03 |
| **4→5** | Stage-4 guide | Stage-5 guide | 01, 03, 04 |
| **5→6** | Stage-5 guide | Stage-6 guides (both) | ALL (01-05) |

**Always Retained:** Shared resources (confidence-calibration, output-requirements), quality-critic files, stage outputs

**Context Tips:** Aggressive unload of stage guides, lazy load frameworks (Stage 3), always retain output files, internalize terminology after Stage 2

---

## Complete 6-Stage Workflow Summary

### **Compact Workflow**

**Prerequisite:** Mode Selection + Critic Selection → Load `modes/collaborative-mode.md` OR `modes/automatic-mode.md`

**Each Stage Pattern (WITH Critic Review):** Work Phase → Critic Phase → Approval → Next Stage

**Each Stage Pattern (WITHOUT Critic Review - Default):** Work Phase → [User Review in Collaborative] → Next Stage

| Stage | Lead | Key Files | Output |
|-------|------|-----------|--------|
| **1** | Doc Specialist | SKILL.md + references/stage-1-guide, terminology | 01-system-understanding.md |
| **2** | Doc Specialist | SKILL.md + references/stage-2-guide, output-requirements | 02-data-flow-analysis.md + JSON |
| **3** | Threat Modeler | SKILL.md + references/stage-3-guide, frameworks | 03-threat-identification.md |
| **4** | Threat Modeler | SKILL.md + references/stage-4-guide, terminology | 04-risk-assessment.md |
| **5** | Threat Modeler | SKILL.md + references/stage-5-guide, confidence | 05-mitigation-strategy.md |
| **6** | Both | SKILL.md + references/stage-6-guides (both) | 00-final-report.md |

**Critic Phase (If Enabled):** Load quality-critic/SKILL.md + references/stage-validation-guide.md

---

## Skill Assignment Matrix

| Stage | Primary Skill | Supporting Skill | Focus |
|-------|--------------|------------------|-------|
| **1** | Documentation Specialist | - | Information extraction & organization |
| **2** | Documentation Specialist | - | Data flow mapping & analysis |
| **3** | Threat Modeler | - | Security threat identification |
| **4** | Threat Modeler | - | Risk assessment & prioritization |
| **5** | Threat Modeler | - | Mitigation control recommendations |
| **6** | Threat Modeler | Documentation Specialist | Content + formatting |

**Quality Critic:** Validates ALL stages (no exceptions)

---

## Operational Mode Integration

**⚠️ CRITICAL:** Mode AND Critic selection MUST occur BEFORE Stage 1

| Mode | File | Use Case |
|------|------|----------|
| **Collaborative** | `modes/collaborative-mode.md` | Active engagement, domain expertise available |
| **Automatic** | `modes/automatic-mode.md` | Autonomous operation, well-documented systems |

| Critic Setting | Use Case |
|----------------|----------|
| **Enabled** | Multi-agent setups, maximum rigor required |
| **Disabled (Default)** | Single-agent runs, efficiency prioritized |

**Execution Order:**
1. **Ask user** for mode → Ask user about critic review
2. Load mode file
3. Load workflow-guide.md
4. Begin Stage 1

**Patterns (WITH Critic Review):**
- **Collaborative:** Work → STOP → Critic → STOP → User Review → User Approval → Next Stage
- **Automatic:** Work → Critic → Agent Decision → Next Stage (NO stopping, fully autonomous)

**Patterns (WITHOUT Critic Review - Default):**
- **Collaborative:** Work → STOP → User Review → User Approval → Next Stage
- **Automatic:** Work → Next Stage (NO stopping, fully autonomous)

**Key Distinction:** Automatic mode NEVER stops for user input. Only Collaborative mode involves user interaction.

**Mode controls:** User interaction patterns | **Critic controls:** Validation overhead | **Skills control:** Work execution

**NEVER start Stage 1 before both selections made**

---

## ⚠️ MANDATORY: Complete Source File Review (Before Stage 1)

### **ALL User-Provided Source Files MUST Be Read**

**CRITICAL:** Before beginning Stage 1 analysis, you MUST identify and read EVERY contextual file provided by the user.

**Required Sequence:**
```
1. IDENTIFY: Determine all files/directories the user has provided as context
2. ENUMERATE: List ALL files in any provided directories (recursive if needed)
3. COUNT: Document total number of source files
4. READ EACH: Open and read EVERY file completely - no exceptions
5. VERIFY: Confirm 100% coverage before proceeding
6. DOCUMENT: Include ALL files in Stage 1 Source Documentation table
```

**Why This Is Critical:**
- Security-relevant context may exist in ANY source file
- Skipping files leads to incomplete threat identification
- All stages depend on complete Stage 1 understanding
- Evidence traceability requires knowing all available sources

**Verification Check (Before Starting Stage 1 Work):**
- [ ] All user-provided sources identified
- [ ] Directory listings performed for all provided directories
- [ ] Total file count known
- [ ] EVERY file read completely
- [ ] No files skipped or summarized from filename only

**If a file cannot be read:** Document the reason explicitly and get user approval to proceed.

---

## Detailed Loading by Stage

### **Stage 1: System Understanding**
```
LOAD:
├── documentation-specialist/SKILL.md
├── documentation-specialist/references/stage-1-system-understanding.md
├── shared/terminology.md
└── shared/confidence-calibration.md

THEN (Before Analysis):
├── IDENTIFY all user-provided source files/directories
├── ENUMERATE all files in provided directories
└── READ EVERY provided file (MANDATORY - no exceptions)
```

### **Stage 2: Data Flow Analysis**
```
LOAD:
├── documentation-specialist/SKILL.md (if not loaded)
├── documentation-specialist/references/stage-2-data-flow-analysis.md
├── shared/terminology.md (if not loaded)
└── shared/output-file-requirements.md
```

### **Stage 3: Threat Identification**
```
LOAD:
├── threat-modeler/SKILL.md
├── threat-modeler/references/stage-3-threat-identification.md
├── threat-modeler/references/frameworks/quick-reference.md
└── shared/terminology.md (if not loaded)
```

### **Stage 4: Risk Assessment**
```
LOAD:
├── threat-modeler/SKILL.md (if not loaded)
├── threat-modeler/references/stage-4-risk-assessment.md
└── shared/confidence-calibration.md (if not loaded)
```

### **Stage 5: Mitigation Strategy**
```
LOAD:
├── threat-modeler/SKILL.md (if not loaded)
├── threat-modeler/references/stage-5-mitigation-strategy.md
└── shared/confidence-calibration.md (if not loaded)
```

### **Stage 6: Final Report**
```
LOAD:
├── threat-modeler/SKILL.md (if not loaded)
├── threat-modeler/references/stage-6-final-reporting.md
├── documentation-specialist/references/stage-6-report-formatting.md
└── shared/output-file-requirements.md
```

### **Critic Phase (If Enabled)**
```
LOAD (only if Critic Review mode enabled):
├── quality-critic/SKILL.md
├── quality-critic/references/core-principles.md    # All protocols consolidated here
└── quality-critic/references/stage-validation-guide.md

OPTIONAL:
└── quality-critic/references/examples.md           # Reference examples if needed

SAVE (MANDATORY - BOTH files after critic analysis):
├── {stage-number}.5-critic-review.md                   # Human-readable review (e.g., 01.5-critic-review.md)
└── ai-working-docs/{stage-number}.5-critic-review.json # AI working doc for subsequent stages
```

**Critic Review Output:** After completing critic analysis, ALWAYS save findings to BOTH:
1. `{stage-number}.5-critic-review.md` - Human-readable markdown for review and audit (e.g., `01.5-critic-review.md`)
2. `ai-working-docs/{stage-number}.5-critic-review.json` - Structured JSON for AI context transfer

**Naming Convention:** The `.5` suffix ensures critic reviews sort immediately after their corresponding stage (e.g., `01-system-understanding.md` followed by `01.5-critic-review.md`).

These files are loaded by subsequent stages to inform their analysis.

**If Critic Review disabled:** Skip this phase entirely, proceed to next stage (or user review in Collaborative mode)

---

## Stage Input Loading (AI Working Docs)

**Prefer JSON for AI-to-AI context:**

| Stage | Primary Inputs (JSON) | Fallback (Markdown) |
|-------|----------------------|---------------------|
| **2** | `ai-working-docs/01-*.json` | `01-system-understanding.md` |
| **3** | `ai-working-docs/01-*.json`, `02-*.json` | `01-*.md`, `02-*.md` |
| **4** | `ai-working-docs/01-*.json`, `02-*.json`, `03-threats.json` | `01-03-*.md` |
| **5** | `ai-working-docs/01-*.json`, `03-threats.json`, `04-risk-assessments.json` | `01-04-*.md` |
| **6** | All `ai-working-docs/*.json` | All `*.md` files |

### Critic Review Inputs (When Critic Mode Enabled)

**MANDATORY:** Load prior critic reviews to inform current stage analysis:

| Stage | Critic Review Inputs |
|-------|---------------------|
| **2** | `01.5-critic-review.json` |
| **3** | `01.5-critic-review.json`, `02.5-critic-review.json` |
| **4** | `01.5-critic-review.json`, `02.5-critic-review.json`, `03.5-critic-review.json` |
| **5** | All prior `*.5-critic-review.json` files |
| **6** | All `*.5-critic-review.json` files |

**Usage:** Check `carry_forward_notes` and `issues_identified` from prior critic reviews to inform current stage work.

---

## Path Shortcuts

| Shortcut | Path |
|----------|------|
| `@doc` | documentation-specialist/SKILL.md |
| `@tm` | threat-modeler/SKILL.md |
| `@qc` | quality-critic/SKILL.md |
| `@s1` | documentation-specialist/references/stage-1-system-understanding.md |
| `@s2` | documentation-specialist/references/stage-2-data-flow-analysis.md |
| `@s3` | threat-modeler/references/stage-3-threat-identification.md |
| `@s4` | threat-modeler/references/stage-4-risk-assessment.md |
| `@s5` | threat-modeler/references/stage-5-mitigation-strategy.md |
| `@s6` | threat-modeler/references/stage-6-final-reporting.md |
| `@critic` | quality-critic/references/stage-validation-guide.md |
| `@principles` | quality-critic/references/core-principles.md |
| `@terms` | shared/terminology.md |
| `@conf` | shared/confidence-calibration.md |
| `@output` | shared/output-file-requirements.md |
| `@rules` | shared/critical-rules.md |

---

## Loading Pattern Mnemonics

**For Quick Reference:**

**Stages 1-2 (Documentation):**
```
Stage Guide + Shared → CRITIC
```

**Stages 3-5 (Security):**
```
Stage Guide + [Frameworks for S3] + Shared → CRITIC
```

**Stage 6 (Combined):**
```
Stage 6 Guides (both) + Shared → CRITIC
```

**All Stages:**
```
WORK PHASE → CRITIC PHASE → APPROVAL DECISION
```

---

## Common Loading Mistakes

| Mistake | Wrong | Correct |
|---------|-------|---------|
| **0. No Startup Selections (CRITICAL)** | Start Stage 1 immediately | Ask user for mode + critic preference → Confirm → Begin |
| **1. Wrong Skill** | Threat-modeler for Stage 1 | Doc-specialist for Stages 1-2, Threat-modeler for 3-5 |
| **2. Skip Critic When Enabled** | Work → Next Stage (with critic ON) | Work → Critic → Approval → Next Stage |
| **3. Run Critic When Disabled** | Work → Critic (with critic OFF) | Work → [User Review] → Next Stage |
| **4. Missing Inputs** | Stage 3 without prior outputs | Always load prior stage outputs |
| **5. Unnecessary Files** | Load all frameworks for Stage 1 | Lazy load: frameworks only for Stage 3 |
| **6. Mixed Roles** | Doc-specialist does security analysis | Strict role separation |

---

## Workflow Verification Checklist

**Pre-Stage 1 (CRITICAL):** Mode selected → Critic preference selected → Mode file loaded → Confirmed

**Before Stage:** Stage guide + Shared resources + Prior outputs (if needed)

**After Work:** Output created → Work ended → Files saved

**If Critic Enabled:** QC skills loaded → Validation performed → Issues identified → Decision made

**If Critic Disabled:** Skip critic phase entirely

**Before Next Stage:** [Critic approval if enabled] → User approval (if Collaborative) → Proceed

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

## Complete Loading Example: Stage 1 (Collaborative, No Critic)

```
1. STARTUP SELECTIONS (⚠️ MANDATORY)
   Use EXACT prompt from .cursorrules → "MANDATORY STARTUP SELECTIONS"
   → User responds with both selections
   → Load modes/collaborative-mode.md
   → Confirm BOTH selections

2. WORK PHASE
   Load: documentation-specialist/references/stage-1-system-understanding.md + shared resources
   Execute: Documentation analysis → Output: 01-system-understanding.md

3. USER REVIEW (Critic disabled)
   Present output to user → User provides feedback → User approves

4. IF APPROVED → Stage 2 (repeat pattern with stage-2 skillset)
```

## Complete Loading Example: Stage 1 (Collaborative, With Critic)

```
1. STARTUP SELECTIONS (⚠️ MANDATORY)
   Use EXACT prompt from .cursorrules → "MANDATORY STARTUP SELECTIONS"
   → User responds with both selections
   → Load modes/collaborative-mode.md
   → Confirm BOTH selections

2. WORK PHASE
   Load: documentation-specialist/references/stage-1-system-understanding.md + shared resources
   Execute: Documentation analysis → Output: 01-system-understanding.md

3. CRITIC PHASE (Critic enabled)
   Load: quality-critic/stage-validation-guide.md + QA framework
   Validate: Data integrity, source traceability → Present findings

4. USER REVIEW
   User reviews work AND critic findings → User approves

5. IF APPROVED → Stage 2 (repeat pattern with stage-2 skillset)
```

**Key:** Use exact startup prompt from `.cursorrules`, Skills loaded PER STAGE
