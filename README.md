# AI-Assisted Threat Modeling Framework

**A first pass at an instruction framework for guiding AI agents in conducting comprehensive security threat modeling.**

> **⚠️ AI Tool Usage Disclaimer:**
> 
> This framework leverages AI language models to generate threat modeling analysis. **AI outputs are NOT guaranteed to be accurate, complete, or correct.** Large Language Models (LLMs) will hallucinate, make errors, and produce plausible-sounding but incorrect information. **All AI-generated threat models MUST be reviewed and validated by qualified security professionals.** This tool augments but does not replace human security expertise. Use at your own risk.

> **📋 Development & Testing Status:**
> 
> This framework is designed for **Cursor** with **Claude Skills** architecture and tested with **`claude-4.5-sonnet`**. Initial validation used an intentionally sparse target service (single text file description) in "Automatic" mode to verify the baseline methodology.
> 
> **⚠️ Limited Testing Scope:** Extensive testing with "Collaborative Mode" and diverse system types has not yet been performed. Users should expect to iterate and provide feedback on methodology refinements.
> 
> **⏱️ Resource Warning:** The complete six-stage process is time-intensive and may consume a large number of AI requests. Cursor Pro or premium plans are strongly recommended. (Note that in initial runs, Cursor only spent ~34 requests in thinking mode, which is 2x cost)

---

> #### Mike Notes:
> - This is a very quick, exploratory, first pass attempt at a TM instruction set. It has major issues. is NOT meant to be a replacement for human security engineers or a formal manual threat modeling process
> - While I think the Critic stages are essential to a "complete" implementation, the current solution does not justify the cost and needs more tuning. To avoid this, explicitly ask to "skip critic phases" during your initial prompt.
> - Output stages 4-6 (risk assessment, mitigation strategy, final report) are of dubious quality at best, but including them for experimentation/tuning.
> - External DFD output is pretty wrecked at the moment, don't rely on it.
> - The stage/phase methodology means running this takes a fairly extended period of time (but still less than actually performing a full TM manually). Ideally I want to split up stages/phases further and do a multi-agent setup to run things concurrently, where possible (If I expand on this)
---

## 🎯 Project Overview

This repository provides a **generalized rule and instruction set** to guide AI agents when performing threat models on target systems. Given an input set of resources (documents, code, API documentation, diagrams, etc.) that detail a target system, AI agents can systematically execute a multi-stage threat modeling process with (an attempt at) built-in quality assurance.

### Primary Goals

- **Systematic Methodology**: Six-stage threat modeling process integrating STRIDE, MITRE ATT&CK, and Kill Chain frameworks
- **Evidence-Based Quality**: Optional adversarial critic analysis attempting to improve analytical rigor without fabricated data (Note: Currently limited effectiveness due to shared agent context; can be disabled to reduce costs by 50-75%)
- **Target Agnostic**: Generalized framework which should (hopefully) be able to handle arbitrary targets, domains, levels of complexity, and completeness of documentation
- **Platform Agnostic**: Core instruction set works across AI platforms with platform-specific loaders (Cursor, GitHub Copilot)

---

## 🚀 Quick Start Guide

### Prerequisites

- **AI Platform**: Cursor, GitHub Copilot, or other AI coding assistant with file editing capabilities
- **Target Documentation**: System architecture docs, code, diagrams, API specs, etc.

### Setup & Execution Steps

1. **Clone this repository** to use as your threat modeling workspace
2. **Open in your AI editor of choice** (Developed with Cursor and GitHub Copilot in mind)
3. **Place target system documentation** in `targets/[system-name]/external-resources/`
4. **Initiate threat modeling** by asking:

   ```
   "Perform a threat model on the system described in 
   ./targets/[system-name]/external-resources/"
   ```

