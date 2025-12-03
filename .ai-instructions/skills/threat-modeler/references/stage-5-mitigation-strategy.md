# Stage 5: Mitigation Strategy | Threat Modeler

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 5 work complete. Ready for critic analysis."

---

## ⚠️ CRITICAL: Concise From The Start

**Stage 5 is a WORKING DOCUMENT, not a final report. DO NOT create verbose output then trim - create concise output from the start.**

| ❌ PROHIBITED | ✅ REQUIRED |
|---------------|-------------|
| Executive Summary | Control-to-threat mapping table |
| Methodology sections | 2-3 sentence implementation guidance |
| Verbose control descriptions | Phased roadmap format |
| Multi-paragraph narratives | Quick wins table |

**Self-check before saving:**
- [ ] No executive summary or methodology section?
- [ ] Control descriptions ≤3 sentences?
- [ ] Using tables for mappings?
- [ ] Implementation guidance is actionable?

**Stage 6 is where elaboration belongs. Keep Stage 5 lean.**

---

## Stage 5 Purpose

Recommend security controls mapped to Stage 3 threats, prioritized by Stage 4 risk ratings.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** `ai-working-docs/01-*.json`, `02-*.json`, `03-threats.json`, `04-risk-assessments.json`
- **Fallback:** `01-system-understanding.md` through `04-risk-assessment.md`
- Source documentation as needed (for implementation feasibility)

**Outputs:**
- **AI Working Doc:** `ai-working-docs/05-mitigations.json`
- **Human-Readable:** `05-mitigation-strategy.md`

---

## Required Output Structure

```markdown
# Stage 5: Mitigation Strategy
**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## Control-to-Threat Mapping

| Control | Type | Threats Addressed | Effectiveness | Effort | Phase |
|---------|------|-------------------|---------------|--------|-------|
| [Control Name] | [Preventive/Detective] | T-001, T-005 | HIGH | LOW | 0 |
| [Control Name] | [Technical/Admin] | T-002 | MEDIUM | MEDIUM | 1 |

## Implementation Roadmap

### Phase 0: Immediate (0-30 days) - CRITICAL threats
| Control | Threats | Implementation Steps | Success Criteria |
|---------|---------|---------------------|------------------|
| [Name] | T-001 | [Brief steps] | [How to verify] |

### Phase 1: Short-Term (1-3 months) - HIGH threats
| Control | Threats | Implementation Steps | Success Criteria |
|---------|---------|---------------------|------------------|

### Phase 2: Medium-Term (3-6 months) - MEDIUM threats
| Control | Threats | Implementation Steps | Success Criteria |
|---------|---------|---------------------|------------------|

## Quick Wins
| Control | Threats | Effort | Impact | Notes |
|---------|---------|--------|--------|-------|
| [Name] | T-001 | LOW | HIGH | [1 sentence] |

## Residual Risk Summary
| Threat | Original Rating | Post-Mitigation | Residual Risk Notes |
|--------|-----------------|-----------------|---------------------|
| T-001 | CRITICAL | LOW | [Brief note] |

**Total Controls:** [N] | **Threats Covered:** [N]/[Total]
**Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence]
```

---

## Control Types

| Type | Purpose | Examples |
|------|---------|----------|
| **Preventive** | Stop attacks before they occur | Input validation, authentication, encryption |
| **Detective** | Identify attacks in progress | Logging, monitoring, IDS |
| **Corrective** | Respond to and recover from attacks | Incident response, backups, failover |

---

## Implementation Phases

| Phase | Timeline | Priority | Focus |
|-------|----------|----------|-------|
| **0** | 0-30 days | CRITICAL | Quick wins, emergency fixes |
| **1** | 1-3 months | HIGH | Substantial risk reduction |
| **2** | 3-6 months | MEDIUM | Foundational improvements |
| **3** | 6-12 months | LOW | Long-term enhancements |

---

## Compact Control Template

```markdown
### [Control Name]
**Type:** [Preventive/Detective/Corrective] | **Effort:** [LOW/MEDIUM/HIGH]
**Threats:** T-001, T-005, T-012
**Implementation:** [2-3 sentence description of what to implement]
**Success Criteria:** [How to verify it's working]
**Residual Risk:** [What risk remains after implementation]

---
```

**Keep entries concise** - Sufficient detail to implement, avoid verbose descriptions

---

## Quality Rules

- **Map all CRITICAL/HIGH threats** - Every high-priority threat needs at least one control
- **Feasible controls only** - Based on documented architecture constraints
- **No cost fabrication** - Don't invent budget figures; use effort levels (LOW/MEDIUM/HIGH)
- **Actionable guidance** - Technical teams should be able to implement from this

---

## Completion Signal

```
✅ STAGE 5 WORK PHASE COMPLETE
- Output File: 05-mitigation-strategy.md
- Total Controls: [N]
- Threats Covered: [N]/[Total] ([%])
- Quick Wins Identified: [N]
- Location: [target]/output/threat-model/
- Confidence: [HIGH/MEDIUM/LOW]
```

---
