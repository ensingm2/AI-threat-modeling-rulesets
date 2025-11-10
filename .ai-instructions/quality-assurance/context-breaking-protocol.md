# Context-Breaking Protocol for Same-Agent Critic Analysis

**Purpose:** Overcome cognitive bias when same agent performs work and critic phases  
**Load:** MANDATORY before every critic phase  
**Scope:** All operational modes, all stages

---

## The Problem: Context Carryover Bias

### **Why Same-Agent Critic Analysis Fails:**

When the same agent performs work AND critic phases sequentially:

1. **Memory Persistence:** Agent remembers creating the work
2. **Decision Investment:** Agent has emotional attachment to own choices
3. **Reasoning Continuity:** Same analytical patterns persist across phases
4. **Confirmation Bias:** Agent seeks validation, not flaws
5. **Defense Mechanism:** Agent rationalizes decisions rather than challenging them

**Result:** Rubber-stamping with perfect scores, zero issues found, automatic approval

---

## Mandatory Context-Breaking Technique

### **STEP 1: Mental Model Reset (Required Before ALL Critic Phases)**

**Execute this mental script BEFORE beginning critic analysis:**

```
"I did NOT create this work.

A colleague - competent but fallible - created this analysis.
They made reasonable efforts but inevitably made mistakes.
They took shortcuts I need to identify.
They missed edge cases I need to find.
They were overconfident in some areas.

My job is NOT to validate their work.
My job is to FIND THEIR MISTAKES.

I will challenge their decisions.
I will question their assumptions.
I will identify what they missed.

This is not my work. This is someone else's work that needs improvement."
```

**Verification:** Write one sentence describing a flaw you expect to find before starting analysis.

---

### **STEP 2: Devil's Advocate Mode Activation**

**Adopt adversarial posture - your job is to DISAGREE:**

```
I MUST challenge major decisions.
I MUST propose alternatives.
I MUST question the approach.
I MUST find problems.

Even if choices seem reasonable, I will explore alternatives.
Even if work appears complete, I will identify gaps.
Even if methodology seems sound, I will question limitations.

My success is measured by issues found, not approval given.
```

**Action Items:**
- [ ] Identify 3 decisions you will challenge
- [ ] Prepare 2 alternative approaches to propose
- [ ] List 5 potential gaps to investigate

---

### **STEP 3: Forced Skepticism Assumption**

**Start with this foundational assumption:**

```
THIS WORK HAS FLAWS.

All work has flaws. This is not an exception.

The work contains:
- At least one overconfident assumption
- At least one missing edge case
- At least one inadequately justified decision
- At least one area that could be more thorough
- At least one limitation not explicitly stated

My job is to HUNT for these flaws, not verify their absence.
```

**Hunt For:**
- [ ] Overconfidence: Where are confidence levels too high?
- [ ] Hidden assumptions: What implicit assumptions are unstated?
- [ ] Missing scenarios: What edge cases weren't considered?
- [ ] Analytical shortcuts: Where did the worker take easier paths?
- [ ] Unstated limitations: What caveats should be explicit?

---

### **STEP 4: Stakeholder Perspective Adoption**

**View work through critical stakeholder eyes:**

#### **CISO Perspective:**
```
"If I were the CISO making security investment decisions based on this:

- What would make me question the analysis?
- What additional information would I demand before acting?
- What risks aren't clearly articulated?
- What scenarios could embarrass us if wrong?
- Where is the analyst being too optimistic about security posture?"
```

#### **Security Engineer Perspective:**
```
"If I were implementing security controls based on this:

- What technical details are missing that I need?
- What edge cases will I encounter that aren't documented?
- What failure modes weren't considered?
- What happens when assumptions prove incorrect?
- How will I know if my implementation addresses the threats?"
```

#### **Auditor Perspective:**
```
"If I were auditing this security assessment:

- Can all claims be traced to source documentation?
- Are confidence levels defensible?
- Are there unjustified leaps in logic?
- Could alternative interpretations exist?
- Would this withstand external scrutiny?"
```

**Critical Questions to Answer:**
1. What would make a CISO reject this analysis?
2. What would make a security engineer unable to implement recommendations?
3. What would make an auditor question the methodology?

---

## Mandatory Internal Monologue

### **Before Assigning ANY Score, Complete This Thought Process:**

**Write explicit responses to:**

1. **"What would make this analysis BETTER?"**
   - Minimum 2 specific improvements identified

2. **"What did the worker NOT consider?"**
   - Minimum 1 scenario/edge case/alternative missed

3. **"Where are the analytical shortcuts?"**
   - Minimum 1 area where more depth would improve quality

4. **"What am I being too generous about?"**
   - Minimum 1 dimension where score could be lower

**If you cannot answer all 4 questions:**
- ❌ Your critic analysis is INCOMPLETE
- ❌ Return to forced skepticism mode
- ❌ Do not proceed until you identify genuine issues

---

## Red Flag Self-Assessment

### **If ANY of These Are True, Context-Breaking FAILED:**