5. **Select operational mode** when prompted by the AI agent:
   
   **⚠️ The agent WILL (should?) ask you to choose a mode before starting analysis. It shouldn't allow you to proceed until you select one.**
   
   - **Collaborative Mode** (Recommended for Critical Systems):
     - **User Involvement:** You'll answer clarifying questions throughout the process
     - **Quality Control:** You'll review and approve each stage after quality validation
     - **Accuracy:** Higher quality through your domain expertise and business context
     - **Time Commitment:** Several hours of intermittent engagement over days/weeks
     - **Best For:** Critical systems, security-sensitive applications, when you have technical knowledge and availability
   
   - **Automatic Mode** (For Well-Documented Systems):
     - **User Involvement:** Hands-off analysis using only provided documentation
     - **Quality Control:** Internal AI-driven critic validation only
     - **Accuracy:** Limited by documentation quality; may have analytical gaps
     - **Time Commitment:** Initial setup only, then autonomous (several hours of AI processing)
     - **Best For:** Well-documented systems, non-critical applications, minimal user availability
   
   **⚠️ Important:** Mode cannot be changed mid-analysis without restarting from the beginning. Choose carefully based on system criticality and your availability.

6. **Follow the six-stage process** with optional critic analysis after each stage
   
   **Critic Review Stages (Optional):**
   - By default, the framework includes adversarial critic analysis after each stage
   - You can explicitly request to **skip critic reviews** to reduce runtime and cost
   - Simply state: *"skip critic reviews"* or *"omit critic stages"* when starting
   - **Trade-off:** Faster execution (50-75% cost reduction) vs. additional quality validation layer
   - **Note:** In Collaborative Mode, you'll still review and approve each stage output

7. **Review all AI outputs critically** - human expert validation is mandatory

---

## 📋 Threat Modeling Methodology

### Six-Stage Process

1. **System Understanding & Scoping**
   - Architecture analysis, component inventory
   - Trust boundary definitions, data asset catalog
   - Assumption documentation with confidence levels

2. **Data Flow Analysis**
   - Triple-format DFD output (Text/Markdown, Mermaid, Draw.io XML)
   - Trust boundary mapping, attack surface identification
   - Content equivalency validation across formats

3. **Threat Identification**
   - STRIDE + MITRE ATT&CK + Kill Chain integration
   - Generic technical threats + system-specific threats
   - Comprehensive coverage requirements (typically 15-25 threats for simple systems, 25-40 for medium complexity, 40+ for complex systems with 7+ major components)

4. **Risk Assessment**
   - CVSS v4.0 scoring with detailed justification (only when sufficient technical information available)
   - Likelihood assessment with operational context
   - Business impact analysis (qualitative when quantitative data unavailable)

5. **Mitigation Strategy**
   - Security controls mapped to specific threats
   - Implementation roadmap with feasibility assessment
   - Residual risk analysis

6. **Final Comprehensive Report**
   - Executive-ready consolidated deliverable
   - 7-section structure with priority-sorted threat inventory
   - Self-contained report with embedded diagrams

### Mandatory Output Files

**Every stage produces output files** in `targets/[system-name]/output/threat-model/` enabling:
- Stage recovery after crashes or interruptions
- Audit trail and version control
- Incremental progress tracking
- Stakeholder communication throughout analysis

---

## 🔍 Quality Assurance Framework

### Evidence-Based Validation

**Adversarial Critic System**: Separate Worker and Critic agent roles aim to improve quality control through:

- **Critic analysis after EVERY stage by default** (enabled unless explicitly disabled by user request)
- **Optional Omission**: You can request to skip critic reviews for efficiency: *"skip critic reviews"* or *"omit critic stages"*
- **Minimum Issues Required:** Must identify at least 2-3 genuine analytical problems per stage (more than 3 is acceptable and encouraged), UNLESS the work demonstrably meets all quality standards after thorough critical analysis, in which case explicit justification is required explaining why fewer issues exist
- **Multi-dimensional quality scoring** (Data Integrity, Methodological Rigor, Source Traceability, Analytical Depth, Stakeholder Utility)
- **Graduated approval system** (Confident ≥90%, Conditional 70-89%, Targeted Revision 40-69%, Major Rework <40%)

### ⚠️ Critic Review Trade-offs

**Why You Might Skip Critic Stages:**

While adversarial critic analysis is valuable **in theory**, the current implementation has significant limitations:

- **Shared Agent Context Problem**: The same AI agent performs both worker and critic roles, leading to context carryover and "rubber-stamping" despite mandatory issue requirements
- **High Resource Cost**: Critic analysis + iterative refinement phases account for **50-75% of total runtime and prompt usage**
- **Limited Value Add**: Given the rubber-stamping tendency, the actual quality improvement often doesn't justify the substantial cost increase

**When to Use Critic Reviews:**
- Complex, high-stakes systems where additional validation layer is worth the cost
- When you have budget/time for comprehensive analysis
- Experimental runs to evaluate critic effectiveness for your use case

