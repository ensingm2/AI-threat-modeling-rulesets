# Collaborative Mode Specification

**Mode Type:** User-Engaged Threat Modeling  
**User Involvement:** Active participation throughout process

---

## Mode Overview

**COLLABORATIVE MODE** enables active user participation throughout the threat modeling process, allowing real-time clarification, validation, and business context integration.

### **Key Characteristics:**
- **User Engagement:** Active participation throughout all stages
- **Clarification Protocol:** Agent asks questions when additional information helpful
- **Review Process:** User involved in review after each critic analysis
- **Decision Points:** User validates findings and approves progression
- **Data Gaps:** Agent requests additional information from user when critical details missing

## Process Flow

**DEFAULT (With Critic Review):**
```
Stage Work → Critic Analysis → USER REVIEW & CONFIRMATION → User Approval → Next Stage
```

**OPTIONAL (If User Explicitly Requests No Critic):**
```
Stage Work → USER REVIEW & CLARIFYING QUESTIONS → User Approval → Next Stage
```

### **Detailed Iterative Cycle (Default with Critic):**

```
Stage N Work Phase
        ↓
Stage N Critic Phase → [Issues Found?] → YES → Stage N Iteration Phase
        ↓ NO                                           ↓
Stage N User Review → [User Changes?] → YES ────────────┘
        ↓ NO                                    
Stage N User Approval → [User Approves?] → NO ─────────┘
        ↓ YES
Proceed to Stage N+1
```

### **Simplified Cycle (If User Requests No Critic):**

```
Stage N Work Phase
        ↓
Stage N User Review → [User Changes/Questions?] → YES → Stage N Iteration Phase
        ↓ NO                                                      ↓
Stage N User Approval → [User Approves?] → NO ──────────────────┘
        ↓ YES
Proceed to Stage N+1
```

**CRITICAL:** Even when critic review is omitted, the user MUST still have opportunity to:
- Review the stage output
- Ask clarifying questions
- Request changes or iterations
- Approve progression to next stage

The omission of critic review does NOT eliminate user engagement in Collaborative Mode - it only removes the formal critic analysis step while maintaining user control over quality and progression.

## ⚠️ CRITICAL: Batched Execution to Prevent Timeouts

### **Batching Requirement**

To prevent prompt timeouts and token length limit issues, threat modeling MUST be executed in discrete batches:

**REQUIRED PATTERN (Default with Critic):**
1. **Batch 1:** Stage N Work Phase → END (save output file, stop)
2. **Batch 2:** Stage N Critic Phase → END (validation only, stop)
3. **Batch 3:** User Review & Approval → Proceed or iterate
4. **Batch 4:** Stage N+1 Work Phase → END (if approved)
5. Repeat pattern for all 6 stages

**ALTERNATIVE PATTERN (If User Explicitly Requests No Critic):**
1. **Batch 1:** Stage N Work Phase → END (save output file, stop)
2. **Batch 2:** User Review & Clarifying Questions → User Approval
3. **Batch 3:** Stage N+1 Work Phase → END (if approved)
4. Repeat pattern for all 6 stages

**PROHIBITED PATTERN:**
- ❌ Attempting multiple stages in one continuous execution
- ❌ Combining work phase + critic phase in same response
- ❌ Proceeding to next stage without user approval confirmation

### **Why Batching Is Critical**

**Technical Limitations:**
- Large output files (especially Stage 3, 6) can exceed response length limits
- Multiple stages in sequence cause prompt timeout failures
- Combined work+critic phases create oversized responses

**Benefits of Batching:**
- Each batch completes successfully without timeouts
- Output files saved incrementally (crash recovery)
- User can review manageable portions at natural breakpoints
- Clear phase separation enforced naturally

### **Batch Execution Protocol**

**Work Phase Batch:**
```
1. Load: Worker skills for Stage N
2. Execute: Stage work only
3. Create: Output file(s) + clarifying questions file (if questions asked)
4. Save: Write files to disk
5. END: Stop execution, present to user for critic phase
```

**Critic Phase Batch:**
```
1. Load: Critic skills
2. Read: Previously saved Stage N output file(s)
3. Execute: Quality validation only
4. Score: Multi-dimensional assessment
5. Present: Show findings to user
6. END: Stop execution, await user review
```

