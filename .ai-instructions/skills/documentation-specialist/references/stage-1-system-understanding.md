# Stage 1: System Understanding | Documentation Specialist

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 1 work complete. Ready for critic analysis."

---

## ⚠️ STOP: Prerequisite Check - Operational Mode Selection

**BEFORE proceeding with Stage 1 work, verify:**
- [ ] User has been asked which operational mode to use (Collaborative or Automatic)
- [ ] Mode file has been loaded
- [ ] Mode selection has been confirmed

**This is a hard gate - NO Stage 1 work without mode selection.**

---

## ⚠️ CRITICAL: Concise From The Start

**Stage 1 is a WORKING DOCUMENT, not a final report. DO NOT create verbose output then trim - create concise output from the start.**

| ❌ PROHIBITED | ✅ REQUIRED |
|---------------|-------------|
| Executive Summary | Tables over prose |
| Table of Contents | ≤3 sentences per component |
| Methodology sections | Brief confidence (1 sentence) |
| Multi-paragraph descriptions | Scale to system complexity |
| "Introduction" or "Overview" sections | Get straight to content |

**Self-check before saving:**
- [ ] No executive summary or TOC?
- [ ] Using tables not prose lists?
- [ ] Each component/boundary ≤3 sentences?
- [ ] No methodology explanations?

**Stage 6 is where elaboration belongs. Keep Stage 1 lean.**

---

## Stage 1 Purpose

Extract and organize factual architectural information from source documentation. You are NOT performing security analysis - that comes in Stage 3+.

**Inputs:**
- All provided source documentation (code, configs, READMEs, interviews, external docs)
- External documentation referenced in sources (query as needed with user approval)

**Outputs:**
- **AI Working Docs:** `ai-working-docs/01-components.json`, `01-trust-boundaries.json`, `01-data-assets.json`, `01-assumptions.json`
- **Human-Readable:** `01-system-understanding.md`

**Your Mission:**
- Read and comprehend all provided documentation
- Extract factual architectural information into structured tables
- Document what is known vs. unknown
- Create concise, well-organized output

**⚠️ COLLABORATIVE MODE:** Always ask user for clarification BEFORE making assumptions.

---

## Required Output Structure

```markdown
# Stage 1: System Understanding
**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## 1. Source Documentation
| File | Type | Key Content |
|------|------|-------------|
| [filename] | [README/Config/Code/etc] | [Brief description] |

**Documentation Quality:** [HIGH/MEDIUM/LOW] - [1 sentence reason]

## 2. System Description
**Business Purpose:** [1-2 sentences]
**Primary Users:** [List]
**Key Functionality:** [Bullet list]
**Source:** [filename, lines]

## 3. Component Inventory
| Component | Type | Function | Technology | Data Handled | Confidence |
|-----------|------|----------|------------|--------------|------------|
| [Name] | [App/DB/API/etc] | [Brief] | [Documented/Unknown] | [Types] | [H/M/L] |

## 4. Trust Boundaries
| Boundary | Type | Separates | Auth Required | Source |
|----------|------|-----------|---------------|--------|
| [Name] | [Network/Privilege/etc] | [A] ↔ [B] | [Yes/No/Unknown] | [file, line] |

## 5. Data Assets
| Asset | Type | Sensitivity | Regulatory | Storage |
|-------|------|-------------|------------|---------|
| [Name] | [PII/Creds/etc] | [Public/Internal/Confidential/Restricted] | [GDPR/PCI/etc or N/A] | [Components] |

## 6. Analysis Scope
**In-Scope:** [List with brief justifications]
**Out-of-Scope:** [List with brief justifications]

## 7. Assumptions
| # | Assumption | Basis | Confidence | Impact if Wrong |
|---|------------|-------|------------|-----------------|
| 1 | [Statement] | [Evidence] | [M/L] | [Brief impact] |

## 8. Documentation Gaps
| Gap | Severity | Impact | Workaround |
|-----|----------|--------|------------|
| [Missing info] | [Critical/Significant/Minor] | [How it affects analysis] | [How to proceed] |

**Overall Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence summary]
```

---

## Workflow Steps

### Step 1: Survey Documentation
Scan all files, categorize by type (README, config, code, etc.)

### Step 2: Extract System Description
Business purpose, users, functionality - with source references

### Step 3: Build Component Inventory Table
For each component: name, type, function, technology (documented vs unknown), data handled

### Step 4: Identify Trust Boundaries Table
Network, process, privilege boundaries with authentication requirements

### Step 5: Catalog Data Assets Table
Data types, sensitivity, regulatory implications, storage locations

### Step 6: Define Scope
In-scope vs out-of-scope with brief justifications

### Step 7: Document Assumptions Table
All assumptions with basis, confidence level, impact if wrong

### Step 8: Identify Gaps Table
Missing information categorized by severity

---

## Quality Rules

- **Every claim needs a source reference** (file, line number)
- **Technology = Documented/Inferred/Unknown** (never fabricate)
- **No fabricated metrics** (user counts, revenue, transaction volumes)
- **Assumptions need confidence levels** (MEDIUM or LOW only - HIGH requires documentation)
- **Tables over prose** where equivalent information

---

## Completion Signal

```
✅ STAGE 1 WORK PHASE COMPLETE
- Output File: 01-system-understanding.md
- Components: [N] | Trust Boundaries: [N] | Assumptions: [N]
- Location: [target]/output/threat-model/
- Overall Confidence: [HIGH/MEDIUM/LOW]
```

---
