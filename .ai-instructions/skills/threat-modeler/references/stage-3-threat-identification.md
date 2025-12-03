# Stage 3: Threat Identification | Threat Modeler

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 3 work complete. Ready for critic analysis."

---

## Conciseness Requirement

**Stage 3 is a WORKING DOCUMENT, not a final report.**

- **NO Executive Summary** - Only Stage 6 has one
- **NO Statistics Sections** - Just count threats at the end
- **NO Framework Summary Sections** - Per-threat mappings are sufficient
- **NO Recommendations** - Belongs in Stage 5/6
- **Compact threat format** - Keep entries concise; avoid verbose descriptions
- **Scale appropriately** - Simple systems have fewer threats than complex ones

---

## Stage 3 Purpose

Apply STRIDE systematically to identify threats, map to MITRE ATT&CK techniques and Kill Chain stages.

**Inputs (prefer JSON, fallback to markdown):**
- **Primary:** `ai-working-docs/01-*.json`, `02-*.json` (components, boundaries, assets, flows, attack surfaces)
- **Fallback:** `01-system-understanding.md`, `02-data-flow-analysis.md`
- Source documentation as needed (code, configs, interviews, external docs)

**Outputs:**
- **AI Working Doc:** `ai-working-docs/03-threats.json`
- **Human-Readable:** `03-threat-identification.md`

---

## Required Output Structure

```markdown
# Stage 3: Threat Identification
**Target:** [Name] | **Date:** [YYYY-MM-DD] | **Mode:** [Collaborative/Automatic]

## Threat Inventory

| ID | Threat Name | STRIDE | Component | ATT&CK | Kill Chain | Rating |
|----|-------------|--------|-----------|--------|------------|--------|
| T-001 | [Name] | S | [Component] | T1190 | Delivery | HIGH |
| T-002 | [Name] | T | [Component] | T1565 | Actions | MEDIUM |

## Threat Details

### T-001: [Threat Name]
**STRIDE:** Spoofing | **Component:** [Name] | **Type:** [Generic/System-Specific]

**Description:** [2-3 sentences describing the threat]

**Attack Scenario:** [Attacker profile] performs [actions] to achieve [outcome].

**Mappings:**
- **ATT&CK:** [Tactic] / [TID] - [Technique Name]
- **Kill Chain:** [Stage] - [Brief context]

**Impact:** [C/I/A impact] | **Rating:** [CRITICAL/HIGH/MEDIUM/LOW] | **Confidence:** [H/M/L]

---

[Repeat for all threats]

---

**Total Threats:** [N] | **By STRIDE:** S:[n] T:[n] R:[n] I:[n] D:[n] E:[n]
**Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence]
```

---

## STRIDE Application

Analyze EACH component for ALL six STRIDE categories:

| Category | Question | Examples |
|----------|----------|----------|
| **S**poofing | Can identity be faked? | User impersonation, service spoofing |
| **T**ampering | Can data be modified? | Data in transit/rest modification |
| **R**epudiation | Can actions be denied? | Missing audit logs, no attribution |
| **I**nfo Disclosure | Can data leak? | API leaks, storage exposure |
| **D**enial of Service | Can availability be impacted? | Resource exhaustion, crashes |
| **E**levation of Privilege | Can access be escalated? | Auth bypass, privilege escalation |

---

## Threat Balance

- **60-70%** Generic Technical Threats (implementation-agnostic)
- **20-30%** System-Specific Threats (based on documented functionality)
- **10-20%** Operational Threats (process and organizational)

**Never fabricate threats to meet count guidelines.**

---

## Compact Threat Template

```markdown
### T-XXX: [Threat Name]
**STRIDE:** [S/T/R/I/D/E] | **Component:** [Name] | **Type:** [Generic/System-Specific]

**Description:** [2-3 sentences]

**Attack Scenario:** [Attacker] with [access/skills] performs [action] via [method] to achieve [outcome].

**Mappings:**
- **ATT&CK:** [Tactic] / [TID] - [Technique]
- **Kill Chain:** [Stage]

**Impact:** C:[H/M/L/N] I:[H/M/L/N] A:[H/M/L/N] | **Rating:** [CRITICAL/HIGH/MEDIUM/LOW] | **Confidence:** [H/M/L]

---
```

**Keep entries concise** - Include required fields without verbose descriptions

---

## MITRE ATT&CK Mapping

For each threat, identify:
- **Tactic:** Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Discovery, Lateral Movement, Collection, Exfiltration, Impact
- **Technique ID:** TXXXX (most specific applicable)

Common techniques: T1190 (Public App Exploit), T1078 (Valid Accounts), T1110 (Brute Force), T1059 (Command Execution), T1565 (Data Manipulation), T1499 (DoS)

---

## Kill Chain Mapping

For each threat, identify stage:
1. **Reconnaissance** - Information gathering
2. **Weaponization** - Preparing attack
3. **Delivery** - Transmitting attack
4. **Exploitation** - Executing attack
5. **Installation** - Establishing persistence
6. **Command & Control** - Maintaining access
7. **Actions on Objectives** - Achieving goals

---

## Incremental Building

For large threat counts, build file incrementally:
1. Create header + inventory table
2. Add threats component-by-component via search_replace
3. Update totals at end

---

## Completion Signal

```
✅ STAGE 3 WORK PHASE COMPLETE
- Output File: 03-threat-identification.md
- Total Threats: [N] (S:[n] T:[n] R:[n] I:[n] D:[n] E:[n])
- Location: [target]/output/threat-model/
- Confidence: [HIGH/MEDIUM/LOW]
```

---
