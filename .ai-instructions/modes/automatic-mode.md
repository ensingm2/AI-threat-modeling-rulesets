# Automatic Mode Specification

**Mode Type:** Autonomous Threat Modeling  
**User Involvement:** None after initial mode selection

**Prerequisites:** `skills/shared/critical-rules.md`, `skills/workflow-guide.md`

---

## ⚠️ CRITICAL: Continuous Execution Required (ALWAYS in Automatic Mode)

**In Automatic mode, regardless of whether Critic Review is enabled or disabled, you MUST:**
1. **Execute ALL 6 stages continuously** in a single session
2. **NOT stop or pause** between stages - proceed immediately
3. **NOT wait for user input** - this is fully autonomous
4. **Save output files** after each stage, then continue to next stage
5. **Complete the entire threat model** before ending
6. **If Critic Review is enabled:** Perform critic analysis inline, then continue (no stopping)

**Execution Flow (Automatic WITHOUT Critic):**
```
Stage 1 → Save → Stage 2 → Save → Stage 3 → Save → Stage 4 → Save → Stage 5 → Save → Stage 6 → Save → COMPLETE
```

**Execution Flow (Automatic WITH Critic):**
```
Stage 1 Work → Critic → Save → Stage 2 Work → Critic → Save → ... → Stage 6 Work → Critic → Save → COMPLETE
```

**DO NOT end your response until Stage 6 is complete (or you hit a technical limit).**

**User involvement ONLY happens in Collaborative mode, NEVER in Automatic mode.**

---

## ⚠️ VERIFICATION: Did you ask about Critic Review mode?

**Before loading this file, you MUST have asked the user BOTH:**
1. ✅ Operational Mode (Automatic - confirmed by loading this file)
2. ❓ **Critic Review Mode** - Did you ask? If not, STOP and ask NOW.

**If Critic Review mode was NOT asked:** 
- STOP immediately
- Return to `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section
- Use the Critic Review portion of that prompt to ask the user

---

## Mode Overview

Fully autonomous threat modeling using only provided documentation, with no user interaction after mode selection.

| Characteristic | Automatic Mode |
|----------------|----------------|
| **User Engagement** | None after mode selection |
| **Clarifying Questions** | Not permitted |
| **Review Process** | Internal agent-based critic only |
| **Progression** | Automatic unless critic requires iteration |
| **Data Gaps** | Document assumptions, use industry standards |

---

## Process Flow

**With Critic Review (if enabled at startup):**
```
Stage Work → Critic Analysis → [Issues?] → NO → Next Stage (Automatic, NO user input)
                                    ↓ YES
                              Iteration (max 1-2) → Re-Critic → Next Stage
```

**Without Critic Review (default for single-agent):**
```
Stage Work → Next Stage (fully autonomous, no validation overhead)
```

**⚠️ CRITICAL:** In Automatic mode, NEVER stop for user input. The agent makes all decisions autonomously.

**User involvement is ONLY for Collaborative mode.** See `workflow-guide.md` for details.

---

## Autonomous Operation Requirements

### Documentation-Constrained Analysis
- Complete all analysis using only provided source materials
- No external resource access without explicit user pre-approval
- No clarifying questions mid-analysis
- Deliverables must be suitable for independent executive review

### Assumption Management
- Make reasonable assumptions with explicit documentation
- Use industry benchmarks when business context unavailable
- Acknowledge analytical limitations and data gaps honestly
- Provide qualitative assessments when quantitative data insufficient

---

## Handling Missing Information

### Template for Documenting Gaps

```markdown
**Data Available:** [What documentation says]
**Data Missing:** [Specific gap]
**Analysis Approach:** [How proceeding despite gap]
**Assumptions Documented:**
- [Assumption with confidence level]
**Implementation Note:** [What would improve analysis]
```

### Examples

**Technology Stack Unknown:**
> **Technology:** Cross-platform mobile application (specific framework not specified)  
> **Confidence:** MEDIUM - Generic security controls applicable across common frameworks

**Business Context Gap:**
> **Data Missing:** Transaction volumes, revenue, customer base size  
> **Approach:** Qualitative risk categories (CRITICAL/HIGH/MEDIUM/LOW)  
> **Assumptions:** Typical payment processing; industry-standard breach costs ($150-250/record)

---

## Agent Decision-Making Authority

### With Critic Review Enabled

**Agent May Approve When:**
- ✅ Critic identified 2-3+ issues AND work phase addressed them
- ✅ Average critic score ≤4.0 across dimensions (3.0-3.5 typical)
- ✅ At least one iteration cycle completed for Stages 1-3
- ✅ Data limitations explicitly acknowledged

**Agent MUST Reject When:**
- ❌ Critic found zero issues (rubber-stamping detected)
- ❌ All critic scores 5/5 without extraordinary justification
- ❌ First iteration approved without any findings (Stages 1-3)
- ❌ Work fabricates technical details or business metrics

**First-Pass Approval Rules:**
- **Stages 1-3:** First-pass approval PROHIBITED (minimum 1 iteration)
- **Stages 4-6:** May approve first pass IF 2+ genuine issues identified

### Continuous Execution (ALWAYS in Automatic Mode)

**⚠️ CRITICAL: Agent MUST continue through ALL stages without stopping:**
- Complete stage work → Save outputs → **IMMEDIATELY proceed to next stage**
- **DO NOT** end response or wait for user input between stages
- **DO NOT** ask "should I continue?" - the answer is always YES
- Execute Stage 1 through Stage 6 in one continuous session
- Only stop after Stage 6 final report is complete
- If Critic Review is enabled: perform critic inline, iterate if needed, then continue
- Quality relies on worker skill execution and source traceability

**This applies whether Critic Review is enabled or disabled.** The only difference is whether critic phases are included in the continuous flow.

---

## Stage-Specific Considerations

| Stage | Automatic Mode Focus |
|-------|---------------------|
| **1** | Document all architecture assumptions explicitly; identify gaps |
| **2** | Mark inferred flows with confidence levels; use generic trust patterns |
| **3** | Emphasize generic technical threats; document which require validation |
| **4** | Use qualitative categories; no fabricated business impact numbers |
| **5** | Provide generic controls applicable across technology variations |
| **6** | Explicitly state limitations in executive summary |

---

## Quality Standards

### Enhanced Requirements (No User Validation)
- **Source Traceability:** Critical - user cannot correct mid-analysis
- **Assumption Documentation:** Every assumption explicit and justified
- **Confidence Calibration:** Conservative given lack of validation
- **Limitation Acknowledgment:** Explicit statement of all constraints

---

## When to Use Automatic Mode

**Recommended:**
- User wants hands-off analysis without interruptions
- Comprehensive documentation already provided
- Preliminary assessment before detailed collaborative analysis

**Limitations:**
- Cannot get real-time clarification
- More conservative risk assessments due to uncertainty
- Generic recommendations when specifics unknown
