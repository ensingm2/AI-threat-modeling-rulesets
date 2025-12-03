# Quality Critic - Examples

**Load:** As needed for reference

---

## 1. TECHNICAL FABRICATION DETECTION

### ❌ FAILED CRITIC REVIEW (Missed Fabrication)

```markdown
# CRITIC REVIEW - Stage 1
**Source Traceability:** Work demonstrates good source documentation usage
**Technical Architecture:** Analysis appropriately covers mobile app, backend, and IoT
**APPROVAL DECISION:** CONFIDENT APPROVAL - work meets quality standards
```

**Problem:** Missed fabricated technical details.

### ✅ PROPER CRITIC REVIEW (Catching Fabrication)

```markdown
# CRITIC REVIEW - Stage 1

## Issues Identified
1. **React Native claim**: No source documentation supports specific framework
   - Source states: "The app can be downloaded via the Google and Apple app stores"
   - Analysis fabricates: "React Native cross-platform framework"
   - **VIOLATION:** Technology stack invented without documentation

2. **PostgreSQL assumption**: No source specification of database technology

3. **REST API pattern**: Source shows API examples but doesn't specify pattern

## Required Corrections
- Remove all specific technology claims not supported by source quotes
- Replace with: "Cross-platform mobile application (framework unspecified)"
- Add assumption flags for architectural inferences

**DECISION:** MAJOR REWORK REQUIRED - Technical fabrication detected
```

### Common Fabrication Red Flags

| Type | Example | Fix |
|------|---------|-----|
| Framework names | "React Native", "Spring Boot" | "Mobile app (framework unknown)" |
| Database tech | "PostgreSQL 13.2" | "Database (type not documented)" |
| Cloud providers | "AWS Lambda" | "Cloud service (provider unknown)" |
| Auth mechanisms | "JWT tokens" | "Authentication (mechanism not documented)" |

---

## 2. MODE-SPECIFIC PROCESS EXAMPLES

### Correct Mode Selection Initiation

```
Agent: "Before beginning threat modeling, I need to confirm the operational mode:

**COLLABORATIVE MODE**: I'll ask clarifying questions and seek your review after each stage.

**AUTOMATIC MODE**: I'll complete all 6 stages autonomously using only provided documentation.

Which mode would you prefer?"

User: "Collaborative Mode"

Agent: "Confirmed: COLLABORATIVE MODE selected. I will engage you for clarification and approval throughout."
```

### Collaborative Mode Stage Flow

```
[Agent completes Stage 1 work]
[Agent performs Stage 1 critic analysis]

Agent: "Stage 1 complete. Critic analysis identified 3 areas for clarification:

1. **Business Model**: Can you clarify how customer prioritization works?
2. **Deployment Scale**: What's the expected fleet size and geographic scope?
3. **Regulatory Context**: Any specific compliance requirements?

Please review the analysis and provide context or corrections."

User: [Provides clarification]
Agent: [Incorporates feedback, seeks approval for Stage 2]
```

### Automatic Mode Stage Flow

```
[Agent completes Stage 1 work]
[Agent performs Stage 1 critic analysis]

Agent: "Stage 1 complete. Critic analysis identified 3 data gaps:

1. **Business Model**: Allocation rules not specified
   - ASSUMPTION: Standard queue-based allocation
   - CONFIDENCE: LOW

2. **Deployment Scale**: Fleet size not documented
   - ASSUMPTION: Regional deployment (100-1000 units)
   - CONFIDENCE: MEDIUM

3. **Regulatory Context**: Specific requirements not identified
   - ASSUMPTION: Standard data protection applies
   - CONFIDENCE: MEDIUM

Proceeding to Stage 2 with documented limitations."
```

### Iteration Examples

**Collaborative - User Requests Changes:**
```
User: "The allocation isn't queue-based - it uses ML-based demand prediction."

Agent: [Returns to Work Phase]
Agent: [Updates Stage 1 with corrected info]
Agent: [Re-performs Critic Phase]
Agent: "Updated. Critic validation confirms correction. Ready for your review."
```

**Automatic - Critic Identifies Issues:**
```
Critic: "TARGETED REVISION - Technology fabrication detected"

Agent: [Returns to Work Phase]
Agent: [Removes fabricated details, adds generic analysis]
Agent: [Re-performs Critic Phase]
Agent: "Revised. Proceeding to Stage 2."
```

---

## 3. SCORE CALIBRATION EXAMPLES

### Score 5/5 (Rare - Requires Justification)

```markdown
**Data Integrity: 5/5**
Justification (200+ words): This analysis demonstrates exceptional data integrity
through systematic source documentation. Every technical claim includes specific
file references with line numbers. The component inventory correctly identifies
8 components with explicit technology markings: 5 documented (with quotes),
2 inferred (with reasoning and alternatives), 1 unknown (appropriately marked).
No fabricated business metrics appear despite documentation gaps around scale...
[continues for 200+ words total]
```

### Score 3/5 (Most Common)

```markdown
**Data Integrity: 3/5**
Justification: Component inventory mostly sourced, but 2 technology inferences
lack alternative interpretations. Trust boundary analysis references Stage 1
but doesn't verify component names match exactly. No fabrications detected,
but confidence levels could be more conservative for inferred items.
```

### Score 1/5 (Major Issues)

```markdown
**Data Integrity: 1/5**
Justification: Multiple fabrications detected. "Node.js with Express" stated
without source - documentation only mentions "API endpoints." PostgreSQL
claimed but no database technology documented. Business metric "10,000 daily
users" appears without any source. Requires complete rework.
```