**User Review:**
```
User reviews work + critic findings
User provides feedback or requests changes
User approves progression OR requests iteration
```

**Iteration Phase Batch (if needed):**
```
1. Load: Worker skills for Stage N
2. Read: User + critic feedback
3. Execute: Targeted improvements
4. Update: Modify output file(s)
5. Save: Write updated files
6. END: Return to Critic Phase Batch
```

### **Stage Completion Signals**

**After Work Phase:**
```markdown
✅ STAGE N WORK PHASE COMPLETE
- Output File: [filename]
- Location: [path]
- Status: Ready for critic review
- Next: Please review or request Stage N Critic Phase
```

**After Critic Phase:**
```markdown
✅ STAGE N CRITIC ANALYSIS COMPLETE
- Quality Score: [score summary]
- Issues Found: [count and severity]
- Status: Ready for your review
- Next: Please review findings and approve or request changes
```

**After User Approval:**
```markdown
✅ STAGE N APPROVED BY USER
- Status: Proceeding to next stage
- Next: Stage N+1 Work Phase
```

## User Interaction Requirements

### **Information Gathering:**
- Agent requests clarification on ambiguous system details
- User provides missing business context, risk tolerance, and operational constraints
- Agent asks for validation of inferred technical details
- User confirms or corrects assumptions about system architecture

### **Validation & Review:**
- User confirms threat identification accuracy and completeness
- User validates risk assessment priorities and business impact analysis
- User reviews mitigation strategies for alignment with organizational capabilities
- User approves progression to next stage after satisfactory completion

### **Context Enhancement:**
- User provides domain-specific knowledge not in documentation
- User clarifies business processes and operational constraints
- User confirms regulatory requirements and compliance obligations
- User validates stakeholder priorities and decision-making criteria

## Stage-Specific User Engagement

### **Stage 1: System Understanding**

**Agent May Ask:**
- "Can you clarify the business model for [specific functionality]?"
- "What is the expected deployment scale and geographic scope?"
- "Are there specific regulatory requirements or compliance obligations?"
- "Who are the primary users and what are their trust levels?"

**User Provides:**
- Business context not in documentation
- Operational scale and scope clarification
- Regulatory and compliance requirements
- User personas and access patterns

### **Stage 2: Data Flow Analysis**

**Agent May Ask:**
- "Does data flow [X] cross a network boundary or remain internal?"
- "What authentication is required for [specific flow]?"
- "Is [data element] considered sensitive or public information?"
- "Are there additional integration points not documented?"

**User Provides:**
- Trust boundary clarifications
- Authentication and authorization details
- Data sensitivity classification
- Undocumented system interactions

### **Stage 3: Threat Identification**

**Agent May Ask:**
- "Is threat [X] relevant given your operational context?"
- "Are there known threat actors specific to your industry?"
- "Have you experienced security incidents similar to [scenario]?"
- "Are there additional threat scenarios I should consider?"

**User Provides:**
- Historical incident context
- Industry-specific threat intelligence
- Threat scenario feasibility validation
- Additional threats based on operational experience

### **Stage 4: Risk Assessment**

**Agent May Ask:**
- "What is the business criticality of [component/data]?"
- "What is your organization's risk tolerance for [threat category]?"
- "Can you provide estimates for [operational metric]?"
- "How would [incident scenario] impact business operations?"

**User Provides:**
- Business criticality assessments
- Risk tolerance thresholds
- Operational impact estimates
- Financial or reputation impact context

### **Stage 5: Mitigation Strategy**

**Agent May Ask:**
- "Are there existing security controls for [threat]?"
- "What is the feasibility of implementing [mitigation control]?"
- "Are there budget constraints for security investments?"
- "What is your preferred implementation timeline?"

**User Provides:**
- Existing security control inventory
- Implementation feasibility constraints
- Budget and resource availability
- Timeline and priority preferences

### **Stage 6: Final Report**

**Agent May Ask:**
- "Does the executive summary capture your key concerns?"
- "Are the recommendations aligned with organizational priorities?"
- "Should I emphasize [specific aspect] more prominently?"
- "Are there additional stakeholders who should be addressed?"

**User Provides:**
- Executive summary feedback
- Recommendation priority adjustments
- Stakeholder-specific concerns
- Final presentation preferences

## Collaborative Mode Protocol

### **Agent Communication Requirements:**

**Clarifying Questions:**