**When to Skip Critic Reviews:**
- Well-documented systems with clear architecture
- Resource-constrained scenarios (time, budget, API limits)
- When **you** (the human expert) will provide the quality review in Collaborative Mode
- Most practical threat modeling scenarios given current implementation limitations

**Future Improvement**: Multi-agent architecture with proper context separation should resolve the rubber-stamping issue and make critic reviews more valuable.

### Zero-Tolerance Data Fabrication Prevention

**PROHIBITED (Automatic Rejection)**:
- Technical stack fabrication (specific frameworks/databases without source documentation)
- Architecture invention (API patterns, schemas not documented in sources)
- Business metrics (revenue, user counts without documented basis)
- Operational scale assumptions (fleet sizes, deployment scope without specification)

**REQUIRED Approach**:
- All claims traced to specific source documentation with quotes
- Explicit assumption flagging with confidence levels (HIGH/MEDIUM/LOW/INSUFFICIENT)
- Generic technical analysis when implementation details unknown
- Transparent acknowledgment of data limitations

---

## ⚠️ Important Disclaimers

### No Guarantees, Support, or Responsibility

This framework is provided **as-is** with:

- ❌ **No suggestions, guarantees, or assurances** of correctness or completeness
- ❌ **No promises of support** should issues arise
- ❌ **No warranty** of fitness for any particular purpose
- ❌ **No responsibility** for any problems, damages, consequences, AI service costs, overage fees, rate limits, or account issues arising from usage

### AI Limitations Apply

**Large Language Models (LLMs) have inherent limitations:**

- **Hallucinations will occur** - AI agents may generate plausible but incorrect information
- **Errors are inevitable** - Technical inaccuracies, logical gaps, and analytical mistakes will happen
- **Human oversight is mandatory** - Security experts must review all outputs critically

### Expert-in-the-Loop Required

**This framework augments, not replaces, human security expertise:**

✅ **Security experts MUST**:
- Provide sufficient context about target systems
- Review all AI-generated analysis critically
- Validate technical claims against source documentation
- Correct errors and hallucinations promptly
- Make final risk and mitigation decisions

❌ **Do NOT**:
- Blindly trust AI-generated threat models
- Use outputs without thorough expert review
- Apply recommendations without validation
- Rely on this framework for compliance attestation without human verification

---

## 🛠️ Platform Information

This framework uses a **platform-agnostic core instruction set** with **platform-specific loaders**. Initially developed and tested with Cursor (`.cursorrules`) and GitHub Copilot (`.github/copilot-instructions.md`) using **`claude-4.5-sonnet`**.

**Architecture:**
- **Core Instructions**: `.ai-instructions/` directory contains platform-agnostic instruction files
- **Platform Loaders**: Small platform-specific files (`.cursorrules`, `.github/copilot-instructions.md`) load the core framework
- **Modular Design**: Claude Skills framework with specialized agent personas
- **Standard Formats**: Markdown documentation, Mermaid diagrams, standard file operations

**Platform Requirements:**
- Multi-turn conversation support
- File reading and writing capabilities
- Markdown rendering (for diagrams and documentation)
- Workspace/directory context awareness

---

## 🏗️ Repository Structure

```
.ai-instructions/                               # Cursor instructions (Claude Skills modular)
├── .cursorrules                         # Primary instruction file (auto-loads)
├── skills/                              # Modular skills framework
│   ├── README.md                         # Framework overview and getting started
│   ├── workflow-guide.md                 # Stage-by-stage guidance
│   ├── documentation-specialist/         # System understanding & DFD specialist
│   ├── threat-modeler/                   # Threat identification, risk, mitigation
│   ├── quality-critic/                   # Adversarial validation framework
│   └── shared/                           # Shared resources (terminology, confidence)
├── threat-modeling/                   # Supplementary DFD and report specs
├── quality-assurance/                 # Quality assurance framework
└── modes/                             # Operational modes (Collaborative/Automatic)

targets/[system-name]/
├── external-resources/                # Place target documentation here
└── output/threat-model/               # AI-generated outputs appear here
```

**Key Files:**
- **Primary Instructions**: `.cursorrules` (auto-loads at workspace root)
- **Methodology**: `.ai-instructions/skills/` directory with modular stage-specific guides
  - Documentation Specialist skills for Stages 1-2
  - Threat Modeler skills for Stages 3-6
  - Quality Critic skills for validation
