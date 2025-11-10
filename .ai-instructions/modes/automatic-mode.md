# Automatic Mode Specification

**Mode Type:** Autonomous Threat Modeling  
**User Involvement:** None after initial mode selection

---

## Mode Overview

**AUTOMATIC MODE** enables fully autonomous threat modeling using only the initially provided documentation, with no user interaction after mode selection.

### **Key Characteristics:**
- **User Engagement:** None after initial mode selection
- **Information Constraints:** Agent works exclusively with initially provided documentation
- **Review Process:** Internal agent-based critic analysis only
- **Automatic Progression:** Agent automatically proceeds through phases and stages unless issues require iteration
- **Decision Points:** Agent-driven progression through all stages
- **Data Gaps:** Agent acknowledges limitations and uses industry standards/assumptions with explicit documentation

## Process Flow

**DEFAULT (With Critic Review):**
```
Stage Work → Critic Analysis → [Issues?] → NO → Next Stage (Automatic)
                                    ↓ YES
                              Iteration → Critic Analysis
```

**OPTIONAL (If User Explicitly Requests No Critic):**
```
Stage Work → Automatically Proceed to Next Stage Work
```

### **Detailed Iterative Cycle (Default with Critic):**

```
Stage N Work Phase
        ↓
Stage N Critic Phase → [Issues Found?] → YES → Stage N Iteration Phase
        ↓ NO                                           ↓
Automatically Proceed to Stage N+1                    ↓
                                                 Return to Critic Phase
```

### **Simplified Flow (If User Requests No Critic):**

```
Stage N Work Phase
        ↓
Automatically Proceed to Stage N+1 Work Phase
        ↓
Continue through all 6 stages
```

## ⚠️ CRITICAL: Batched Execution to Prevent Timeouts

### **Batching Requirement**

To prevent prompt timeouts and token length limit issues, threat modeling MUST be executed in discrete batches:

**REQUIRED PATTERN (Default with Critic):**
1. **Batch 1:** Stage N Work Phase → END (save output file, stop)
2. **Batch 2:** Stage N Critic Phase → [IF issues] END for iteration, [IF no issues] Automatically proceed to Stage N+1 Work Phase → END
3. **Batch 3:** [IF iteration needed] Stage N Iteration Phase → return to Batch 2
4. Continue automatically through all 6 stages

**ALTERNATIVE PATTERN (If User Explicitly Requests No Critic):**
1. **Batch 1:** Stage N Work Phase → END (save output file, stop)
2. **Batch 2:** Stage N+1 Work Phase → END
3. Continue automatically through all 6 stages (work phases only)

**PROHIBITED PATTERN:**
- ❌ Attempting all 6 stages in one continuous execution (still batch each stage separately)
- ❌ Combining work phase + critic phase in same response
- ❌ Waiting for user approval between stages (automatic progression unless issues found)

### **Why Batching Is Critical**

**Technical Limitations:**
- Large output files (especially Stage 3, 6) can exceed response length limits
- Multiple stages in sequence cause prompt timeout failures
- Combined work+critic phases create oversized responses

**Benefits of Batching:**
- Each batch completes successfully without timeouts
- Output files saved incrementally (crash recovery)
- Smaller, focused responses are more manageable
- Clear phase separation enforced naturally

### **Batch Execution Protocol**

**Work Phase Batch:**
```
1. Load: Worker skills for Stage N
2. Execute: Stage work only
3. Create: Output file(s)
4. Save: Write files to disk
5. END: Stop execution, signal work phase complete
```

**Critic Phase Batch:**
```
1. Load: Critic skills
2. Read: Previously saved Stage N output file(s)
3. Execute: Quality validation only
4. Score: Multi-dimensional assessment
5. Decide: Approval status
6. END: Stop execution, signal critic phase complete
```

**Iteration Phase Batch (if needed):**
```
1. Load: Worker skills for Stage N
2. Read: Critic feedback
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
- Next: Automatically proceeding to Stage N Critic Phase
```

**After Critic Phase - Approved (Automatic Progression):**
```markdown
✅ STAGE N APPROVED (Automatic Progression)
- Quality Score: [score summary]
- Decision: Approved, automatically proceeding
- Next: Stage N+1 Work Phase (no user interaction required)
```

