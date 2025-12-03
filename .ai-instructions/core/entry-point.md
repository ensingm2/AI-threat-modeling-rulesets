# Threat Modeling Framework - Central Entry Point

**Platform:** Multi-platform (Cursor, GitHub Copilot, Aider)

---

## 🎯 Framework Overview

Provides systematic, evidence-based threat modeling using:
- **6-Stage Workflow:** System Understanding → Data Flow → Threats → Risk → Mitigation → Final Report
- **Multiple Frameworks:** STRIDE + MITRE ATT&CK + Cyber Kill Chain
- **Quality Assurance:** Mandatory adversarial critic review after each stage
- **Evidence-Based:** All claims traced to source documentation with confidence levels

---

## 📁 Project Structure

```
.ai-instructions/
├── core/entry-point.md           # THIS FILE - Start here
├── modes/                        # Collaborative vs Automatic mode behaviors
├── skills/
│   ├── workflow-guide.md         # CANONICAL: Stage execution patterns
│   ├── documentation-specialist/ # Stages 1, 2, 6
│   ├── threat-modeler/           # Stages 3, 4, 5, 6
│   ├── quality-critic/           # All stages (validation)
│   └── shared/                   # Cross-stage resources
└── targets/                      # Security research targets
```

---

## 🚀 Quick Start

### Step 1: Load Framework
1. Read `skills/README.md` - Skills overview
2. Read `skills/workflow-guide.md` - Stage execution patterns

### Step 2: MANDATORY Startup Selections (BOTH REQUIRED)

**⚠️ CRITICAL: You MUST ask BOTH questions in a single prompt before beginning Stage 1.**

**📋 AUTHORITATIVE PROMPT:** See `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section for the exact script to use verbatim. This includes the required disclaimer about multi-agent vs single-agent value.

**After user responds:**
1. **Load:** `modes/collaborative-mode.md` OR `modes/automatic-mode.md`
2. **Confirm** BOTH selections before proceeding to Stage 1

**PROHIBITED:**
- ❌ Starting Stage 1 without asking about operational mode
- ❌ Starting Stage 1 without asking about critic review mode  
- ❌ Assuming either preference without explicit user selection
- ❌ Using your own wording instead of the exact script from `.cursorrules`

### Step 3: Review ALL User-Provided Source Files (MANDATORY)

**⚠️ BEFORE beginning Stage 1 analysis:**
1. **Identify:** Determine all files/directories the user has provided as context
2. **Enumerate:** List ALL files in any provided directories (recursive if needed)
3. **Read EVERY file:** No exceptions - open and read each file completely
4. **Verify coverage:** Confirm 100% of source files have been read
5. **Document:** Include ALL files in Stage 1 Source Documentation table

**Prohibited:**
- ❌ Starting analysis before reading ALL provided source files
- ❌ Skipping files that "seem irrelevant"
- ❌ Assuming file contents from filename alone
- ❌ Assuming you know what files exist without listing directories

### Step 4: Execute 6-Stage Workflow
Follow `workflow-guide.md` for stage-by-stage loading patterns.

---

## ❌ Critical Rules

**Full details:** `skills/shared/critical-rules.md`

| Rule | Summary |
|------|---------|
| **Mode First** | Ask user for mode BEFORE Stage 1 |
| **Critic Selection** | Ask user about Critic Review mode at startup (default: OFF) |
| **Read ALL Source Files** | Identify and read EVERY user-provided contextual file before Stage 1 analysis |
| **Concise From Start** | Stages 1-5: tables, ≤3 sentences/item. NO verbose-then-trim. Stage 6 = comprehensive |
| **Never Fabricate** | All claims need sources; use confidence levels |
| **Batched Execution** | One phase per response (Work OR Critic) |
| **Role Separation** | Workers create, critics validate - never combined |

---

## 🎭 Skills Framework

| Skill | Stages | Role |
|-------|--------|------|
| **Documentation Specialist** | 1, 2, 6 (support) | Information extraction, documentation |
| **Threat Modeler** | 3, 4, 5, 6 | Security analysis, risk, mitigations |
| **Quality Critic** | All (validation) | Adversarial quality validation |

**Loading pattern:** SKILL.md + stage guide + shared resources → Critic validation

**Details:** `skills/README.md` and `skills/workflow-guide.md`

---

## 📚 Key Resources

All paths relative to `skills/`:

| Resource | File | When to Load |
|----------|------|--------------|
| **Workflow** | `workflow-guide.md` | Always (canonical reference) |
| **Critical Rules** | `shared/critical-rules.md` | Always |
| **Terminology** | `shared/terminology.md` | Stages 1-2, as needed |
| **Confidence** | `shared/confidence-calibration.md` | All stages |
| **Output Specs** | `shared/output-file-requirements.md` | All stages |
| **Frameworks** | `threat-modeler/references/frameworks/quick-reference.md` | Stage 3 |
| **Critic Protocols** | `quality-critic/references/core-principles.md` | Critic phases |

---

## 📊 Stage Outputs

**Location:** `[target]/output/threat-model/`

| Stage | Output File |
|-------|-------------|
| 1 | `01-system-understanding.md` + `ai-working-docs/01-*.json` |
| 2 | `02-data-flow-analysis.md` + `ai-working-docs/02-*.json` |
| 3 | `03-threat-identification.md` + `ai-working-docs/03-threats.json` |
| 4 | `04-risk-assessment.md` + `ai-working-docs/04-*.json` |
| 5 | `05-mitigation-strategy.md` + `ai-working-docs/05-*.json` |
| 6 | `06-final-comprehensive-report.md` |

**Specs:** `shared/output-file-requirements.md`

---

## 🔧 External Resource Access

**Permitted (with user approval):** Official docs, CVE databases, compliance standards, academic research

**Prohibited:** Direct system interaction, vulnerability exploitation, live probing

**Protocol:** Request approval → Justify need → Specify sources → Proceed after approval

**Fallback:** Use qualitative assessment with explicit data gap documentation

---

## 🌐 Platform Notes

| Platform | Loader | Notes |
|----------|--------|-------|
| **Cursor** | `.cursorrules` (auto) | Full workspace context |
| **GitHub Copilot** | `.github/copilot-instructions.md` | Limited file reading |
| **Aider** | Manual loading | Explicit file reading required |

---

## ✅ Getting Started Checklist

- [ ] Entry point loaded (this file)
- [ ] `skills/workflow-guide.md` loaded
- [ ] Target selected from `targets/` directory
- [ ] **User asked for BOTH selections in single prompt:**
  - [ ] Operational mode (Collaborative or Automatic)
  - [ ] Critic review mode (With Critic or Without Critic)
- [ ] Mode file loaded and confirmed
- [ ] BOTH selections confirmed before proceeding
- [ ] **ALL user-provided source files reviewed:**
  - [ ] All provided directories enumerated
  - [ ] EVERY provided file read completely
  - [ ] 100% coverage verified
- [ ] Ready to begin Stage 1

---

*Framework by Mike Ensing (ensingm2@gmail.com) | OWASP 2025 Global AppSec USA*
