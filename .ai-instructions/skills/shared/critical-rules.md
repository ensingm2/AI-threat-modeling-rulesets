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
2. **Collaborative Mode:** STOP → User reviews and provides feedback/approval → Continue
3. **Automatic Mode:** Proceed directly to next stage (NO stopping)
4. Repeat for all 6 stages

**Process WITH Critic Review (If enabled):**
1. Complete stage work → Create output file(s)
2. Perform critic analysis
3. **Collaborative Mode:** STOP → User reviews work AND critic findings → User approves → Continue
4. **Automatic Mode:** Agent decides based on critic findings → Iterate if needed → Continue (NO stopping)
5. Repeat for all 6 stages

---

### 2. MANDATORY: Review ALL User-Provided Source Files

**⚠️ BEFORE beginning Stage 1 work, you MUST identify and read EVERY contextual file provided by the user.**

**Required Process:**
1. **Identify all sources:** Determine ALL files/directories the user has provided as context for the threat model (may include code, documentation, configs, diagrams, or any other relevant files)
2. **Enumerate completely:** List ALL files in any provided directories - use recursive directory listing if needed
3. **Read EVERY file:** Open and thoroughly read each file - no exceptions, no skipping
4. **Document coverage:** Track which files have been reviewed in Stage 1 output
5. **Reference throughout:** Cross-reference findings to specific source files in all stages

**Prohibited:**
- ❌ Starting Stage 1 without identifying all user-provided source files
- ❌ Skipping any provided file (even if it seems irrelevant)
- ❌ Making assumptions about file contents without reading them
- ❌ Reading only "key" files - ALL provided files must be read
- ❌ Summarizing from memory without re-reading source files when needed
- ❌ Assuming you know what files exist without explicitly listing directories

**Verification Checklist:**
- [ ] All user-provided directories enumerated
- [ ] Total file count documented
- [ ] Each file explicitly opened and read
- [ ] Source Documentation table in Stage 1 includes ALL provided files
- [ ] Files flagged as "Not Reviewed" or "Partial" require justification

**Why This Matters:**
- Critical security context may exist in ANY file
- Missing a single file can lead to incomplete threat identification
- Source traceability requires complete coverage
- Business context often distributed across multiple documents

**Hard Gate:** Stage 1 CANNOT be considered complete unless 100% of user-provided source files are documented in the Source Documentation table.

---

### 3. CONCISE FROM THE START (Stages 1-5)

**DO NOT create verbose stage files and trim later. Create concise files from the start.**

**Stages 1-5 are WORKING DOCUMENTS:**
- Tables over prose
- No executive summaries, TOCs, or methodology sections
- Cross-reference by ID, don't duplicate content
- Scale output to system complexity

**Exceptions - Allow More Detail For Key Sections:**
- **Stage 1:** Business Purpose (2-4 sentences), Primary Users (role descriptions), Assumptions (2-3 sentences with rationale)
- **Stage 3:** Description (3-5 sentences), Attack Scenario (2-4 sentences)
- **Stage 4:** Justification (2-4 sentences explaining rating rationale)
- **Stage 5:** Implementation Steps (3-5 specific actions), Success Criteria (2-3 sentences with verification methods)

**Stage 6 is the ONLY comprehensive report:**
- Executive summary belongs here
- Full narratives and elaboration belong here
- Stakeholder-ready formatting belongs here

**Why this matters:**
- Verbose-then-trim wastes 40%+ tokens
- Creates inconsistency between versions
- Trimming risks removing important information
- But overly terse content lacks actionable detail

**Self-check before saving Stages 1-5:**
- [ ] No executive summary or TOC?
- [ ] Tables used instead of prose lists?
- [ ] No methodology explanations?
- [ ] Key sections have sufficient detail for clarity?

---

### 4. NEVER FABRICATE DATA OR QUANTIFY WITHOUT DATA

**Prohibited Fabrications:**
- ❌ Business metrics (user counts, revenue, transaction volumes)
- ❌ Technical details (specific frameworks, versions, configurations)
- ❌ Risk scores (CVSS scores without proper calculation)
- ❌ Cost estimates (dollar amounts without budget data)
- ❌ System characteristics (performance metrics, capacity)