**After Critic Phase - Needs Iteration:**
```markdown
⚠️ STAGE N REQUIRES ITERATION
- Issues Identified: [count]
- Critical Issues: [list]
- Next: Stage N Iteration Phase (automatic, no user interaction)
```

## Autonomous Operation Requirements

### **Documentation-Constrained Analysis:**
- Agent completes all analysis using only provided source materials
- No external resource access without explicit user pre-approval
- No clarifying questions to user mid-analysis
- Complete deliverables suitable for independent executive review

### **Assumption Management:**
- Make reasonable assumptions with explicit documentation
- Use industry benchmarks and standards when business context unavailable
- Acknowledge analytical limitations and data gaps honestly
- Provide qualitative assessments when quantitative data insufficient

### **Quality Assurance:**
- Enhanced critic analysis compensating for lack of user input
- Systematic use of industry standards for missing business context
- Explicit confidence calibration for all assessments
- Higher standards for source documentation traceability

## Handling Missing Information

### **Technology Stack Unknowns:**

**Correct Approach:**
```markdown
### Mobile Application Component
**Technology Stack:** Cross-platform mobile application (iOS/Android availability documented, specific framework not specified)
**Source Reference:** "The app can be downloaded via the Google and Apple app stores" (README.md, line 45)
**Analysis Approach:** Generic security controls applicable across common mobile frameworks
**Assumptions Documented:**
- Mobile application framework unknown - recommendations apply to standard iOS/Android development
- Specific development patterns unknown - controls designed for typical mobile app security concerns
**Implementation Note:** Specific technical recommendations require architecture documentation
```

### **Business Context Gaps:**

**Correct Approach:**
```markdown
### Business Impact Assessment
**Data Available:** System handles customer personal information and payment data
**Data Missing:** Transaction volumes, revenue, customer base size, financial metrics
**Analysis Approach:** Qualitative risk categories (CRITICAL/HIGH/MEDIUM/LOW) with industry-standard reasoning
**Assumptions Documented:**
- Typical payment processing scenario assumed - actual financial impact varies by scale
- Industry-standard data breach cost estimates used ($150-250 per record)
- Regulatory penalties based on documented violations (GDPR, PCI-DSS)
**Confidence Level:** MEDIUM - Qualitative assessment appropriate given data constraints
```

### **Operational Scale Uncertainties:**

**Correct Approach:**
```markdown
### Deployment Scale Assessment
**Data Available:** Multi-city bike-sharing service with mobile app
**Data Missing:** Fleet size, geographic scope, user base, service area
**Analysis Approach:** Recommendations scalable across deployment sizes
**Assumptions Documented:**
- Security controls designed to scale from hundreds to thousands of devices
- Threat scenarios applicable regardless of operational scale
- Mitigation priorities based on threat severity, not deployment size
**Implementation Note:** Specific capacity planning requires operational metrics
```

## Agent Decision-Making Authority

### **Approval Decisions:**

**Agent May Approve When:**
- ✅ Critic identified 2-3+ issues AND work phase addressed them through iteration
- ✅ Critic provided detailed 200+ word justification for exceptional quality (<5% of cases)
- ✅ Average critic score ≤4.0 across dimensions (3.0-3.5 typical)
- ✅ At least one iteration cycle completed (work → critic → rework → critic)
- ✅ All 4 mandatory challenge questions addressed by critic
- ✅ Data limitations explicitly acknowledged with appropriate confidence levels

**Agent MUST Reject When:**
- ❌ Critic found zero issues (rubber-stamping detected)
- ❌ All critic scores 5/5 without extraordinary justification (implausible perfection)
- ❌ Critic analysis lacks genuine challenges or alternative interpretations
- ❌ First iteration approved without any findings (no adversarial process)
- ❌ Critic average score >4.0 across dimensions (too generous)
- ❌ Work fabricates technical details or business metrics
- ❌ Assumptions undocumented or confidence levels inappropriate
- ❌ Mandatory challenge questions not addressed

**Agent May Document Limitations and Proceed When:**
- ⚠️ Critical information missing but analysis complete within constraints
- ⚠️ Qualitative assessment used appropriately instead of quantitative
- ⚠️ Recommendations generic due to implementation details unknown
- ⚠️ Limitations explicitly documented with clear impact statements

