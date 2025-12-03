# Critical Rules | Load: Always | ~800 tokens

**Scope:** All threat modeling stages, all operational modes  
**Priority:** These rules are absolute and non-negotiable

---

## ❌ CRITICAL PROHIBITIONS

### 1. NEVER START WITHOUT BOTH MANDATORY SELECTIONS

**⚠️ BEFORE beginning ANY threat modeling work, you MUST ask BOTH questions in a SINGLE prompt.**

**📋 AUTHORITATIVE PROMPT:** See `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section for the exact script to use verbatim.

**After user responds:**
1. Load the selected mode file from `modes/`
2. Confirm BOTH selections before proceeding to Stage 1

**Prohibited:**
- ❌ Starting Stage 1 without asking about operational mode
- ❌ Starting Stage 1 without asking about critic review mode
- ❌ Assuming either preference without explicit user selection
- ❌ Asking about mode but forgetting to ask about critic review
- ❌ Asking the two questions in separate prompts (MUST be combined)
- ❌ Using your own wording instead of the exact script from `.cursorrules`

**DEFAULT:** Critic Review mode OFF (user must explicitly enable)

**Process WITHOUT Critic Review (Default):**
1. Complete stage work → Create output file(s)
2. **END WORK PHASE**
3. **Collaborative Mode:** User reviews and provides feedback/approval
4. **Automatic Mode:** Proceed directly to next stage
5. Repeat for all 6 stages

**Process WITH Critic Review (If enabled):**
1. Complete stage work → Create output file(s)
2. **END WORK PHASE** (no validation in same response)
3. Load critic skills → Perform quality validation
4. **END CRITIC PHASE** (no rework in same response)
5. If not approved → Return to step 1 with feedback

---

### 3. CONCISE FROM THE START (Stages 1-5)

**DO NOT create verbose stage files and trim later. Create concise files from the start.**

**Stages 1-5 are WORKING DOCUMENTS:**
- Tables over prose
- 2-3 sentences max per threat/control
- No executive summaries, TOCs, or methodology sections
- Cross-reference by ID, don't duplicate content
- Scale output to system complexity

**Stage 6 is the ONLY comprehensive report:**
- Executive summary belongs here
- Full narratives and elaboration belong here
- Stakeholder-ready formatting belongs here

**Why this matters:**
- Verbose-then-trim wastes 40%+ tokens
- Creates inconsistency between versions
- Trimming risks removing important information
- LLMs naturally over-elaborate; explicit constraint is required

**Self-check before saving Stages 1-5:**
- [ ] No executive summary or TOC?
- [ ] Tables used instead of prose lists?
- [ ] Each item ≤3 sentences?
- [ ] No methodology explanations?

---

### 4. NEVER FABRICATE DATA

**Prohibited Fabrications:**
- ❌ Business metrics (user counts, revenue, transaction volumes)
- ❌ Technical details (specific frameworks, versions, configurations)
- ❌ Risk scores (CVSS scores without proper calculation)
- ❌ Cost estimates (dollar amounts without budget data)
- ❌ System characteristics (performance metrics, capacity)

**Required Behaviors:**
- ✅ Cite sources: Trace all claims to specific documentation sections
- ✅ Document assumptions: Clearly identify inferred vs. documented behaviors
- ✅ Use confidence levels: HIGH (85-95%), MEDIUM (70-<85%), LOW (50-<70%), INSUFFICIENT (<50%)
- ✅ Mark unknowns: Technology = Documented/Inferred/Unknown

---

### 5. EXECUTION PROTOCOL (MODE-DEPENDENT)

**⚠️ AUTOMATIC MODE + NO CRITIC = CONTINUOUS EXECUTION**

**When user selects Automatic mode WITHOUT Critic Review:**
```
Stage 1 → Stage 2 → Stage 3 → Stage 4 → Stage 5 → Stage 6 → DONE
```
- Execute ALL stages continuously without stopping
- Save files after each stage, then IMMEDIATELY proceed to next
- NO user interaction until final report is complete
- This is the expected behavior for autonomous operation

**COLLABORATIVE MODE or CRITIC ENABLED = BATCHED EXECUTION**

**When user review or critic validation is required:**
```
Batch 1: Stage N Work Phase → Save files → STOP
Batch 2: Stage N Critic Phase (if enabled) → Validation → STOP
Batch 3: Stage N+1 Work Phase → Save files → STOP
```

**Prohibited (when batching applies):**
- ❌ Combining work + critic in same response
- ❌ Skipping user review in Collaborative mode

**Note:** Incremental file building (for large outputs) is still required in ALL modes to avoid tool parameter limits.

---

### 6. MANDATORY ROLE SEPARATION

| Role | Permitted | Prohibited |
|------|-----------|------------|
| **Worker** | Complete deliverables, create outputs | Validate own work, approve progression |
| **Critic** | Find flaws, challenge assumptions | Complete deliverables, fix problems |

**Absolute Prohibition:** Same agent performing work AND critic roles in same response.

**After Work Phase:** "Stage [N] work is complete. The deliverables are ready for critic analysis."

---

## Quality Standards

### Minimum Critic Requirements

Every critic analysis MUST have:
1. 2-3+ issues identified OR 200+ word justification for exceptional quality
2. At least 3 challenges from forced challenge list
3. Average score ≤4.0 across dimensions (3.0-3.5 typical)
4. Evidence of adversarial (not confirmatory) mindset

### Score Distribution

| Score | Frequency | Meaning |
|-------|-----------|---------|
| 5/5 | <5% | Exceptional - requires 200+ word justification |
| 4/5 | ~20% | Excellent with minor observations |
| 3/5 | ~50% | **MOST COMMON** - good, needs improvement |
| 2/5 | ~20% | Needs revision |
| 1/5 | ~5% | Major rework |

**If average score >4.0:** You are rubber-stamping. Recalibrate.

---

**This file consolidates all critical rules. Other files should reference this rather than duplicating content.**
