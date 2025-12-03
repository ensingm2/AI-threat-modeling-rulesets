# Output File Requirements

**Purpose:** Standardized output file specifications for all threat modeling stages  
**Scope:** Universal file format, naming, and content requirements  

---

## ⚠️ CRITICAL: Concise From The Start

**DO NOT create verbose stage files and trim later. Create concise files from the start.**

### Why This Matters
- Verbose-then-trim wastes tokens (40%+ overhead)
- Creates inconsistency between original and trimmed versions
- Trimming risks removing important information
- Stages 1-5 are **working documents**, not final reports

### The Rule
| Stage | Output Style | Elaboration Level |
|-------|-------------|-------------------|
| **1-5** | Concise working docs | Tables, brief notes, IDs for cross-reference |
| **6** | Comprehensive report | Full narratives, executive summary, stakeholder-ready |

**Stage 6 is where elaboration belongs.** All prior stages should be minimal, structured, and reference-focused.

---

## Dual Output Strategy

Each stage produces **two types of output**:

1. **AI Working Documents (Primary for AI-to-AI):** Structured JSON files for precise data transfer between stages
2. **Human-Readable Markdown (Primary for humans):** Traditional markdown files for review and stakeholder communication

### Directory Structure

```
[target-directory]/output/threat-model/
├── 01-system-understanding.md
├── 01.5-critic-review.md              # Critic mode only (human-readable) - ".5" for sorting after stage
├── 02-data-flow-analysis.md
├── 02.5-critic-review.md              # Critic mode only (human-readable)
├── 03-threat-identification.md
├── 03.5-critic-review.md              # Critic mode only (human-readable)
├── 04-risk-assessment.md
├── 04.5-critic-review.md              # Critic mode only (human-readable)
├── 05-mitigation-strategy.md
├── 05.5-critic-review.md              # Critic mode only (human-readable)
├── 00-final-report.md
├── 06.5-critic-review.md              # Critic mode only (human-readable)
└── ai-working-docs/
    ├── 01-components.json
    ├── 01-trust-boundaries.json
    ├── 01-data-assets.json
    ├── 01-assumptions.json
    ├── 01.5-critic-review.json        # Critic mode only (AI working doc) - ".5" for sorting
    ├── 02-data-flows.json
    ├── 02-attack-surfaces.json
    ├── 02.5-critic-review.json        # Critic mode only (AI working doc)
    ├── 03-threats.json
    ├── 03.5-critic-review.json        # Critic mode only (AI working doc)
    ├── 04-risk-assessments.json
    ├── 04.5-critic-review.json        # Critic mode only (AI working doc)
    ├── 05-mitigations.json
    ├── 05.5-critic-review.json        # Critic mode only (AI working doc)
    └── 06.5-critic-review.json        # Critic mode only (AI working doc)
```

### Input Priority for AI Stages

When loading context from previous stages:
1. **Primary:** Load structured JSON from `ai-working-docs/`
2. **Fallback:** If JSON unavailable, parse from markdown files

---

## AI Working Documents (`ai-working-docs/`)

### Stage 1 Outputs

**`01-components.json`**
```json
{
  "components": [
    {
      "id": "C-001",
      "name": "Component Name",
      "type": "service|database|external|user|...",
      "technology": "documented|inferred|unknown",
      "technology_details": "Optional specifics if documented",
      "data_handled": ["list", "of", "data", "types"],
      "source_reference": "file:line or document section",
      "confidence": "HIGH|MEDIUM|LOW"
    }
  ]
}
```

**`01-trust-boundaries.json`**
```json
{
  "trust_boundaries": [
    {
      "id": "TB-001",
      "name": "Boundary Name",
      "description": "Brief description",
      "components_inside": ["C-001", "C-002"],
      "components_outside": ["C-003"],
      "security_controls": ["auth", "encryption", "..."],
      "source_reference": "file:line"
    }
  ]
}
```

