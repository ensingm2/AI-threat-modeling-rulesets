# Skills Framework

**Purpose:** Modular, persona-based architecture for systematic threat modeling

---

## Quick Navigation

| Need | Go To |
|------|-------|
| **Full framework overview** | `../core/entry-point.md` |
| **Stage-by-stage execution** | `workflow-guide.md` |
| **Stages 1, 2, 6 (documentation)** | `documentation-specialist/SKILL.md` |
| **Stages 3, 4, 5, 6 (security)** | `threat-modeler/SKILL.md` |
| **Quality validation** | `quality-critic/SKILL.md` |
| **Terminology** | `shared/terminology.md` |
| **Confidence levels** | `shared/confidence-calibration.md` |
| **Critical rules** | `shared/critical-rules.md` |

---

## Skills Summary

| Skill | Stages | Role |
|-------|--------|------|
| **Documentation Specialist** | 1, 2, 6 (support) | Information extraction, documentation |
| **Threat Modeler** | 3, 4, 5, 6 | Security analysis, risk, mitigations |
| **Quality Critic** | All (validation) | Adversarial quality validation |

---

## Directory Structure

```
skills/
├── workflow-guide.md              # Stage transitions and loading patterns
├── documentation-specialist/
│   ├── SKILL.md                   # Skill definition
│   └── references/                # Stage 1, 2, 6 guides
├── threat-modeler/
│   ├── SKILL.md                   # Skill definition
│   └── references/                # Stage 3-6 guides + frameworks
├── quality-critic/
│   ├── SKILL.md                   # Skill definition
│   └── references/                # Validation guides
└── shared/                        # Cross-skill resources
    ├── terminology.md
    ├── confidence-calibration.md
    ├── critical-rules.md
    └── output-file-requirements.md
```

---

## Loading Pattern

**Each stage:** Load SKILL.md + stage guide + relevant shared resources  
**Critic phase:** Load quality-critic/SKILL.md + core-principles.md + stage-validation-guide.md  
**Details:** See `workflow-guide.md`
