# Technical Fabrication Detection - Examples | Load: As Needed | ~800 tokens

---

## ENHANCED EXAMPLES: TECHNICAL FABRICATION DETECTION

### **❌ FAILED CRITIC REVIEW (MISSED FABRICATION):**

```markdown
# CRITIC REVIEW - Stage 1
**Source Traceability:** Work demonstrates good source documentation usage
**Technical Architecture:** Analysis appropriately covers mobile app, backend, and IoT components
**Assumption Handling:** Key assumptions identified and documented
**APPROVAL DECISION:** CONFIDENT APPROVAL - work meets quality standards
```

**Problem:** This critic review missed multiple instances of fabricated technical details.

---

### **✅ PROPER CRITIC REVIEW (CATCHING FABRICATION):**

```markdown
# CRITIC REVIEW - Stage 1
**CRITICAL TECHNICAL FABRICATION IDENTIFIED:**
- **React Native claim**: No source documentation supports specific framework choice
  - Source states: "The app can be downloaded via the Google and Apple app stores"  
  - Analysis fabricates: "React Native cross-platform framework"
  - **VIOLATION:** Specific technology stack invented without documentation basis

**ADDITIONAL TECHNICAL ISSUES:**
- **PostgreSQL database assumption**: No source specification of database technology
- **REST API pattern claim**: Source shows API examples but doesn't specify architectural pattern
- **Microservices architecture**: Inferred from "serverless apps" but specific pattern not documented

**REQUIRED CORRECTIONS:**
- Remove all specific technology stack claims not supported by source quotes
- Replace with generic analysis: "Cross-platform mobile application (framework unspecified)"
- Add assumption flags for all architectural inferences
- Require technology specification for detailed security recommendations

**DECISION:** MAJOR REWORK REQUIRED - Technical fabrication violates evidence-based analysis standards
```

---

### **Critic Success Criteria for Technical Claims:**
- **Every specific technology must have source quote or be marked as assumption**
- **Generic recommendations must be used when technical details unknown**
- **Implementation guidance must acknowledge specification requirements**  
- **Architecture inferences must be clearly flagged and justified**

---

## Key Fabrication Red Flags

**Watch for these common fabrications:**

1. **Specific Framework Names** without source quotes
   - React Native, Angular, Spring Boot, Django, etc.
   - Database technologies (PostgreSQL, MongoDB, MySQL)
   - Cloud providers (AWS, Azure, GCP) without documentation

2. **Architectural Pattern Specifics**
   - "Microservices architecture" from vague descriptions
   - "RESTful API" vs other API patterns
   - "Event-driven architecture" assumptions

3. **Technology Stack Details**
   - Programming languages not documented
   - Deployment platforms assumed
   - CI/CD tools or processes

4. **Implementation Specifics**
   - Authentication mechanisms (JWT, OAuth, SAML)
   - Encryption algorithms or protocols
   - Session management approaches

**Proper Handling:**
- Use generic terminology: "Mobile application" not "React Native app"
- Flag as assumptions: "⚠️ ASSUMPTION: Likely uses REST API pattern based on..."
- Require specification: "Security recommendations require technology stack specification"

---

**This example demonstrates proper fabrication detection. Return to validation-protocol.md for complete validation procedures.**