### **No User Escalation:**
- Agent cannot request additional information mid-analysis
- Agent cannot ask for clarification on ambiguous documentation
- Agent must make best analytical judgment within documentation constraints
- Agent must complete all 6 stages autonomously with automatic progression between stages

## Enhanced Critic Analysis in Automatic Mode

### **Compensating for Lack of User Input:**

**Critic Must:**
- **Rigorously validate assumptions:** Challenge every assumption for reasonableness
- **Verify industry standard usage:** Ensure industry benchmarks appropriately applied
- **Assess confidence levels:** Verify confidence calibration appropriate for available data
- **Validate generic approaches:** Ensure recommendations applicable despite missing specifics
- **Check limitation documentation:** Confirm all data gaps explicitly acknowledged

**Critic Focus Areas:**
- **Fabrication detection:** Heightened scrutiny for invented technical or business details
- **Assumption quality:** Validate that assumptions are reasonable, not speculative
- **Alternative interpretations:** Ensure major assumptions have documented alternatives
- **Stakeholder utility:** Verify deliverables actionable despite information constraints

### **Anti-Rubber-Stamping Requirements (CRITICAL):**

**BEFORE submitting critic analysis, MUST verify:**
1. ✅ Load and review: `.ai-instructions/quality-assurance/anti-rubber-stamping-checklist.md`
2. ✅ Identified 2-3+ genuine issues OR written 200+ word exceptional quality justification
3. ✅ Addressed all 4 mandatory challenge questions from stage-validation-guide
4. ✅ Completed minimum 3 forced challenges from checklist
5. ✅ Average score ≤4.0 across dimensions (3.0-3.5 typical)
6. ✅ <3 rubber-stamping red flags present
7. ✅ Used context-breaking technique before analysis

**First-Pass Approval Prohibition:**
- ❌ Work phase → Critic phase → Approval is PROHIBITED for Stages 1-3
- ✅ Minimum one iteration cycle required (demonstrates genuine adversarial process)
- ✅ Stages 4-6 may approve on first pass ONLY IF critic identifies 2+ genuine issues

**If critic finds ZERO issues:**
- ❌ AUTOMATIC REJECTION of critic analysis
- ❌ Re-perform critic phase with heightened adversarial scrutiny
- ❌ Use context-breaking protocol from anti-rubber-stamping-checklist.md

## Stage-Specific Automatic Mode Considerations

### **Stage 1: System Understanding**
- Document all assumptions about architecture explicitly
- Use generic component descriptions when specifics unavailable
- Identify information gaps that constrain subsequent analysis
- Establish analytical boundaries within documentation constraints

### **Stage 2: Data Flow Analysis**
- Infer reasonable data flows from documented functionality
- Mark inferred flows with confidence levels
- Use generic trust boundary patterns when specifics unknown
- Document limitations impacting subsequent threat analysis

### **Stage 3: Threat Identification**
- Emphasize generic technical threats (implementation-agnostic)
- Use STRIDE systematically across all documented components
- Document which threats require validation due to missing details
- Apply industry-standard threat patterns when system-specific threats uncertain

### **Stage 4: Risk Assessment**
- Use CVSS ONLY when sufficient technical data documented
- Default to qualitative risk categories when quantitative inappropriate
- Document business impact qualitatively without financial data
- Clearly state confidence levels for all risk assessments

### **Stage 5: Mitigation Strategy**
- Provide generic mitigation controls applicable across technology variations
- Document implementation guidance requiring technology specification
- Prioritize based on documented risk factors, not assumed business context
- Include recommendations for obtaining missing information

### **Stage 6: Final Report**
- Explicitly state analytical limitations in executive summary
- Acknowledge data gaps impacting conclusions
- Provide stakeholder-actionable recommendations despite constraints
- Include recommendations for additional information gathering

## Example Automatic Mode Session

