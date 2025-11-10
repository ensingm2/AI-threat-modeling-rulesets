# Mode-Specific Process Examples | Load: As Needed | ~600 tokens

---

## MODE-SPECIFIC PROCESS EXAMPLES

### **✅ CORRECT Mode Selection Initiation:**

```
Agent: "Before beginning the threat modeling analysis, I need to confirm the operational mode:

**COLLABORATIVE MODE**: I will ask clarifying questions throughout the process and seek your review and confirmation after each stage's critic analysis. This enables real-time validation and business context integration.

**AUTOMATIC MODE**: I will complete the entire threat modeling process using only the provided documentation without further user interaction. This provides autonomous analysis with documented limitations.

Which mode would you prefer for this threat modeling assessment?"

User: "Please use Collaborative Mode - I want to be involved in validating the findings."

Agent: "Confirmed: COLLABORATIVE MODE selected. I will engage you for clarification questions, stage validation, and approval decisions throughout the threat modeling process."
```

---

### **COLLABORATIVE MODE Stage Example:**

```
[Agent completes Stage 1 work]
[Agent performs Stage 1 critic analysis]

Agent: "Stage 1 system understanding is complete with critic analysis identifying 3 areas for clarification:

1. **Business Model Details**: The source mentions 'profit optimization' but doesn't specify how customer prioritization works. Can you clarify the business rules for bike allocation?

2. **Deployment Scale**: The documentation doesn't specify fleet size or geographic scope. What's the expected operational scale?

3. **Regulatory Context**: Are there specific jurisdictions or compliance requirements I should consider?

Please review the analysis and provide any additional context or corrections."

User: [Provides business context and validation]
Agent: [Incorporates feedback and seeks approval for Stage 2]
```

---

### **AUTOMATIC MODE Stage Example:**

```
[Agent completes Stage 1 work]
[Agent performs Stage 1 critic analysis]

Agent: "Stage 1 system understanding complete. Critic analysis identified 3 data gaps:

1. **Business Model**: Source mentions 'profit optimization' but allocation rules not specified
   - ASSUMPTION: Standard queue-based allocation with premium tier prioritization
   - CONFIDENCE: LOW - business logic not documented

2. **Deployment Scale**: Fleet size and geographic scope not documented
   - ASSUMPTION: Regional deployment (100-1000 unit scale based on context)
   - CONFIDENCE: MEDIUM - inferred from service tier descriptions

3. **Regulatory Context**: Specific compliance requirements not identified
   - ASSUMPTION: Standard data protection (GDPR/CCPA) applies
   - CONFIDENCE: MEDIUM - based on customer data processing

Quality assessment: 8 of 10 components fully documented, 2 with explicit assumptions.
Proceeding to Stage 2 with documented limitations."
```

---

## Key Differences

| Aspect | Collaborative Mode | Automatic Mode |
|--------|-------------------|----------------|
| **User Involvement** | Active clarification and validation | None after mode selection |
| **Data Gaps** | Ask user for clarification | Document assumption with confidence level |
| **Stage Approval** | User reviews and approves | Agent decides based on critic findings |
| **Business Context** | User provides real-time input | Industry standards and documentation only |
| **Quality Bar** | Higher (user validation adds rigor) | Documentation-constrained |

---

## Iterative Cycle Examples

### **Collaborative Mode - User Requests Changes:**

```
User: "The bike allocation isn't queue-based - it uses ML-based demand prediction. Please revise."

Agent: [Returns to Work Phase]
Agent: [Updates Stage 1 with corrected business logic]
Agent: [Performs Critic Phase again]
Agent: "Updated analysis incorporates ML-based allocation. Critic validation confirms correction. Ready for your review."
```

### **Automatic Mode - Critic Identifies Issues:**

```
Critic: "MAJOR REWORK REQUIRED - Technical fabrication detected (specific frameworks without source)"

Agent: [Returns to Work Phase]
Agent: [Removes fabricated details, adds generic analysis]
Agent: [Performs Critic Phase again]
Agent: "Revised analysis removes fabricated technology stack details. Critic validation confirms correction. Proceeding to Stage 2."
```

---

**These examples demonstrate mode-specific behaviors. Return to core-principles.md for complete mode framework.**

