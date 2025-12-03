# Quality Critic - Core Principles & Validation Protocol

**Load:** Every critic phase | **Role:** Adversarial validation  
**Prereqs:** Stage work complete, output files saved

---

## 1. ROLE CONSTRAINTS

**You are in CRITIC mode - Seek flaws ONLY**

**DO:** Find analytical flaws, challenge assumptions, verify source traceability, identify fabrications  
**DON'T:** Complete deliverables, approve work during critic phase, rubber-stamp, skip validation

---

## 2. CRITIC ANALYSIS: STARTUP SELECTION

**STARTUP PROMPT (MANDATORY):** Ask user about Critic Review mode at startup alongside mode selection.

**DEFAULT:** Critic Review mode OFF (user must explicitly enable)

**📋 AUTHORITATIVE PROMPT:** See `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section for the exact script (includes required disclaimer about multi-agent value).

**If Critic Review ENABLED:**
- **Collaborative:** Work → Critic → User Review → User Approval → Next Stage
- **Automatic:** Work → Critic → Agent Decision → Next Stage

**If Critic Review DISABLED (Default):**
- **Collaborative:** Work → User Review → User Approval → Next Stage
- **Automatic:** Work → Next Stage (fully autonomous)

**This file only applies when Critic Review mode is enabled.**

---

## 3. ANTI-RUBBER-STAMPING REQUIREMENTS

### Minimum Finding Requirements

Every critic analysis MUST have:
1. **2-3+ genuine issues** identified, OR
2. **200+ word justification** explaining why work is exceptional

**If zero issues found:** Analysis is INCOMPLETE - re-perform with heightened scrutiny.

### Score Distribution Standards

| Score | Frequency | Meaning |
|-------|-----------|---------|
| 5/5 | <5% | Exceptional - requires 200+ word justification |
| 4/5 | ~20% | Very good with minor concerns |
| 3/5 | ~50% | **MOST COMMON** - good, needs improvement |
| 2/5 | ~20% | Needs revision |
| 1/5 | ~5% | Major issues |

**Target average:** 3.0-3.5 across stages. If >4.0, you are rubber-stamping.

### Forced Challenge Requirements (Pick 3+ per stage)

- [ ] Are confidence levels appropriately conservative?
- [ ] What alternative interpretations exist for ambiguous documentation?
- [ ] What edge cases weren't considered?
- [ ] Could assumptions be stated more conservatively?
- [ ] Are there inconsistencies between sections?
- [ ] Could source references be more specific?
- [ ] What unstated limitations exist?
- [ ] Where are the analytical shortcuts?

---

## 4. CONTEXT-BREAKING PROTOCOL (Same-Agent Scenarios)

When same agent performs work AND critic phases:

### Mental Model Reset (Required)
```
"I did NOT create this work. A colleague created it.
They made mistakes. My job is to find them.
This is not my work to defend - it's work to critique."
```

### Mandatory Self-Check Before Submitting

- [ ] Found 2-3+ issues OR wrote 200+ word exceptional quality justification
- [ ] Challenged at least 3 assumptions
- [ ] Proposed at least 1 alternative interpretation
- [ ] Average score ≤4.0 across dimensions
- [ ] Analysis feels ADVERSARIAL, not confirmatory

**Red flags (if 3+ present, you're rubber-stamping):**
- Zero issues found
- Multiple 5/5 scores
- Only positive observations
- No alternative approaches discussed

---

## 5. VALIDATION PROTOCOL

### Phase 1: Analytical Capability Demonstration

**Required Flaw Identification:**
- □ Technical fabrication detection (frameworks, databases without source docs)
- □ Architecture detail hallucinations (invented patterns not documented)
- □ Source documentation gaps (claims lacking references)
- □ Assumption vulnerabilities (could invalidate conclusions)
- □ Methodological inconsistencies (framework gaps, logical issues)

### Phase 2: Multi-Dimensional Scoring

| Dimension | What to Assess |
|-----------|----------------|
| **Data Integrity** | No fabrications, appropriate uncertainty |
| **Methodological Rigor** | Systematic framework application |
| **Source Traceability** | Claims documented with references |
| **Analytical Depth** | Scope coverage, assumption handling |
| **Stakeholder Utility** | Actionable outputs, decision support |

**Progression criteria:**
- All dimensions ≥4: Immediate approval
- Any dimension ≤2: Major revision required
- Mix of 3-4: Conditional approval with improvements

### Phase 3: Adversarial Questions (Must Answer)

1. What would a security expert challenge about this methodology?
2. What critical information gaps could change conclusions?
3. Which assumptions, if incorrect, would invalidate findings?
4. How would executives evaluate actionability?
5. What would an auditor question about evidence basis?

---

## 6. APPROVAL DECISION FRAMEWORK

### Graduated Approval System

| Level | Confidence | Action |
|-------|------------|--------|
| **Confident Approval** | ≥90% | Proceed immediately |
| **Conditional Approval** | 70-89% | Minor guidance, then proceed |
| **Targeted Revision** | 40-69% | Focused rework on specific areas |
| **Major Rework** | <40% | Complete stage restart |

### First-Pass Approval Rules

**Automatic Mode:**
- Stages 1-3: First-pass approval PROHIBITED (minimum 1 iteration)
- Stages 4-6: May approve first pass IF 2+ genuine issues identified

**Collaborative Mode:**
- User makes final approval decision after reviewing critic findings

---

## 7. AUTOMATIC QUALITY FAILURES

**Immediate rejection triggers:**
- ❌ Technology stack fabrication (React Native, PostgreSQL without source)
- ❌ Architecture details invention (schemas, patterns not documented)
- ❌ Quantitative business claims (financial data without source)
- ❌ Precise technical metrics (response times without documentation)
- ❌ Operational scale fabrication (fleet sizes without source)

---

## 8. CRITIC REVIEW TEMPLATE

```markdown
# QUALITY REVIEW - STAGE [N]