- **Quality Framework**: `.ai-instructions/quality-assurance/` (modular framework with core-principles.md, validation-protocol.md, approval-criteria.md)
- **Operational Modes**: `.ai-instructions/modes/collaborative-mode.md` or `.ai-instructions/modes/automatic-mode.md`

---

## 📚 Documentation

### Core Documentation

- **[.cursorrules](.cursorrules)** - Primary instruction file (auto-loads at workspace root)
- **[.ai-instructions/README.md](.ai-instructions/README.md)** - Framework overview and quick start guide
- **[.ai-instructions/skills/README.md](.ai-instructions/skills/README.md)** - Skills framework overview and getting started guide
- **[.ai-instructions/skills/workflow-guide.md](.ai-instructions/skills/workflow-guide.md)** - Stage-by-stage workflow guide
- **[.ai-instructions/skills/](./.ai-instructions/skills/)** - Modular skills directory with specialized agent personas:
  - `documentation-specialist/` - System understanding and data flow analysis
  - `threat-modeler/` - Threat identification, risk assessment, and mitigation
  - `quality-critic/` - Adversarial validation framework
  - `shared/` - Core terminology, confidence calibration, and shared resources
- **[.ai-instructions/quality-assurance/](.ai-instructions/quality-assurance/)** - Modular quality validation framework (core-principles, validation-protocol, approval-criteria)
- **[.ai-instructions/modes/](.ai-instructions/modes/)** - Operational modes (Collaborative and Automatic)

The framework uses a modular Claude Skills approach organized around specialized agent personas for systematic threat modeling.

---

## 🔗 Related Resources

- **[STRIDE Threat Modeling](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-threats)** - Microsoft's threat classification framework
- **[MITRE ATT&CK](https://attack.mitre.org/)** - Adversary tactics and techniques knowledge base
- **[Cyber Kill Chain](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)** - Lockheed Martin's attack progression framework
- **[CVSS v4.0](https://www.first.org/cvss/v4.0/specification-document)** - Common Vulnerability Scoring System for risk quantification

---

## ⚠️ Known Issues

Based on initial testing:

- **Single-agent rubber stamping** - Critic retains worker context, leading to insufficient critical analysis despite mandated iterations
  - **Mitigation Available**: You can now explicitly request to skip critic stages, reducing cost by 50-75% while accepting that quality validation comes from human review instead
- **DFD generation** - The Data-flow documentation is alright, but the formatting of the mermaid and draw.io XML output tends to have syntax errors and needs tuning before "real" use.
- **Expectation anchoring** - Agent consistently hits suggested numeric ranges (e.g., "40-60 threats"), suggesting response tailoring
- **Unspoken assumptions** - Occasional implementation details assumed without documentation support
- **Meaningless metrics** - Confidence scores and impact ratings many times lack evidence. Likelihood, severity, prioritization, etc also don't have a high degree of accuracy and need human review.
- **Processing time** - Complete six-stage process with critic reviews takes ~1.75-2 hours on basic inputs
   - Note that work-only mode (no critic) reduces this by 50-75%

---

## 🔮 Potential Next Steps

- **Multi-agent architecture with proper worker/critic context separation** (HIGH PRIORITY)
   - Should resolve rubber-stamping issue by preventing context carryover between roles
   - Would make critic reviews genuinely valuable instead of expensive validation theater
   - Could introduce productive "churn" from different isolated agent types to promote iteration/refinement
   - Might speed things up if we can break up stages and effectively mapreduce
- Fix DFD generation for more complex views
- Final report generation rules need some tuning, the format of the report is fairly mediocre currently
- Remove numeric anchors from instructions to prevent response biasing

---

## 🙏 Attribution

**Framework created by:** Mike Ensing (ensingm2@gmail.com)  
**Initially developed during:** Adam Shostack's Threat Modeling Intensive with AI training at OWASP 2025 Global AppSec USA

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**Summary:**
- ✅ Commercial use, modification, distribution, and private use permitted
- ✅ Attribution required (license and copyright notice must be included)
- ❌ No warranty or liability

---

**Remember: This framework augments human security expertise but does not replace it. Always apply critical thinking and professional judgment to AI-generated threat models.**
