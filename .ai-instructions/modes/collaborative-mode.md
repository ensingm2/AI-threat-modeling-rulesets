# Collaborative Mode Specification

**Mode Type:** User-Engaged Threat Modeling  
**User Involvement:** Active participation throughout process

**Prerequisites:** `skills/shared/critical-rules.md`, `skills/workflow-guide.md`

---

## ⚠️ VERIFICATION: Did you ask about Critic Review mode?

**Before loading this file, you MUST have asked the user BOTH:**
1. ✅ Operational Mode (Collaborative - confirmed by loading this file)
2. ❓ **Critic Review Mode** - Did you ask? If not, STOP and ask NOW.

**If Critic Review mode was NOT asked:** 
- STOP immediately
- Return to `.cursorrules` → "MANDATORY STARTUP SELECTIONS" section
- Use the Critic Review portion of that prompt to ask the user

---

## Mode Overview

Active user participation throughout the threat modeling process, allowing real-time clarification, validation, and business context integration.

| Characteristic | Collaborative Mode |
|----------------|-------------------|
| **User Engagement** | Active throughout all stages |
| **Clarifying Questions** | Agent asks when information helpful |
| **Review Process** | User reviews after each critic analysis |
| **Progression** | User validates and approves each stage |
| **Data Gaps** | Agent requests info from user when critical |

---

## Process Flow

**With Critic Review (if enabled at startup):**
```
Stage Work → Critic Analysis → USER REVIEW → User Approval → Next Stage
```

**Without Critic Review (default for single-agent):**
```
Stage Work → USER REVIEW & QUESTIONS → User Approval → Next Stage
```

**CRITICAL:** Regardless of critic setting, user MUST still review, ask questions, and approve each stage.

**Batching details:** See `workflow-guide.md`

---

## ⚠️ Always Ask Before Assuming

**NEVER make assumptions without first asking the user.**

**ALWAYS prompt user when encountering:**
- Vague or ambiguous documentation
- Missing technical details
- Unclear security controls
- Unspecified business context
- Technology stack gaps
- Architecture ambiguities

**ONLY document assumptions AFTER user confirms they have no additional context.**

---

## Stage-Specific User Engagement

### Stage 1: System Understanding
**Agent May Ask:**
- "Can you clarify the business model for [functionality]?"
- "What is the expected deployment scale and geographic scope?"
- "Are there specific regulatory requirements?"

### Stage 2: Data Flow Analysis
**Agent May Ask:**
- "Does data flow [X] cross a network boundary or remain internal?"
- "What authentication is required for [specific flow]?"
- "Is [data element] considered sensitive?"

### Stage 3: Threat Identification
**Agent May Ask:**
- "Is threat [X] relevant given your operational context?"
- "Are there known threat actors specific to your industry?"
- "Have you experienced similar security incidents?"

### Stage 4: Risk Assessment
**Agent May Ask:**
- "What is the business criticality of [component/data]?"
- "What is your organization's risk tolerance?"
- "How would [incident scenario] impact business operations?"

### Stage 5: Mitigation Strategy
**Agent May Ask:**
- "Are there existing security controls for [threat]?"
- "What is the feasibility of implementing [control]?"
- "Are there budget constraints for security investments?"

### Stage 6: Final Report
**Agent May Ask:**
- "Does the executive summary capture your primary concerns?"
- "Is the level of technical detail appropriate for intended audience?"

---

## Documenting Clarifying Questions

**MANDATORY:** All clarifying questions and responses MUST be logged.

| Item | Requirement |
|------|-------------|
| **File** | `{stage-number}_clarifying_questions.md` |
| **Location** | `[target]/output/threat-model/` |
| **Content** | Question, response, how incorporated |
| **Cross-Reference** | `*Source: User clarification (see Question [N])*` |

---

## User Response Protocol

**During Active Sessions:** Responses expected within same session

**If Delayed:**
- Continue waiting, document current state
- Provide status when user returns
- **DON'T:** Switch to Automatic Mode without explicit request

**Mode Change:** User may request "Switch to Automatic Mode" - agent confirms and documents

---

## Quality Validation

### Critic Phase (If Enabled)
- Critic reviews independently
- Critic identifies issues
- Critic does NOT approve (user approves)

### User Review Phase
- User reviews work (and critic findings if critic enabled)
- User may provide additional context
- User decides when standards are met

### Approval
- User explicitly approves progression
- User may request iterations regardless of critic assessment (if enabled)
- Approval documented in output files

**Note:** When critic review is disabled (default), user review serves as the primary quality gate.

---

## When to Use Collaborative Mode

**Recommended:**
- User can answer architecture questions
- User can provide business context
- Real-time clarification improves quality significantly
- Business context critical for risk assessment

**Benefits:**
- Higher quality through domain expertise
- Early clarification prevents rework
- Stakeholder buy-in for implementation
- Documentation captures institutional knowledge