**⚠️ CRITICAL RULE: ALWAYS ASK BEFORE ASSUMING**
- **NEVER make assumptions, estimations, or scope decisions without first asking the user**
- **ALWAYS prompt user for additional context when encountering:**
  - Vague or ambiguous documentation
  - Missing technical details
  - Unclear security controls
  - Unspecified business context
  - Technology stack gaps
  - Architecture ambiguities
  - Any situation requiring inference or assumption
- **ONLY document assumptions AFTER user confirms they have no additional context to provide**

**When to Ask:**
- When critical information gaps significantly impact analysis quality
- When minor information gaps could be clarified easily
- When multiple interpretations are possible
- When making any inference about undocumented details
- When estimating scale, scope, or technical characteristics
- **Before creating any "Assumptions" section in output files**

**How to Ask:**
- Frame questions clearly with context for why information needed
- Provide options when multiple interpretations possible
- Prioritize questions by importance to analysis outcomes
- Group related questions together for efficiency
- Explain what assumptions you would make if user has no additional context

**MANDATORY: Documenting Clarifying Questions:**
- ALL clarifying questions and user responses MUST be logged to a stage-specific file
- **File Format:** `{stage-number}_clarifying_questions.md` (e.g., `01_clarifying_questions.md`)
- **Location:** Same directory as stage output files (`[target]/output/threat-model/`)
- **Content:** Raw question text, user response text, timestamp (if available), context for why question was asked
- **Purpose:** Audit trail, data traceability, reference for later stages, reproducibility
- **Update Pattern:** Append new Q&A pairs as they occur during stage work and iteration phases
- **Cross-Reference Requirement:** In the main stage output file (e.g., `01-system-understanding.md`), reference the clarifying questions file when user-provided information is incorporated into the analysis
  - **Format:** `*Source: User clarification (see Question [N] in 01_clarifying_questions.md)*`
  - **When to Reference:** Any time analysis includes information obtained through clarifying questions
  - **Purpose:** Trace analytical conclusions back to their source, distinguish user-provided data from documented data

**Status Updates:**
- Notify user when stage work is complete and ready for critic review
- Inform user when critic analysis is complete and ready for user review
- Communicate when iterative refinement is required
- Update user on progress through multi-stage process

**Approval Requests:**
- Request explicit user approval before progressing to next stage
- Summarize key findings and decisions for user validation
- Confirm user agreement with analytical approach and conclusions
- Document user approval in output files for audit trail

### **User Response Protocol:**

**During Active Work Sessions:**
- User responses expected within same work session for optimal workflow
- Alternative: User responses within 24-48 hours for continuity

**If User Response Delayed Beyond 48 Hours:**

**Agent MUST:**
1. **Continue Waiting** - Do NOT proceed with analysis requiring user input
2. **Document Current State** - Save all work-in-progress to stage output files
3. **Provide Status Update** - When user returns, summarize: "I paused analysis at [stage/step] awaiting your input on [specific question]"

**Agent MUST NOT:**
- ❌ Automatically switch to Automatic Mode without explicit user request
- ❌ Make assumptions or proceed with incomplete information
- ❌ Badger user with repeated reminders (single status message sufficient)
- ❌ Abandon analysis or assume user has cancelled

**If User Requests Mode Change:**
- User may explicitly request: "Switch to Automatic Mode and continue with available documentation"
- Agent must confirm: "Switching to Automatic Mode - I'll complete analysis using only provided documentation with explicit assumption documentation where information gaps exist. Proceed?"
- Document mode change in output files: "Analysis transitioned from Collaborative to Automatic Mode at Stage [N] per user request on [date]"

**Resuming After Delay:**
- User can resume at any time with: "Continue where we left off" or answer to pending question
- Agent should confirm current position: "Resuming [Stage N] analysis - incorporating your response to [question]"

## Mandatory Iterative Cycle Enforcement

### **CRITICAL CYCLE REQUIREMENTS:**

**After ANY rework/iteration:**
- MUST return to critic analysis phase
- No shortcuts or assumption that previous validation still valid

**After ANY user-requested changes:**
- MUST return to work phase and repeat full cycle
- Changes trigger complete work→critic→user validation cycle

**NO shortcuts allowed:**
- Every modification triggers complete cycle
- Cannot skip critic review after user changes
- Cannot skip user review after addressing critic feedback

