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

**Exceptions - Allow More Detail For:**
- **Business Purpose:** 2-4 sentences to capture value proposition, market context, and why security matters
- **Primary Users:** Brief description of each user type's role and access level (not just names)
- **Assumptions:** 2-3 sentences per assumption explaining the reasoning and security implications

**Self-check before saving:**
- [ ] No executive summary or TOC?
- [ ] Using tables not prose lists?
- [ ] Each component/boundary ≤3 sentences?
- [ ] No methodology explanations?
- [ ] Business Purpose provides sufficient context?
- [ ] Assumptions explain rationale, not just state facts?

**Stage 6 is where elaboration belongs. Keep Stage 1 lean, but ensure key context is captured.**

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

## ⚠️ MANDATORY: Complete Source File Review

**CRITICAL: You MUST identify and read EVERY contextual file provided by the user before proceeding with analysis.**

### Required Steps (Non-Negotiable):

**Step 0a: Identify ALL User-Provided Sources**
```
1. Determine what files/directories the user has provided as context
2. List ALL files in any provided directories (recursive if needed)
3. Count total files across all provided sources
4. Create checklist of ALL files to read
```

**Step 0b: Read EVERY File**
```
For EACH user-provided file:
  - Open and read the complete file
  - Extract relevant information
  - Note key security-relevant details
  - Check off from enumeration list
```

**Step 0c: Verify Complete Coverage**
```
Before proceeding to analysis:
  - Confirm all files from enumeration are checked off
  - Document any files that couldn't be read (with reason)
  - 100% coverage required to proceed
```

### Prohibited:
- ❌ Starting analysis before enumerating all provided files
- ❌ Skipping files that "seem irrelevant"
- ❌ Reading file summaries instead of full content
- ❌ Assuming file contents based on filename
- ❌ Proceeding with <100% file coverage without explicit user approval
- ❌ Assuming you know what files exist without explicitly listing directories

### Source Documentation Table Must Include:
EVERY user-provided file MUST appear in the Source Documentation table, with:
- Exact filename and path
- File type classification
- Key content summary (proving it was actually read)

**Hard Gate:** Stage 1 is INCOMPLETE if any user-provided source file is missing from documentation.

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
**Business Purpose:** [2-4 sentences covering: what the system does, who it serves, why it matters, and key security considerations]

**Primary Users:**
| User Type | Role | Access Level | Security Relevance |
|-----------|------|--------------|-------------------|
| [Type] | [What they do] | [What they can access] | [Why they matter for security] |

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
| 1 | [Statement] | [Evidence/reasoning - 1-2 sentences] | [M/L] | [Security implications - 1-2 sentences] |

*Note: Assumptions should explain WHY you believe something and WHAT security impact results if wrong.*

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