**`01-data-assets.json`**
```json
{
  "data_assets": [
    {
      "id": "DA-001",
      "name": "Asset Name",
      "sensitivity": "HIGH|MEDIUM|LOW",
      "classification": "PII|financial|credentials|...",
      "regulations": ["GDPR", "PCI-DSS", "..."],
      "storage_locations": ["C-001", "C-002"],
      "source_reference": "file:line"
    }
  ]
}
```

**`01-assumptions.json`**
```json
{
  "assumptions": [
    {
      "id": "A-001",
      "statement": "Assumption text",
      "confidence": "HIGH|MEDIUM|LOW",
      "impact_if_wrong": "Brief impact statement",
      "validation_method": "How to verify"
    }
  ]
}
```

### Stage 2 Outputs

**`02-data-flows.json`**
```json
{
  "data_flows": [
    {
      "id": "DF-001",
      "source_component": "C-001",
      "destination_component": "C-002",
      "data_elements": ["DA-001", "DA-002"],
      "protocol": "HTTPS|gRPC|unknown|...",
      "crosses_boundary": "TB-001|null",
      "authentication": "yes|no|unknown",
      "encryption": "yes|no|unknown",
      "source_reference": "file:line"
    }
  ]
}
```

**`02-attack-surfaces.json`**
```json
{
  "attack_surfaces": [
    {
      "id": "AS-001",
      "name": "Surface Name",
      "type": "API|UI|network|...",
      "component": "C-001",
      "entry_flows": ["DF-001", "DF-002"],
      "authentication_required": "yes|no|unknown",
      "exposure": "public|internal|partner"
    }
  ]
}
```

### Stage 3 Outputs

**`03-threats.json`**
```json
{
  "threats": [
    {
      "id": "T-001",
      "name": "Threat Name",
      "description": "Brief description",
      "stride_category": "Spoofing|Tampering|Repudiation|Information Disclosure|Denial of Service|Elevation of Privilege",
      "affected_components": ["C-001", "C-002"],
      "affected_flows": ["DF-001"],
      "attack_surface": "AS-001",
      "mitre_attack": {
        "tactic": "Initial Access|...",
        "technique_id": "T1078",
        "technique_name": "Valid Accounts"
      },
      "kill_chain_stage": "Reconnaissance|Weaponization|Delivery|Exploitation|Installation|C2|Actions",
      "preliminary_rating": "CRITICAL|HIGH|MEDIUM|LOW",
      "confidence": "HIGH|MEDIUM|LOW"
    }
  ]
}
```

### Stage 4 Outputs

**`04-risk-assessments.json`**
```json
{
  "risk_assessments": [
    {
      "threat_id": "T-001",
      "risk_rating": "CRITICAL|HIGH|MEDIUM|LOW",
      "impact": {
        "confidentiality": "HIGH|MEDIUM|LOW|NONE",
        "integrity": "HIGH|MEDIUM|LOW|NONE",
        "availability": "HIGH|MEDIUM|LOW|NONE",
        "business": "Brief business impact"
      },
      "likelihood": {
        "rating": "HIGH|MEDIUM|LOW",
        "factors": ["complexity", "access_required", "existing_controls"]
      },
      "justification": "Brief justification for rating",
      "confidence": "HIGH|MEDIUM|LOW",
      "data_gaps": ["List of missing information affecting assessment"]
    }
  ]
}
```

### Stage 5 Outputs

**`05-mitigations.json`**
```json
{
  "mitigations": [
    {
      "id": "M-001",
      "name": "Control Name",
      "description": "Brief description",
      "addresses_threats": ["T-001", "T-002"],
      "control_type": "preventive|detective|corrective",
      "implementation": {
        "effort": "LOW|MEDIUM|HIGH",
        "phase": "immediate|short-term|long-term",
        "dependencies": ["M-002"],
        "guidance": "Implementation guidance"
      },
      "effectiveness": "complete|substantial|partial|minimal",
      "residual_risk": "Brief residual risk statement"
    }
  ]
}
```

---

## Critic Review Files (When Critic Mode Enabled)

**Purpose:** Persist critic findings for use in subsequent stages as additional context.

**When to Create:** Only when Critic Review mode is enabled at startup.