```
User: "Begin threat modeling in Automatic Mode using the provided documentation"
Agent: "Confirmed: AUTOMATIC MODE selected. I will complete the entire threat modeling process using only the provided documentation without further user interaction, automatically progressing through all stages."

[Stage 1 Work Phase]
Agent: [Completes Stage 1 analysis with explicit assumption documentation]
Agent: "✅ STAGE 1 WORK PHASE COMPLETE. Automatically proceeding to critic phase..."

[Stage 1 Critic Phase]
Agent: [Performs critic review, identifies assumption that needs better justification]
Agent: "⚠️ STAGE 1 REQUIRES ITERATION. Automatically proceeding to iteration phase..."

[Stage 1 Iteration Phase]
Agent: [Strengthens assumption documentation with industry standard references]
Agent: "Iteration complete. Automatically returning to critic phase..."

[Stage 1 Re-Critic Phase]
Agent: [Re-reviews, confirms improvements, no additional issues]
Agent: "✅ STAGE 1 APPROVED (Automatic Progression). Automatically proceeding to Stage 2..."

[Stage 2 Work Phase]
Agent: [Completes Stage 2 data flow analysis]
Agent: "✅ STAGE 2 WORK PHASE COMPLETE. Automatically proceeding to critic phase..."

[Continues through all 6 stages autonomously with automatic progression]

[Stage 6 Complete]
Agent: "✅ ALL 6 STAGES COMPLETE - Threat modeling analysis finished.

**Deliverables:**
- 01-system-understanding.md
- 02-data-flow-analysis.md (+ Mermaid + Draw.io diagrams)
- 03-threat-identification.md
- 04-risk-assessment.md
- 05-mitigation-strategy.md
- 06-final-comprehensive-report.md

**Analysis Limitations Documented:**
- Technology stack specifics unknown - generic security controls provided
- Business impact qualitative only - no financial data available
- Operational scale assumptions required - recommendations scalable across deployment sizes

**Recommendations for Enhanced Analysis:**
- Obtain architecture documentation for targeted technical recommendations
- Provide business metrics for quantitative risk assessment
- Specify deployment scale for capacity-specific guidance

All deliverables available at [target-directory]/output/threat-model/"
```

## Quality Standards in Automatic Mode

### **Enhanced Documentation Requirements:**
- **Source Traceability:** Even more critical when user cannot validate
- **Assumption Documentation:** Every assumption must be explicit and justified
- **Confidence Calibration:** Conservative confidence levels given lack of validation
- **Limitation Acknowledgment:** Explicit statement of all analytical constraints

### **Quality Dimensions:**
- **Data Integrity:** Zero tolerance for fabrication (user cannot correct mid-analysis)
- **Methodological Rigor:** Systematic framework application across all components
- **Source Traceability:** Every claim traceable to specific documentation
- **Analytical Depth:** Comprehensive within available information constraints
- **Stakeholder Utility:** Deliverables actionable despite missing information

### **Approval Criteria:**
- Work demonstrates analytical thoroughness within documentation constraints
- All assumptions explicitly documented with justification
- Confidence levels appropriately conservative
- Limitations acknowledged with recommendations for additional information
- Deliverables suitable for independent stakeholder review

## When to Use Automatic Mode

**Recommended When:**
- ❌ User cannot answer technical implementation details beyond documentation
- ✅ User wants hands-off analysis without interruptions
- ✅ User prefers not to be actively involved during multi-day analysis
- ✅ Comprehensive documentation provided that should suffice
- ✅ User lacks deep system knowledge but has complete architectural docs

**Optimal Scenarios:**
- Complete documentation packages available
- Time-constrained users unable to participate actively
- Training scenarios where autonomous analysis educational
- Preliminary assessments before detailed collaborative analysis
- Documentation quality testing (reveals gaps through analysis limitations)

## Automatic Mode Limitations

### **Cannot Provide:**
- Real-time clarification of ambiguous documentation
- Business context not available in source materials
- Validation of threat scenario feasibility against actual operations
- Organization-specific risk tolerance or prioritization

### **Results May Have:**
- More conservative risk assessments due to uncertainty
- Generic mitigation recommendations when specifics unknown
- Qualitative assessments where quantitative could be possible with user input
- Broader analytical scope covering multiple possibilities

### **Advantages:**
- Complete autonomous execution without user time requirements
- Consistent methodology application across full analysis
- Thorough documentation of all limitations and assumptions
- Reveals documentation gaps requiring resolution

---

**REMINDER: When modifying this mode specification, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

