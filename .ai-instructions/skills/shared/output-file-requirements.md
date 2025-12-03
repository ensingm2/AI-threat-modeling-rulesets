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
├── 02-data-flow-analysis.md
├── 03-threat-identification.md
├── 04-risk-assessment.md
├── 05-mitigation-strategy.md
├── 06-final-comprehensive-report.md
└── ai-working-docs/
    ├── 01-components.json
    ├── 01-trust-boundaries.json
    ├── 01-data-assets.json
    ├── 01-assumptions.json
    ├── 02-data-flows.json
    ├── 02-attack-surfaces.json
    ├── 03-threats.json
    ├── 04-risk-assessments.json
    └── 05-mitigations.json
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

## Human-Readable Markdown Files

### Conciseness Rules for Stages 1-5

**Stages 1-5 are working documents. Be concise from the start - do not elaborate then trim.**

#### PROHIBITED in Stages 1-5
| ❌ DON'T | Why |
|----------|-----|
| Executive Summaries | Only Stage 6 has one |
| Table of Contents | Only Stage 6 needs one |
| Methodology Explanations | Already in instruction files |
| Prose paragraphs per item | Use tables instead |
| "Overview" or "Introduction" sections | Get straight to content |
| Duplicate statistics | Present once (table OR prose) |
| Recommendations | Belongs in Stage 5/6 only |
| Verbose threat/control descriptions | 2-3 sentences max per item |

#### REQUIRED in Stages 1-5
| ✅ DO | Example |
|-------|---------|
| Tables over prose | Component inventory as table, not paragraphs |
| Brief confidence statements | "Confidence: MEDIUM - [1 sentence reason]" |
| Cross-reference by ID | "See T-001" not full threat description |
| Scale to complexity | Simple system = shorter output |
| Single-sentence justifications | Not multi-paragraph explanations |

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
| 6 | `06-final-comprehensive-report.md` | Stakeholder deliverable (comprehensive) |

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

## Stage Input Requirements

Each stage must load structured data from previous stages:

| Stage | Required JSON Inputs | Fallback Markdown |
|-------|---------------------|-------------------|
| 2 | `01-*.json` | `01-system-understanding.md` |
| 3 | `01-*.json`, `02-*.json` | `01-*.md`, `02-*.md` |
| 4 | `01-*.json`, `02-*.json`, `03-threats.json` | `01-03-*.md` |
| 5 | `01-*.json`, `03-threats.json`, `04-risk-assessments.json` | `01-04-*.md` |
| 6 | All `ai-working-docs/*.json` | All `*.md` files |

**REMINDER: Stages 1-5 are working documents. Save elaboration for Stage 6.**
