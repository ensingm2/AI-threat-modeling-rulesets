# Stage 2: Data Flow Analysis | Documentation Specialist

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 2 work complete. Ready for critic analysis."

---

## ⚠️ CRITICAL: Concise From The Start

**Stage 2 is a WORKING DOCUMENT, not a final report. DO NOT create verbose output then trim - create concise output from the start.**

| ❌ PROHIBITED | ✅ REQUIRED |
|---------------|-------------|
| Executive Summary | Flow details in table columns |
| Table of Contents | 1-2 sentences per security note |
| Prose paragraphs per flow | Scale to system complexity |
| Detailed flow narratives | Reference Stage 1 IDs |

**Self-check before saving:**
- [ ] No executive summary or TOC?
- [ ] Flow details in tables not prose?
- [ ] Security notes ≤2 sentences each?
- [ ] Using Stage 1 component IDs?

**Stage 6 is where elaboration belongs. Keep Stage 2 lean.**

---

## Stage 2 Purpose

Create data flow documentation for Stage 3 threat analysis.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** `ai-working-docs/01-components.json`, `01-trust-boundaries.json`, `01-data-assets.json`
- **Fallback:** `01-system-understanding.md`
- Source documentation as needed (code, configs, API specs for flow details)

**Outputs:**
- **AI Working Docs:** `ai-working-docs/02-data-flows.json`, `02-attack-surfaces.json`
- **Human-Readable:** `02-data-flow-analysis.md`

---

## Required Output Structure

```markdown
# Stage 2: Data Flow Analysis
**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## 1. Stage 1 References
**Components:** [List from Stage 1]
**Trust Boundaries:** [List from Stage 1]

## 2. Data Flow Inventory
| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-001 | [Src] | [Dest] | [Data] | [HTTP/etc/Unknown] | [TB-X or None] | [Y/N/?] |

## 3. Trust Boundary Crossings
| Boundary | Flows Crossing | Auth Required | Security Notes |
|----------|----------------|---------------|----------------|
| TB-1 | DF-001, DF-005 | [Yes/No/?] | [Brief concern] |

## 4. Attack Surfaces
| Entry Point | Type | Component | Boundary | Auth | Key Flows |
|-------------|------|-----------|----------|------|-----------|
| Public API | API Endpoint | [Component] | TB-1 | No | DF-001, DF-002 |

## 5. Critical Data Paths
| Path Name | Flows | Data Sensitivity | Security Notes |
|-----------|-------|------------------|----------------|
| Auth Flow | DF-001→DF-002→DF-003 | Credentials | [Brief note] |

**Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence]
```

---

## Workflow Steps

### Step 1: Reference Stage 1
Extract exact component names, trust boundary names, data assets.

### Step 2: Identify Data Flows
For each flow: source, destination, data, protocol (documented/unknown), boundary crossed, auth required.

### Step 3: Build Data Flow Table
One row per flow - NO detailed prose sections per flow.

### Step 4: Map Attack Surfaces
Entry points with associated flows.

---

## Quality Rules

- **Tables over prose** - flow details in table columns, not paragraphs
- **Consistent flow IDs** - DF-001 in markdown matches DF-001 in JSON
- **Exact Stage 1 names** - no component/boundary name variations
- **Protocol = Documented/Unknown** - don't fabricate TLS versions etc.

---

## Completion Signal

```
✅ STAGE 2 WORK PHASE COMPLETE
- Output Files: 02-data-flow-analysis.md, ai-working-docs/02-*.json
- Total Flows: [N]
- Attack Surfaces: [N]
- Location: [target]/output/threat-model/
```

---
