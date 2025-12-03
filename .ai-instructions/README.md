# AI Assistant Framework for Threat Modeling

**Creator:** Mike Ensing (ensingm2@gmail.com)  
**Development:** Adam Shostack's Threat Modeling Intensive with AI, OWASP 2025 Global AppSec USA  
**Project:** LLM Instruction Sets and Methodology for Threat Modeling  
*Note: Attribution does not need to be included in generated threat model files.*

---

## 🚀 Getting Started

| Step | Action |
|------|--------|
| **1** | Read `core/entry-point.md` - Central framework overview |
| **2** | Read `skills/workflow-guide.md` - Stage execution patterns |
| **3** | Select target from `targets/` directory |
| **4** | **⚠️ MANDATORY: Agent asks BOTH questions in single prompt:** |
|       | • Operational mode: Collaborative or Automatic |
|       | • Critic Review mode: With Critic or Without Critic (default: OFF) |
| **5** | Load mode file and confirm BOTH selections |
| **6** | Begin Stage 1 following workflow guide |

**CRITICAL:** Steps 4-5 are NON-NEGOTIABLE. Never start Stage 1 without asking BOTH questions.

---

## Directory Structure

```
.ai-instructions/
├── core/
│   └── entry-point.md          # Central entry point (START HERE)
├── modes/
│   ├── collaborative-mode.md   # User-engaged mode
│   └── automatic-mode.md       # Autonomous mode
└── skills/                     # Modular skills framework
    ├── workflow-guide.md       # Stage loading patterns
    ├── documentation-specialist/
    ├── threat-modeler/
    ├── quality-critic/
    └── shared/
```

---

## 6-Stage Workflow

| Stage | Skill | Output |
|-------|-------|--------|
| **1** System Understanding | Doc Specialist | `01-system-understanding.md` |
| **2** Data Flow Analysis | Doc Specialist | `02-data-flow-analysis.md` |
| **3** Threat Identification | Threat Modeler | `03-threat-identification.md` |
| **4** Risk Assessment | Threat Modeler | `04-risk-assessment.md` |
| **5** Mitigation Strategy | Threat Modeler | `05-mitigation-strategy.md` |
| **6** Final Report | Both | `06-final-comprehensive-report.md` |

**Pattern (with Critic):** Work Phase → Critic Phase → Approval → Next Stage  
**Pattern (without Critic - default):** Work Phase → [User Review] → Next Stage

---

## Platform Support

| Platform | Loader File |
|----------|-------------|
| **Cursor** | `.cursorrules` (auto-loaded) |
| **GitHub Copilot** | `.github/copilot-instructions.md` |
| **Other** | Load `core/entry-point.md` manually |

---

## Key Principles

- **Evidence-based:** All claims traced to source documentation
- **Quality-assured:** Optional critic validation (valuable for multi-agent setups)
- **Multi-framework:** STRIDE + MITRE ATT&CK + Kill Chain
- **Confidence-calibrated:** HIGH/MEDIUM/LOW/INSUFFICIENT levels
- **Efficiency-aware:** Default settings optimized for single-agent runtime

---

## Maintenance Guidelines

When updating framework instructions:
1. Make changes to `.ai-instructions/` files (platform-agnostic)
2. Update platform loaders only if loading mechanism changes
3. Test changes with a sample threat model
4. Keep platform-specific features clearly marked