**Prohibited Quantification (without sufficient data):**
- ❌ Regulatory fine amounts (e.g., "$4.2M GDPR fine")
- ❌ Financial impact figures (e.g., "$500K-$2M breach cost")
- ❌ Remediation cost estimates (e.g., "$45K implementation cost")
- ❌ Timeline estimates with specific durations (e.g., "0-30 days")
- ❌ Any dollar amount, percentage, or specific number without source data

**Correct Approaches:**
- ✅ "GDPR Article 83 penalties (up to 4% annual revenue)" - cite the regulation, not a dollar amount
- ✅ "HIGH financial impact" - qualitative category, not fabricated numbers
- ✅ "Phase 0 (Immediate)" - priority-based, not day-based
- ✅ "Specific figures require business data" - acknowledge the gap

**Required Behaviors:**
- ✅ Cite sources: Trace all claims to specific documentation sections
- ✅ Document assumptions: Clearly identify inferred vs. documented behaviors
- ✅ Use confidence levels: HIGH (85-95%), MEDIUM (70-<85%), LOW (50-<70%), INSUFFICIENT (<50%)
- ✅ Mark unknowns: Technology = Documented/Inferred/Unknown
- ✅ Use qualitative categories when quantitative data unavailable

---

### 5. EXECUTION PROTOCOL (MODE-DEPENDENT)

**⚠️ AUTOMATIC MODE = ALWAYS CONTINUOUS EXECUTION**

**When user selects Automatic mode (with OR without Critic Review):**
```
Stage 1 → Stage 2 → Stage 3 → Stage 4 → Stage 5 → Stage 6 → DONE
(If Critic enabled: Work → Critic → Work → Critic → ... all in one continuous flow)
```
- Execute ALL stages continuously without stopping
- Save files after each stage, then IMMEDIATELY proceed to next
- If Critic Review enabled: perform critic analysis inline, then continue
- NO user interaction until final report is complete
- This is the expected behavior for autonomous operation

**COLLABORATIVE MODE = BATCHED EXECUTION (User Involvement Required)**

**Only Collaborative mode requires stopping for user review:**
```
Batch 1: Stage N Work Phase → Save files → STOP (wait for user)
Batch 2: Stage N Critic Phase (if enabled) → Validation → STOP (wait for user)
Batch 3: Stage N+1 Work Phase → Save files → STOP
```

**Prohibited (in Collaborative mode only):**
- ❌ Combining work + critic in same response
- ❌ Skipping user review between stages

**Key Rule:** User involvement ONLY in Collaborative mode. Automatic mode is fully autonomous.

**Note:** Incremental file building (for large outputs) is still required in ALL modes to avoid tool parameter limits.

---

### 6. MANDATORY FOOTER ON ALL MARKDOWN OUTPUTS

**Every human-readable markdown file (Stages 1-6) MUST include the standard footer.**

**Footer includes:**
- AI-generated content disclaimer
- Generation date (YYYY-MM-DD)
- Framework version (git commit hash or "Unknown")
- Model name (self-identify)
- Repository link

**See:** `shared/output-file-requirements.md` → "MANDATORY: Report Footer" for exact template.

**Prohibited:**
- ❌ Saving any markdown output without the footer
- ❌ Modifying the disclaimer text
- ❌ Omitting any required footer fields

---

### 7. ROLE SEPARATION

| Role | Permitted | Prohibited |
|------|-----------|------------|
| **Worker** | Complete deliverables, create outputs | Fix problems identified by critic (must iterate) |
| **Critic** | Find flaws, challenge assumptions | Complete deliverables, fix problems |

**Role Separation by Mode:**
- **Collaborative Mode:** Work and critic phases MUST be in separate responses (user reviews between)
- **Automatic Mode:** Work and critic phases MAY be in same response for continuous execution

**After Work Phase (Collaborative only):** "Stage [N] work is complete. Ready for review."

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