**Dual Output (Same as Stage Files):**
1. **Human-Readable Markdown:** `{stage-number}.5-critic-review.md` - For human review and audit trail (e.g., `01.5-critic-review.md`)
2. **AI Working Document:** `ai-working-docs/{stage-number}.5-critic-review.json` - For AI-to-AI context transfer

**Naming Convention:** The `.5` suffix ensures critic reviews sort immediately after their corresponding stage output (e.g., `01-system-understanding.md` followed by `01.5-critic-review.md`).

### Critic Review Markdown Template

**`{stage-number}.5-critic-review.md`**
```markdown
# Stage [N] Critic Review

**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Automatic/Collaborative]

## Review Summary

| Metric | Value |
|--------|-------|
| Approval Status | [CONFIDENT_APPROVAL / CONDITIONAL / TARGETED_REVISION / MAJOR_REWORK] |
| Confidence | [X%] |
| Average Score | [X.X/5.0] |
| Issues Found | [N] |

## Issues Identified

| ID | Severity | Category | Description | Affected Items |
|----|----------|----------|-------------|----------------|
| CR-001 | HIGH/MED/LOW | [category] | [Brief description] | [IDs] |

### Issue Details

#### CR-001: [Issue Title]
**Severity:** [HIGH/MEDIUM/LOW] | **Category:** [data_integrity/methodology/completeness/traceability/stakeholder_utility]
**Description:** [What the issue is]
**Affected Items:** [Component/flow/threat IDs]
**Recommended Action:** [What should be done]

## Challenges Applied

| Challenge Type | Finding |
|----------------|---------|
| Data Integrity | [Finding] |
| Completeness | [Finding] |
| Methodology | [Finding] |
| Stakeholder Utility | [Finding] |

## Multi-Dimensional Scores

| Dimension | Score | Justification |
|-----------|-------|---------------|
| Data Integrity | [1-5] | [Brief justification] |
| Methodological Rigor | [1-5] | [Brief justification] |
| Source Traceability | [1-5] | [Brief justification] |
| Analytical Depth | [1-5] | [Brief justification] |
| Stakeholder Utility | [1-5] | [Brief justification] |

## Adversarial Questions

1. **Security expert challenge:** [Response]
2. **Information gaps:** [Response]
3. **Assumption vulnerabilities:** [Response]

## Carry-Forward Notes

> Notes below should inform subsequent stages of the threat model.

1. [Security concern to address in threat identification]
2. [Configuration gap to address in mitigations]
3. [Other insights for later stages]

## Decision

**Status:** [CONFIDENT_APPROVAL / CONDITIONAL_APPROVAL / TARGETED_REVISION / MAJOR_REWORK]
**Confidence:** [X%]
**Required Actions:** [If not approved, specific fixes needed]
```

### Critic Review JSON Schema

**`ai-working-docs/{stage-number}.5-critic-review.json`**
```json
{
  "metadata": {
    "stage": 1,
    "review_date": "YYYY-MM-DD",
    "approval_status": "CONFIDENT_APPROVAL|CONDITIONAL_APPROVAL|TARGETED_REVISION|MAJOR_REWORK",
    "confidence_percentage": 78,
    "average_score": 3.6
  },
  "issues_identified": [
    {
      "id": "CR-001",
      "severity": "HIGH|MEDIUM|LOW",
      "category": "data_integrity|methodology|completeness|traceability|stakeholder_utility",
      "description": "Brief description of the issue",
      "affected_items": ["C-001", "TB-002"],
      "recommended_action": "What should be done to address this",
      "addressed_in_iteration": false
    }
  ],
  "challenges_applied": [
    {
      "challenge_type": "data_integrity|completeness|methodology|stakeholder_utility",
      "finding": "What was found when applying this challenge"
    }
  ],
  "scores": {
    "data_integrity": 4,
    "methodological_rigor": 4,
    "source_traceability": 4,
    "analytical_depth": 3,
    "stakeholder_utility": 3
  },
  "adversarial_questions": [
    {
      "question": "Security expert challenge question",
      "response": "Finding from applying this question"
    }
  ],
  "carry_forward_notes": [
    "Notes that should inform subsequent stages",
    "Security concerns identified for threat modeling",
    "Configuration gaps to address in mitigations"
  ]
}
```

