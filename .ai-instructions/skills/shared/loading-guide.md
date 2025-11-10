# File Loading Guide | Reference: All Stages

**Purpose:** Centralized loading patterns for efficient context management

---

## Loading by Stage

### **Stage 1: System Understanding**
```
LOAD:
├── documentation-specialist/role-reminder.md
├── documentation-specialist/stage-1-guide.md
├── shared/core-terms.md
└── shared/confidence-calibration.md
```

### **Stage 2: Data Flow Analysis**
```
LOAD:
├── documentation-specialist/role-reminder.md (if not loaded)
├── documentation-specialist/stage-2-guide.md
├── shared/core-terms.md (if not loaded)
└── shared/output-file-requirements.md
```

### **Stage 3: Threat Identification**
```
LOAD:
├── threat-modeler/role-reminder.md
├── threat-modeler/stage-3-threat-identification.md
├── threat-modeler/frameworks/quick-reference.md
├── shared/core-terms.md (if not loaded)
└── shared/threat-modeling-terms.md
```

### **Stage 4: Risk Assessment**
```
LOAD:
├── threat-modeler/role-reminder.md (if not loaded)
├── threat-modeler/stage-4-risk-assessment.md
├── shared/core-terms.md (if not loaded)
├── shared/risk-assessment-terms.md
└── shared/confidence-calibration.md (if not loaded)
```

### **Stage 5: Mitigation Strategy**
```
LOAD:
├── threat-modeler/role-reminder.md (if not loaded)
├── threat-modeler/stage-5-mitigation-strategy.md
├── shared/core-terms.md (if not loaded)
└── shared/confidence-calibration.md (if not loaded)
```

### **Stage 6: Final Report**
```
LOAD:
├── threat-modeler/role-reminder.md (if not loaded)
├── threat-modeler/stage-6-final-reporting.md
├── documentation-specialist/role-reminder.md
├── documentation-specialist/stage-6-guide.md
└── shared/output-file-requirements.md
```

---

## Critic Phase (All Stages)

```
LOAD:
├── quality-critic/role-reminder.md
├── quality-critic/stage-validation-guide.md (specific stage section)
├── quality-assurance/core-principles.md (always)
├── quality-assurance/validation-protocol.md
└── quality-assurance/approval-criteria.md
```

**Optional (as needed):**
- `quality-assurance/examples/fabrication-detection.md`
- `quality-assurance/examples/cvss-validation.md` (Stage 4)
- `quality-assurance/examples/mode-specific-processes.md`

---

## Optional/Detailed Files

Load ONLY when comprehensive guidance needed:

### **Frameworks (Stage 3)**
- `threat-modeler/frameworks/detailed/stride.md` - Complete STRIDE guidance
- `threat-modeler/frameworks/detailed/mitre-attack.md` - Full tactic/technique listings
- `threat-modeler/frameworks/detailed/kill-chain.md` - Detailed stage descriptions

### **Confidence (All Stages)**
- `shared/confidence-calibration-detailed.md` - Extended examples and edge cases


---

## Context Optimization Tips

**ALWAYS Load:**
- Role reminder for current agent type
- Stage-specific guide
- Core terms (useful across all stages)

**Load Once, Retain:**
- Confidence calibration (used across stages)
- Core terms (used across stages)
- Output file requirements (referenced multiple times)

**Load As Needed:**
- Framework detailed files (Stage 3)
- QA examples (critic phase)
- Terminology category files (stage-specific)

**NEVER Load Unnecessarily:**
- Detailed files when quick reference sufficient
- Stage guides for stages not currently executing
- Examples when process is clear

---

## Path Shortcuts

**Quality Assurance:**
- `@qa/core` → quality-assurance/core-principles.md
- `@qa/validation` → quality-assurance/validation-protocol.md
- `@qa/approval` → quality-assurance/approval-criteria.md

**Skills:**
- `@tm/role` → threat-modeler/role-reminder.md
- `@ds/role` → documentation-specialist/role-reminder.md
- `@qc/role` → quality-critic/role-reminder.md

**Shared:**
- `@shared/core` → shared/core-terms.md
- `@shared/conf` → shared/confidence-calibration.md
- `@shared/output` → shared/output-file-requirements.md

---

**This guide centralizes loading patterns. Reference as needed to optimize context management.**

