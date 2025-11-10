# Quality Assurance Framework - Modular Structure

**Purpose:** Evidence-based validation through systematic capability demonstration  
**Architecture:** Modular files optimized for dynamic context loading

---

## 📁 Directory Structure

```
quality-assurance/
├── README.md (this file)                  # Framework overview and loading guidance
├── core-principles.md                     # ALWAYS LOAD - Critical prohibitions and foundational principles (~1,500 tokens)
├── validation-protocol.md                 # LOAD FOR CRITIC WORK - 3-phase validation procedures (~2,000 tokens)
├── approval-criteria.md                   # LOAD FOR APPROVAL - Graduated decision framework (~800 tokens)
├── critic-review-template.md              # LOAD FOR STRUCTURE - Response template (~600 tokens)
└── examples/                              # OPTIONAL - Load specific examples as needed
    ├── fabrication-detection.md           # Technical claim validation examples (~800 tokens)
    ├── cvss-validation.md                 # Stage 4 CVSS scoring examples (~500 tokens)
    └── mode-specific-processes.md         # Collaborative vs Automatic mode examples (~600 tokens)
```

**Total Framework:** ~6,800 tokens (modular loading) vs ~18,000 tokens (monolithic)  
**Typical Load:** Core + Validation + Approval = ~4,300 tokens (76% reduction for common usage)

---

## 🎯 Loading Patterns

### **Initial Context Load (Minimal)**

When first starting threat modeling, load ONLY:
- **`core-principles.md`** (~1,500 tokens)

This provides critical prohibitions, role separation, and mode-specific approaches.

---

### **Critic Phase Load (Primary)**

When performing critic analysis after stage work:
1. **`core-principles.md`** (~1,500 tokens) - If not already loaded
2. **`validation-protocol.md`** (~2,000 tokens) - Complete validation procedures
3. **`approval-criteria.md`** (~800 tokens) - Decision framework

**Total:** ~4,300 tokens for complete critic capability

---

### **Approval Decision Load (Focused)**

When making final approval decision:
- **`approval-criteria.md`** (~800 tokens) - Graduated system
- **`critic-review-template.md`** (~600 tokens) - Structure guidance

**Total:** ~1,400 tokens for approval framework

---

### **Optional Reference Load (As Needed)**

Load specific examples only when guidance needed:
- **`examples/fabrication-detection.md`** - When uncertain about catching fabrication
- **`examples/cvss-validation.md`** - Stage 4 only, when validating CVSS scoring
- **`examples/mode-specific-processes.md`** - When clarifying mode behavior

**Advantage:** Load only relevant examples (~500-800 tokens each) instead of all examples

---

## 📋 File Purposes and Content

### **core-principles.md** (ALWAYS LOAD FIRST)
- Critical Prohibition: NEVER SKIP CRITIC ANALYSIS
- Mandatory Agent Role Separation
- Mode-Specific Quality Frameworks (Collaborative vs Automatic)
- Adversarial Incentive Structure
- Mandatory Iterative Cycle Enforcement

### **validation-protocol.md** (CRITIC WORK)
- Phase 1: Analytical Capability Demonstration
- Phase 2: Multi-Perspective Validation
- Phase 3: Data Integrity and Precision Validation
- Stage-Specific Validations (DFD, Threat Completeness, CVSS, Final Report)
- Critic Performance Standards
- Multi-Dimensional Quality Scoring

### **approval-criteria.md** (APPROVAL DECISIONS)
- Evidence-Based Approval Criteria
- Stage-Specific Capability Validation (1-6)
- Graduated Approval System (Confident/Conditional/Targeted/Major Rework)
- Quality Assurance Without Forced Iteration

### **critic-review-template.md** (RESPONSE STRUCTURE)
- Systematic Quality Validation Structure
- Mandatory Critic Response Language
- Analytical Rigor Framework
- Prohibited vs Required Behaviors

### **examples/** (OPTIONAL REFERENCE)
- Practical demonstrations of proper critic reviews
- Common failure patterns and corrections
- Mode-specific process illustrations
- CVSS validation specifics (Stage 4)

---

## 🚀 Usage Examples

### **Example 1: Starting Threat Modeling**

```markdown
Agent loads: .ai-instructions/quality-assurance/core-principles.md

Agent confirms: Mode selection, Critical prohibitions, Role separation understood
Agent proceeds: To Stage 1 work with foundational quality principles
```

### **Example 2: Performing Stage 3 Critic Analysis**

```markdown
Agent loads: 
- core-principles.md (if not in context)
- validation-protocol.md (for complete validation procedures)
- approval-criteria.md (for decision framework)

Agent performs: Systematic validation using 3-phase protocol
Agent checks: Stage 3 specific requirements (STRIDE completeness, threat count, etc.)
Agent decides: Using graduated approval criteria
```

### **Example 3: Uncertain About CVSS Validation (Stage 4)**

```markdown
Agent loads:
- validation-protocol.md (already loaded)
- examples/cvss-validation.md (for specific guidance)

Agent reviews: Examples of appropriate vs inappropriate CVSS usage
Agent applies: Proper validation criteria to Stage 4 work
```

---

## 🔄 Migration from Monolithic Framework

**Previous Structure:**
- Single file: `quality-assurance-framework.md` (~18,000 tokens)
- Required loading entire framework regardless of need

**New Structure:**
- Modular files with focused purposes
- Load only what's needed for current task
- Examples separated for optional reference

**Benefits:**
- 76% token reduction for typical usage (4,300 vs 18,000)
- Faster context loading and processing
- Easier maintenance and updates
- Clearer file purposes and navigation

---

## 🔗 Cross-References

**Referenced by:**
- `.cursorrules` - Points to core-principles.md for critical prohibitions
- `.ai-instructions/core/entry-point.md` - Links to complete framework
- `.ai-instructions/skills/quality-critic/stage-validation-guide.md` - Uses validation protocol

**References to:**
- `.ai-instructions/skills/shared/confidence-calibration.md` - Confidence level framework
- `.ai-instructions/skills/threat-modeling/stage-6-final-report-requirements.md` - Stage 6 specifics
- `.ai-instructions/modes/collaborative-mode.md` - Collaborative approach details
- `.ai-instructions/modes/automatic-mode.md` - Automatic approach details

---

## 📊 Token Optimization Summary

| Load Pattern | Files | Token Count | Reduction |
|--------------|-------|-------------|-----------|
| **Minimal (Start)** | core-principles.md | ~1,500 | 92% |
| **Critic Work** | core + validation + approval | ~4,300 | 76% |
| **Approval Only** | approval + template | ~1,400 | 92% |
| **With Examples** | All files | ~6,800 | 62% |
| **Previous (Monolithic)** | Single file | ~18,000 | Baseline |

---

**This modular structure enables efficient context loading while maintaining comprehensive quality assurance capabilities.**

