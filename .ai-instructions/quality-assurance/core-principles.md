# Quality Assurance - Core Principles | Load: Always | ~1,500 tokens

**Scope:** All threat modeling projects | **Modes:** Collaborative/Automatic  
**Related:** `validation-protocol.md`, `approval-criteria.md`, `critic-review-template.md`

---

## ❌ CRITICAL PROHIBITION: NEVER SKIP CRITIC ANALYSIS (Unless User Explicitly Requests) ❌

**DEFAULT RULE:** Critic analysis is MANDATORY and always expected after ANY stage completion. The agent must NEVER proactively offer to skip or bypass quality validation.

**EXPLICIT USER EXCEPTION:** If and ONLY if the user explicitly states they want to omit critic review stages (e.g., "skip critic reviews," "omit critic stages," "proceed without critic analysis"), then the agent may proceed directly from stage to stage performing only work phases.

**PROHIBITED QUESTIONS (NEVER ASK PROACTIVELY):**
- "Should I perform critic analysis or proceed to next stage?"
- "Would you like me to skip quality review?"
- "Do you want critic analysis or should I continue?"

**REQUIRED DEFAULT BEHAVIOR:** Complete stage work → Automatically proceed to critic analysis → Follow iterative cycles until quality standards met

**EXCEPTION BEHAVIOR (User-Requested Only):** Complete stage work → User review (Collaborative) or proceed to next stage (Automatic) → No critic phase

---

## REQUIREMENT: CRITIC ANALYSIS IS MANDATORY BY DEFAULT

**DEFAULT ENFORCEMENT:** Critic analysis is MANDATORY after every stage completion unless the user has explicitly requested to omit critic review stages.

**PERMITTED USER OVERRIDE:** The user may explicitly request to skip critic review stages for efficiency reasons (e.g., runtime, cost, shared context limitations). When this explicit request is made:
- **Collaborative Mode:** Proceed directly from work phase to user review, allowing user to review output and provide feedback, then continue to next stage
- **Automatic Mode:** Proceed directly from work phase to next stage work phase

**PROHIBITED AGENT BEHAVIOR (Unless User Has Explicitly Requested Omission):**
- ❌ NEVER ask "Should I perform critic analysis or proceed to next stage?"
- ❌ NEVER proactively offer to skip quality review or critic evaluation
- ❌ NEVER suggest proceeding without adversarial validation
- ❌ NEVER provide any option to bypass critic analysis

**DEFAULT SEQUENCE:** Work Phase → Critic Phase → Validation/Approval Phase → (Iteration if needed)

**USER-REQUESTED EXCEPTION SEQUENCE:**
- **Collaborative:** Work Phase → User Review & Clarifying Questions → User Approval → Next Stage Work Phase
- **Automatic:** Work Phase → Next Stage Work Phase

---

## CORE PRINCIPLE: ADVERSARIAL QUALITY VALIDATION (MODE-DEPENDENT)

### **Mandatory Agent Role Separation**

- **WORKER AGENT:** Complete deliverables ONLY - no validation, approval, or quality assessment permitted
- **CRITIC AGENT:** Seek flaws and problems ONLY - no work completion or approval decisions permitted  
- **USER VALIDATOR (Collaborative Mode):** Review critic findings, provide additional context, approve stage progression
- **AGENT VALIDATOR (Automatic Mode):** Make approval decisions based on critic analysis within documentation constraints
- **ABSOLUTE PROHIBITION:** Same agent performing both work and critic roles in same session/response under any circumstances

### **Mode-Specific Quality Validation Approaches**

#### **COLLABORATIVE MODE Quality Framework**

**User Engagement Integration with Mandatory Iterative Cycles:**
- Critic analysis followed by mandatory user review and validation
- **ANY modifications trigger return to work phase and complete cycle repetition**
- User provides missing business context and validates analytical assumptions  
- User confirms threat identification completeness and accuracy
- User approves risk prioritization and mitigation strategy alignment with business objectives
- **Quality validated through iterative refinement until both critic and user standards met**
- **No progression allowed until both critic analysis and user approval achieved**

**User Input Benefits:** Real-time clarification, business context validation, threat scenario confirmation, mitigation alignment with constraints

#### **AUTOMATIC MODE Quality Framework**

**Autonomous Quality Assurance with Mandatory Iterative Cycles:**
- Enhanced critic analysis compensating for lack of user input
- **ANY critic-identified issues trigger return to work phase and complete cycle repetition**
- Systematic use of industry benchmarks and standard practices when business context unavailable
- Explicit documentation of analytical limitations and confidence levels
- **Quality validated through iterative refinement until critic analysis standards consistently met**
- **No progression allowed until critic finds no significant issues requiring rework**

**Documentation-Constrained Analysis:** Enhanced traceability standards, explicit uncertainty handling, industry practices with caveats, quality measured by completeness within constraints

---

### **Adversarial Incentive Structure**

**Worker Success:** Comprehensive coverage, methodological soundness, complete traceability