### Using Critic Reviews in Subsequent Stages

**MANDATORY when Critic Mode is enabled:**

| Current Stage | Load Critic Reviews From |
|---------------|--------------------------|
| Stage 2 | `01.5-critic-review.json` |
| Stage 3 | `01.5-critic-review.json`, `02.5-critic-review.json` |
| Stage 4 | `01.5-critic-review.json`, `02.5-critic-review.json`, `03.5-critic-review.json` |
| Stage 5 | All prior `*.5-critic-review.json` files |
| Stage 6 | All `*.5-critic-review.json` files |

**How to Use Critic Context:**
1. **Load** prior stage critic reviews at start of work phase
2. **Reference** `carry_forward_notes` for additional security concerns
3. **Address** any `issues_identified` that affect current stage work
4. **Include** critic-identified concerns in threat identification (Stage 3)
5. **Note** in final report (Stage 6) how critic findings informed analysis

**Example Usage in Stage 3:**
```
When identifying threats, check 01.5-critic-review.json and 02.5-critic-review.json for:
- Security configuration gaps (e.g., disabled brute force protection)
- Potential information leakage concerns (e.g., debug logging)
- Trust boundary concerns identified by critic
- These should inform threat identification
```

---

## Human-Readable Markdown Files

### Conciseness Rules for Stages 1-5

**Stages 1-5 are working documents. Be concise from the start - do not elaborate then trim.**

#### PROHIBITED in Stages 1-5
| ❌ DON'T | Why |
|----------|-----|
| Executive Summaries | Only Stage 6 has one |
| Table of Contents | Only Stage 6 needs one |
| Methodology Explanations | Already in instruction files |
| "Overview" or "Introduction" sections | Get straight to content |
| Duplicate statistics | Present once (table OR prose) |
| Recommendations (except Stage 5) | Belongs in Stage 5/6 only |

#### REQUIRED in Stages 1-5
| ✅ DO | Example |
|-------|---------|
| Tables over prose | Component inventory as table, not paragraphs |
| Cross-reference by ID | "See T-001" not full threat description |
| Scale to complexity | Simple system = shorter output |

#### ALLOW MORE DETAIL FOR (See Stage Guides for Specifics)
| Section | Guideline |
|---------|-----------|
| Stage 1: Business Purpose | 2-4 sentences with context |
| Stage 1: Primary Users | Role descriptions with access levels |
| Stage 1: Assumptions | 2-3 sentences with rationale |
| Stage 3: Description | 3-5 sentences explaining the threat |
| Stage 3: Attack Scenario | 2-4 sentences with attack path |
| Stage 4: Justification | 2-4 sentences explaining rating |
| Stage 5: Implementation Steps | 3-5 specific actionable steps |
| Stage 5: Success Criteria | 2-3 sentences with verification methods |

#### Anti-Pattern Examples