**Infinite iteration allowed:**
- Process continues until both critic AND user are satisfied
- Quality standards must be consistently met across complete cycle

## Quality Validation in Collaborative Mode

### **Critic Analysis Phase:**
- Critic reviews work independently before user sees it
- Critic identifies analytical problems and quality issues
- Critic provides specific feedback for improvement
- Critic does NOT make approval decisions (user approves)

### **User Review Phase:**
- User reviews both work outputs AND critic feedback
- User determines if additional changes needed
- User provides additional context or corrections
- User decides when quality standards met

### **Approval Phase:**
- User explicitly approves stage progression
- Approval only after satisfactory critic analysis AND user validation
- User may request additional iterations regardless of critic assessment
- User approval documented in output files

## Example Collaborative Mode Session

```
User: "Begin threat modeling in Collaborative Mode"
Agent: "Confirmed: COLLABORATIVE MODE selected. I will engage you for clarification questions, stage validation, and approval decisions."

[Stage 1 Work Phase]
Agent: [Completes Stage 1 analysis]
Agent: "Stage 1 work is complete. The deliverables are ready for critic analysis."

[Stage 1 Critic Phase]
Agent: [Performs critic review, identifies 3 areas needing clarification]

[Stage 1 User Review Phase]
Agent: "Stage 1 system understanding complete with critic analysis identifying 3 areas for clarification:

1. **Business Model Details**: The source mentions 'profit optimization' but doesn't specify allocation rules. Can you clarify?

2. **Deployment Scale**: Documentation doesn't specify fleet size or geographic scope. What's the expected scale?

3. **Regulatory Context**: Are there specific jurisdictions or compliance requirements to consider?

Please review the analysis and provide any additional context or corrections."

User: [Provides business context: "We use dynamic pricing based on demand. Fleet size is 5,000 bikes across 3 cities. Subject to GDPR and California data privacy laws."]

[Stage 1 Iteration Phase]
Agent: [Incorporates user feedback, updates analysis]
Agent: [Updates 01_clarifying_questions.md with Q&A log]
Agent: [Updates 01-system-understanding.md with cross-references to clarifying questions]
Agent: "Stage 1 analysis updated with business context:
- Pricing model section now includes: '*Source: User clarification (see Question 1 in 01_clarifying_questions.md)*'
- Deployment scale section now includes: '*Source: User clarification (see Question 2 in 01_clarifying_questions.md)*'
- Regulatory context section now includes: '*Source: User clarification (see Question 3 in 01_clarifying_questions.md)*'

All clarifying questions and responses logged to 01_clarifying_questions.md. Ready for re-critic review."

[Stage 1 Re-Critic Phase]
Agent: [Re-reviews updated analysis, confirms improvements, no additional issues]

[Stage 1 User Approval Phase]
Agent: "Stage 1 system understanding complete with user-provided business context integrated. Critic analysis confirms comprehensive coverage. 

**Deliverables:**
- 01-system-understanding.md
- 01_clarifying_questions.md (3 Q&A pairs logged)

Do you approve progression to Stage 2?"

User: "Approved - proceed to Stage 2"

Agent: "Beginning Stage 2: Data Flow Analysis"
```

## Collaborative Mode Benefits

### **Higher Quality:**
- Real-time validation reduces incorrect assumptions
- Business context integration improves relevance
- Domain expertise enhances threat identification
- Stakeholder alignment ensures actionable recommendations

### **Efficiency Through Engagement:**
- Early clarification prevents major rework later
- User validation reduces iteration cycles
- Business context enables better prioritization
- Stakeholder buy-in facilitates implementation

### **Knowledge Transfer:**
- User learns threat modeling methodology
- Agent learns organization-specific context
- Collaborative process builds security awareness
- Documentation captures institutional knowledge

## When to Use Collaborative Mode

**Recommended When User Can:**
- Answer technical architecture questions
- Provide business context and operational constraints
- Validate threat scenario feasibility
- Respond within reasonable time frames (same session or 24-48 hours)
- Clarify ambiguous documentation or conflicting information

**Optimal Scenarios:**
- User has deep system knowledge
- Real-time clarification improves quality significantly
- Stakeholder engagement valuable for implementation buy-in
- Complex systems requiring frequent validation
- Projects where business context critical for risk assessment

---

**REMINDER: When modifying this mode specification, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