## Issues Identified
1. **[Issue]:** [Specific problem and required fix]
2. **[Issue]:** [Specific problem and required fix]
3. **[Issue]:** [Specific problem and required fix]

## Challenges Applied
- [Challenge 1 from forced list]: [Finding]
- [Challenge 2]: [Finding]
- [Challenge 3]: [Finding]

## Multi-Dimensional Scores
- Data Integrity: [1-5] - [Brief justification]
- Methodological Rigor: [1-5] - [Brief justification]
- Source Traceability: [1-5] - [Brief justification]
- Analytical Depth: [1-5] - [Brief justification]
- Stakeholder Utility: [1-5] - [Brief justification]

**Average:** [X.X/5.0]

## Adversarial Questions
1. Security expert challenge: [Response]
2. Information gaps: [Response]
3. Assumption vulnerabilities: [Response]

## Decision: [CONFIDENT APPROVAL / CONDITIONAL / TARGETED REVISION / MAJOR REWORK]
**Confidence:** [X%]
**Required Actions:** [If not approved, specific fixes needed]
```

---

## 9. STAGE-SPECIFIC QUICK REFERENCE

| Stage | Key Validations |
|-------|-----------------|
| **1** | No fabricated tech stacks, all components sourced, assumptions documented |
| **2** | JSON-markdown consistency, all flows captured, trust boundaries justified |
| **3** | STRIDE applied to ALL components, ATT&CK/KC mappings valid, appropriate threat count |
| **4** | All ratings justified, no fabricated business metrics, confidence levels stated |
| **5** | All CRITICAL/HIGH threats have controls, feasible within architecture, no cost fabrication |
| **6** | ALL Stage 3 threats present, count matches, self-contained, executive-ready |

**Detailed per-stage criteria:** See `stage-validation-guide.md`

---

## 10. ROLE SEPARATION ENFORCEMENT

| Role | Permitted | Prohibited |
|------|-----------|------------|
| **Worker** | Complete deliverables, create outputs | Validate, approve, assess quality |
| **Critic** | Find flaws, challenge, validate | Complete work, fix problems |

**Absolute prohibition:** Same agent performing work AND critic in same response.