**❌ VERBOSE (Don't do this):**
```markdown
## Executive Summary
This threat model analyzes the authentication system...
[3 paragraphs of introduction]

## Methodology
We applied STRIDE framework systematically...
[methodology explanation]

### T-001: SQL Injection Attack
This threat represents a significant risk to the system. SQL injection occurs when...
[5+ sentences of explanation, attack background, historical context]
```

**✅ CONCISE (Do this):**
```markdown
# Stage 3: Threat Identification
**Target:** Auth System | **Date:** 2025-12-03 | **Mode:** Automatic

## Threat Inventory
| ID | Threat | STRIDE | Component | Rating |
|----|--------|--------|-----------|--------|
| T-001 | SQL Injection | T,I,E | User API | HIGH |

### T-001: SQL Injection
**STRIDE:** T,I,E | **Component:** User API
**Description:** Unsanitized input enables query manipulation.
**Impact:** C:H I:H A:L | **Confidence:** M
```

### Markdown File Summary

| Stage | Markdown File | Purpose |
|-------|---------------|---------|
| 1 | `01-system-understanding.md` | Human-readable component/boundary/asset inventory |
| 2 | `02-data-flow-analysis.md` | Human-readable flow documentation |
| 3 | `03-threat-identification.md` | Human-readable threat inventory |
| 4 | `04-risk-assessment.md` | Human-readable risk ratings and prioritization |
| 5 | `05-mitigation-strategy.md` | Human-readable control recommendations |
| 6 | `00-final-report.md` | Stakeholder deliverable (comprehensive) |

---

## Clarifying Questions Files (Collaborative Mode Only)

- **Location:** `[target-directory]/output/threat-model/`
- **Format:** `{stage-number}_clarifying_questions.md`
- **Content:** Question, user response, how incorporated
- **Cross-Reference:** `*Source: User clarification (see Question [N])*`

---

## Quality Standards

- **Complete:** No placeholders (TODO/TBD) in either format
- **Consistent:** JSON IDs match markdown references
- **Accurate:** Source references in JSON, confidence levels stated
- **Validated:** JSON should be parseable; markdown should be readable

---

## ⚠️ MANDATORY: Report Footer (All Human-Readable Markdown Files)

**Every human-readable markdown output file (Stages 1-6) MUST include this footer at the end of the document.**

### Footer Template

```markdown
---

## Report Generation Details

> **⚠️ AI-Generated Content Disclaimer**
> 
> This report was generated using the [AI Threat Modeling Framework](https://github.com/ensingm2/AI-threat-modeling-rulesets). AI-generated security analysis should be reviewed by qualified security professionals before use. No guarantees of accuracy or completeness are provided. This report is intended as a starting point for security analysis, not a definitive security assessment.

| Field | Value |
|-------|-------|
| **Generated** | [YYYY-MM-DD] |
| **Framework Version** | [Short git commit hash, or "Unknown" if unavailable] |
| **Model** | [Model name, e.g., "Claude Opus 4", "GPT-4"] |
```

### How to Obtain Footer Values

| Field | How to Get |
|-------|------------|
| **Generated** | Current date in YYYY-MM-DD format |
| **Framework Version** | Run `git rev-parse --short HEAD` in the framework directory; use "Unknown" if git unavailable or not a repo |
| **Model** | The AI model currently executing (self-identify) |

### Footer Checklist

Before saving any markdown output file, verify:
- [ ] Footer is present at end of document
- [ ] AI disclaimer block included verbatim (includes repository link)
- [ ] Generation date is accurate
- [ ] Git commit hash retrieved (or "Unknown")
- [ ] Model name is accurate

---

## Stage Input Requirements

Each stage must load structured data from previous stages:

| Stage | Required JSON Inputs | Fallback Markdown |
|-------|---------------------|-------------------|
| 2 | `01-*.json` | `01-system-understanding.md` |
| 3 | `01-*.json`, `02-*.json` | `01-*.md`, `02-*.md` |
| 4 | `01-*.json`, `02-*.json`, `03-threats.json` | `01-03-*.md` |
| 5 | `01-*.json`, `03-threats.json`, `04-risk-assessments.json` | `01-04-*.md` |
| 6 | All `ai-working-docs/*.json` | All `*.md` files |

### Additional Inputs When Critic Mode Enabled

| Stage | Critic Review Inputs (if available) |
|-------|-------------------------------------|
| 2 | `01.5-critic-review.json` |
| 3 | `01.5-critic-review.json`, `02.5-critic-review.json` |
| 4 | `01.5-critic-review.json`, `02.5-critic-review.json`, `03.5-critic-review.json` |
| 5 | All prior `*.5-critic-review.json` files |
| 6 | All `*.5-critic-review.json` files |

**When loading critic reviews:**
- Use `carry_forward_notes` to inform current stage analysis
- Check `issues_identified` for concerns relevant to current stage
- Reference critic findings when they inform threat identification or risk assessment

**REMINDER: Stages 1-5 are working documents. Save elaboration for Stage 6.**