**Critic Success:** Find genuine flaws (not rubber-stamp), identify real issues, actively challenge decisions

---

## CRITICAL: PREVENTING RUBBER-STAMPING IN SAME-AGENT SCENARIOS

### **Context Carryover Problem**

When the same agent performs work AND critic phases in sequence, context carryover creates bias:
- Agent remembers creating the work
- Agent has investment in defending own decisions
- Agent's reasoning patterns persist across phases
- **Result:** Rubber-stamping with perfect scores

### **MANDATORY MINIMUM FINDING REQUIREMENTS**

**The critic MUST identify AT LEAST ONE of:**
1. **2-3+ Genuine Issues** requiring iteration, OR
2. **1-2 Minor Observations** with detailed analysis, OR
3. **Explicit Justification** (minimum 200 words) explaining why work is genuinely exceptional

**If critic finds ZERO issues:**
- ❌ AUTOMATIC REJECTION of critic analysis
- ❌ Critic phase must be re-performed with heightened scrutiny
- ❌ 5/5 perfect scores require extraordinary justification

### **Score Calibration Standards**

**5/5 (Perfect):** EXTREMELY RARE - Reserved for work that:
- Exceeds all framework requirements significantly
- Shows innovative approach beyond baseline expectations
- Has demonstrably zero fabrication after extensive verification
- Demonstrates exceptional depth beyond typical analysis
- **Frequency: Expected <5% of stages**
- **Requires 200+ word justification**

**4/5 (Excellent):** Work meets all standards with minor observations
- Minor issues identified but work fundamentally sound
- **Frequency: Expected ~20% of stages**

**3/5 (Good):** Work adequate with some improvements needed
- Multiple observations requiring attention
- **Frequency: Expected ~50% of stages (MOST COMMON)**
- **This should be the typical score**

**2/5 (Needs Revision):** Multiple issues requiring rework
- Significant problems but approach salvageable
- **Frequency: Expected ~20% of stages**

**1/5 (Major Rework):** Fundamental problems
- Core methodology flaws requiring restart
- **Frequency: Expected ~5% of stages**

### **Average Score Reality Check**

**Across all stages, average score should be approximately 3.0-3.5/5.0**

If your average across multiple stages is >4.0/5.0:
- ❌ You are rubber-stamping
- ❌ Re-calibrate scoring standards
- ❌ Increase adversarial scrutiny

### **Forced Challenge Requirements**

**Critic MUST challenge at least 3 of the following per stage:**
- [ ] Are there alternative interpretations of ambiguous documentation?
- [ ] Could any confidence levels be lower given data quality?
- [ ] Are there missing edge cases or unusual scenarios?
- [ ] Could any assumptions be stated more conservatively?
- [ ] Are there inconsistencies between sections?
- [ ] Could any source references be more specific?
- [ ] Are there unstated limitations?
- [ ] What would a more thorough analysis include?
- [ ] Where are the analytical shortcuts?
- [ ] What scenarios weren't considered?

**Failure to challenge = Incomplete critic analysis**

### **First-Pass Approval Prohibition**

**In Automatic Mode:**
- Work phase → Critic phase → Approval is PROHIBITED
- Minimum one iteration cycle required for stages 1-3
- Demonstrates genuine adversarial process occurred
- Exception: Stages 4-6 may approve on first pass if 2+ issues identified and documented

---

## MANDATORY ITERATIVE CYCLE ENFORCEMENT

### **CRITICAL PROCESS REQUIREMENTS:**

**Work Phase Requirements:**
- Complete stage deliverables ONLY
- NO validation or approval activities permitted
- NO quality assessment or problem identification
- CREATE output files with complete stage work
- **END WORK PHASE** - worker role concludes

**Critic Phase:** Load validation criteria, validate systematically (NO work), identify issues, **END PHASE**

**Validation/Approval:** Collaborative (user reviews), Automatic (agent evaluates)

**Iteration:** Work Phase → Critic Phase → repeat until approved

**Progression:** Critic finds no major issues OR user approves (Collaborative)

---

### **VIOLATION PREVENTION:**

**❌ PROHIBITED BEHAVIORS:**
- Combining work and critic activities in same response
- Self-approval or self-validation of work
- Skipping critic phase after work completion
- Proceeding to next stage without critic approval
- Asking user if critic analysis should be skipped

**✅ REQUIRED BEHAVIORS:**
- Explicit phase separation with clear boundaries
- Automatic critic analysis after ALL stage work
- Iterative cycles until quality standards met
- Never offering option to skip quality validation

---

## Further Reading

For complete quality validation details, see:
- **`validation-protocol.md`** - Detailed 3-phase validation protocol
- **`approval-criteria.md`** - Graduated approval system and capability-based enforcement
- **`critic-review-template.md`** - Systematic review template and language standards
- **`implementation-guide.md`** - Process flow and success metrics
- **`examples/`** - Practical examples of proper critic review

---

**This file contains the foundational principles of the quality assurance framework. Load validation-protocol.md for detailed validation procedures.**