- ❌ I found zero issues
- ❌ I'm giving multiple 5/5 scores
- ❌ I'm approving on first pass
- ❌ I'm not proposing any alternatives
- ❌ I'm accepting all assumptions without challenge
- ❌ My analysis feels confirmatory, not adversarial
- ❌ I remember creating this work and defending it
- ❌ I'm thinking "this is pretty good" instead of "what's wrong with this"

**If 2+ red flags present:**
1. STOP critic analysis immediately
2. Re-execute STEPS 1-4 above with greater intensity
3. Force yourself to write "The most significant problem with this work is..."
4. Do not continue until you've identified genuine issues

---

## Practical Application Examples

### **Example 1: Challenging Assumptions**

**Worker's Assumption:**
> "The system uses HTTPS/TLS for all communications (MEDIUM confidence, inferred from PCI-DSS requirements)"

**Context-Breaking Critic Response:**
```
CHALLENGE: Could confidence be LOWER?

Alternative interpretation: PCI-DSS requires encryption for card data specifically,
not necessarily ALL communications. Bike telemetry, GPS updates, lock status
might use unencrypted protocols to reduce IoT device overhead.

ISSUE IDENTIFIED: Assumption confidence should be LOW, not MEDIUM.
Alternative scenario: Mixed encryption (card data HTTPS, telemetry unencrypted)
should be documented as possibility.

Impact if wrong: Threat model may underestimate attack surface if some communications
are actually cleartext.
```

---

### **Example 2: Identifying Missing Scenarios**

**Worker's Data Flow Analysis:**
> "22 data flows identified covering normal operations"

**Context-Breaking Critic Response:**
```
CHALLENGE: What scenarios are MISSING?

Missing edge cases:
- Error/exception flows: What happens when bike computer loses connectivity?
- Failure mode flows: What happens when payment processor times out?
- Admin flows: How do concierges remotely unlock bikes for maintenance?
- Recovery flows: What happens during system restart or crash recovery?

ISSUE IDENTIFIED: Analysis covers happy path only, missing ~8-10 error/admin flows.

Impact: Threat model will miss attack vectors related to error handling and
privileged operations.
```

---

### **Example 3: Questioning Methodology**

**Worker's Component Inventory:**
> "5 major components identified and analyzed"

**Context-Breaking Critic Response:**
```
CHALLENGE: Could component categorization be MORE GRANULAR?

Alternative approach: "BaaSCS Cloud Service" treated as single component,
but actually contains:
- Authentication service (identity management)
- Payment processing integration (PCI scope)
- Bike fleet management (operational data)
- Profit-o-matic AI system (customer discrimination)
- Ride tracking and billing (transaction processing)

ISSUE IDENTIFIED: Lumping these into single component masks different security
boundaries, trust zones, and threat profiles.

Impact: Threat identification will be less specific. Mitigation strategies
will be too generic. Different sub-components have different risk profiles.
```

---

## Success Criteria

### **You've Successfully Broken Context When:**

1. ✅ You identified 2-3+ genuine issues requiring worker attention
2. ✅ You challenged at least 3 assumptions or decisions
3. ✅ You proposed at least 1 alternative interpretation/approach
4. ✅ Your average score is ≤4.0 (typically 3.0-3.5)
5. ✅ You answered all 4 mandatory internal monologue questions
6. ✅ You feel adversarial, not confirmatory
7. ✅ You found things that would make stakeholders question the analysis

**If NOT all criteria met:**
- ❌ Context-breaking incomplete
- ❌ Re-execute protocol with greater intensity
- ❌ Do not submit critic analysis

---

## Integration with Other Quality Frameworks

**This protocol MUST be used in conjunction with:**

1. **Before starting:** Load and execute this context-breaking protocol
2. **During analysis:** Use `stage-validation-guide.md` technical validation criteria
3. **Before submitting:** Verify all items in `anti-rubber-stamping-checklist.md`
4. **Score calibration:** Reference `core-principles.md` score distribution standards
5. **Role mindset:** Review `quality-critic/role-reminder.md` adversarial incentives

---

## Protocol Compliance Verification

**Before submitting critic analysis, verify:**

- [ ] I executed Step 1: Mental Model Reset (wrote expected flaw)
- [ ] I executed Step 2: Devil's Advocate Mode (identified 3 challenges)
- [ ] I executed Step 3: Forced Skepticism (hunted for 5 flaw types)
- [ ] I executed Step 4: Stakeholder Perspectives (answered 3 critical questions)
- [ ] I completed mandatory internal monologue (answered all 4 questions)
- [ ] I verified <2 red flags present in self-assessment
- [ ] I reviewed practical examples and applied similar skepticism
- [ ] I met all success criteria for context-breaking

**If ANY checkbox unchecked:**
- ❌ Protocol not followed
- ❌ Context-breaking incomplete
- ❌ Critic analysis will be rejected
- ❌ Re-execute protocol completely

---

**This protocol is MANDATORY for all critic phases in same-agent scenarios. Skipping this protocol results in rubber-stamping and automatic rejection of critic work.**

