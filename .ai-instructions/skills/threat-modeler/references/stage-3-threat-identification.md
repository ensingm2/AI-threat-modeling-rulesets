# Stage 3: Threat Identification | Threat Modeler

**Role:** Worker Mode | **Constraints:** See `SKILL.md` | **On completion:** "Stage 3 work complete. Ready for critic analysis."

---

## ⚠️ CRITICAL: Concise From The Start

**Stage 3 is a WORKING DOCUMENT, not a final report. DO NOT create verbose output then trim - create concise output from the start.**

| ❌ PROHIBITED | ✅ REQUIRED |
|---------------|-------------|
| Executive Summary | Threat summary table first |
| Statistics sections | Compact threat template |
| Framework summaries | Per-threat ATT&CK/Kill Chain inline |
| Recommendations | Scale to system complexity |
| Multi-paragraph threat descriptions | Clear attack narratives |

**Exceptions - Allow More Detail For:**
- **Description:** 3-5 sentences to fully explain the threat mechanism, prerequisites, and potential consequences
- **Attack Scenario:** 2-4 sentences describing the attacker profile, attack steps, and realistic exploitation path

**Self-check before saving:**
- [ ] No executive summary, TOC, or statistics section?
- [ ] Each threat has clear description and attack scenario?
- [ ] No recommendations (save for Stage 5)?
- [ ] Using compact threat template?
- [ ] Descriptions explain the "how" and "why" of the threat?

**Stage 6 is where elaboration belongs. Keep Stage 3 lean, but ensure threats are clearly understood.**

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

**Description:** [3-5 sentences: What is this threat? How does it work technically? What are the prerequisites? What are the potential consequences?]

**Attack Scenario:** [2-4 sentences: Who is the attacker (external/internal, skill level)? What specific steps would they take? What access/tools do they need? What is the realistic exploitation path?]

**Mappings:**
- **ATT&CK:** [Tactic] / [TID] - [Technique Name]
- **Kill Chain:** [Stage] - [Brief context]

**Impact:** C:[H/M/L/N] I:[H/M/L/N] A:[H/M/L/N] | **Rating:** [CRITICAL/HIGH/MEDIUM/LOW] | **Confidence:** [H/M/L]

---

[Repeat for all threats]

---

**Total Threats:** [N] | **By STRIDE:** S:[n] T:[n] R:[n] I:[n] D:[n] E:[n]
**Confidence:** [HIGH/MEDIUM/LOW] - [1 sentence]

---

## Report Generation Details

> **⚠️ AI-Generated Content Disclaimer**
> 
> This report was generated using the [AI Threat Modeling Framework](https://github.com/ensingm2/AI-threat-modeling-rulesets). AI-generated security analysis should be reviewed by qualified security professionals before use. No guarantees of accuracy or completeness are provided. This report is intended as a starting point for security analysis, not a definitive security assessment.

| Field | Value |
|-------|-------|
| **Generated** | [YYYY-MM-DD] |
| **Framework Version** | [Run `git rev-parse --short HEAD` or "Unknown"] |
| **Model** | [AI model name, e.g., "Claude Opus 4"] |
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

**Description:** [3-5 sentences explaining: What is this threat? How does it work? What are the prerequisites? What could happen if exploited?]

**Attack Scenario:** [2-4 sentences describing: Who is the attacker? What steps do they take? What access/tools are needed? What is the realistic attack path?]

**Mappings:**
- **ATT&CK:** [Tactic] / [TID] - [Technique]
- **Kill Chain:** [Stage]

**Impact:** C:[H/M/L/N] I:[H/M/L/N] A:[H/M/L/N] | **Rating:** [CRITICAL/HIGH/MEDIUM/LOW] | **Confidence:** [H/M/L]

---
```

**Balance clarity with conciseness** - Descriptions should be thorough enough to understand the threat without external references, but avoid unnecessary elaboration

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

## Quality Rules

- **Include mandatory footer** (see `shared/output-file-requirements.md`)

---

## Completion Signal

**⚠️ Do NOT include this in the output file. Communicate completion in your response only.**

After saving the output files, report completion in your response:
- Output File: 03-threat-identification.md
- Total Threats: [N] (S:[n] T:[n] R:[n] I:[n] D:[n] E:[n])
- Location: [target]/output/threat-model/
- Confidence: [HIGH/MEDIUM/LOW]

---
