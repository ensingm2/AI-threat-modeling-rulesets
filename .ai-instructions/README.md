# AI Assistant Framework for Threat Modeling

---

**Attribution & Development Context**

**Creator:** Mike Ensing (ensingm2@gmail.com)

**Development:** Initial implementation developed during Adam Shostack's Threat Modeling Intensive with AI training at OWASP 2025 Global AppSec USA.

**Project:** LLM Instruction Sets and Methodology for Threat Modeling

*Note for AI Agents: This attribution is for reference only and does not need to be included in generated threat model files.*

---

**Repository:** LLM Instruction Sets and Methodology for Threat Modeling  
**Purpose:** Platform-agnostic AI assistant instruction framework for security research and threat modeling

## 🚀 Getting Started

**New to this framework?** Start here:
- **`.ai-instructions/core/entry-point.md`** - Central framework entry point with complete overview (START HERE)
- **`.ai-instructions/skills/README.md`** - Complete skills framework overview and getting started guide
- **`.ai-instructions/README.md`** - This file - comprehensive framework documentation

**Critical Rules:** See `.cursorrules` for NEVER SKIP CRITIC ANALYSIS requirement and `.ai-instructions/core/entry-point.md` for complete prohibitions

---

## Directory Structure

### 📋 Core Instructions
- **`.cursorrules`** - Platform-specific loader for Cursor (auto-loads, ~1.5-2K tokens)
  - Minimal loader with critical prohibitions inline
  - References centralized instruction repository
  - Points to `.ai-instructions/core/entry-point.md` for complete framework
- **`.ai-instructions/core/`** - Central framework documentation (platform-agnostic)
  - `entry-point.md` - Complete framework overview and entry point for all platforms
  - Multi-target security research operational guidelines
  - Critical prohibitions (NEVER SKIP CRITIC, NEVER FABRICATE, etc.)
  - Platform-specific integration notes

### 🎭 Skills Framework (PRIMARY)
**Directory:** `skills/`  
**START HERE** - This is the main threat modeling approach

- **`README.md`** - Framework overview and getting started guide (main entry point)
- **`workflow-guide.md`** - Deterministic stage-by-stage loading patterns and transitions
- **`documentation-specialist/`** - Technical documentation extraction and organization (Stages 1, 2, 6)
  - `role-reminder.md` - Documentation Specialist role reminder (~100 tokens)
  - `stage-1-guide.md` - System understanding documentation work
  - `stage-2-guide.md` - Data flow analysis and triple-format DFD creation
  - `stage-6-guide.md` - Final report formatting and organization
- **`threat-modeler/`** - Security analysis and threat identification (Stages 3, 4, 5, 6)
  - `role-reminder.md` - Threat Modeler role reminder (~150 tokens)
  - `stage-1-system-understanding.md` - Alternative Stage 1 approach (points to doc-specialist)
  - `stage-2-data-flow-analysis.md` - Alternative Stage 2 approach (points to doc-specialist)
  - `stage-3-threat-identification.md` - STRIDE + ATT&CK + Kill Chain threat modeling
  - `stage-4-risk-assessment.md` - CVSS scoring and risk prioritization
  - `stage-5-mitigation-strategy.md` - Security control recommendations
  - `stage-6-final-reporting.md` - Comprehensive report content assembly
  - `frameworks/` - STRIDE, MITRE ATT&CK, Kill Chain framework guidance
    - `quick-reference.md` - Consolidated framework quick reference
    - `detailed/` - Detailed framework files (stride.md, mitre-attack.md, kill-chain.md)
- **`quality-critic/`** - Adversarial validation for all stages
  - `role-reminder.md` - Quality Critic role reminder (~200 tokens)
  - `stage-validation-guide.md` - Stage-specific validation criteria
- **`shared/`** - Common resources used across all skills
  - `core-terms.md` - Core architectural and methodology terminology
  - `threat-modeling-terms.md` - Threat modeling specific terms
  - `risk-assessment-terms.md` - Risk assessment specific terms
  - `confidence-calibration.md` - Confidence level definitions (HIGH/MEDIUM/LOW/INSUFFICIENT)
  - `output-file-requirements.md` - Output format specifications
  - `loading-guide.md` - Centralized loading patterns reference

**Skills Framework Features:**
- ✅ Modular, persona-based architecture with clear role separation
- ✅ Deterministic, repeatable workflows with explicit stage-by-stage loading
- ✅ Systematic separation of documentation work from security analysis
- ✅ Rigorous quality validation with mandatory adversarial critic review
- ✅ Evidence-based process with anti-fabrication controls
- ✅ Mandatory output files for each stage (stage recovery, audit trail)

### 🎯 Supplementary Specifications
**Directory:** `threat-modeling/`  
*Referenced by skills framework for detailed format specifications*
- **`stage-2-dfd-requirements.md`** - Data Flow Diagram format specifications
  - Triple-format DFD requirements (Text/Markdown, Mermaid, Draw.io XML)
  - Content equivalency validation criteria
  - Platform-specific validation tools and preview capabilities (optional)
- **`stage-6-final-report-requirements.md`** - Comprehensive final report structure
  - Executive summary, architecture overview, priority-sorted threats, recommendations
  - Self-contained deliverable specifications
  - Multi-file consistency verification

### 🔍 Quality Assurance Framework  
**Directory:** `quality-assurance/`
- **`README.md`** - Modular quality assurance framework overview and loading patterns
- **`core-principles.md`** - Critical prohibitions and foundational quality principles (~1,500 tokens)
- **`validation-protocol.md`** - 3-phase validation procedures for critic analysis (~2,000 tokens)
- **`approval-criteria.md`** - Graduated approval system and stage-specific validation (~800 tokens)
- **`critic-review-template.md`** - Systematic response structure (~600 tokens)
- **`examples/`** - Optional reference examples (fabrication detection, CVSS validation, mode processes)
  - Graduated approval system eliminating forced iterations
  - Evidence-focused validation preventing rubber-stamping
  - Platform-agnostic quality validation workflows

### 🔧 Cross-System Maintenance
- **`CROSS_SYSTEM_VERIFICATION_CHECKLIST.md`** - Verification checklist for maintaining consistency
  - Core concepts checklist (6-stage methodology, quality assurance, operational modes)
  - Platform file mapping and verification workflow
  - Change log template and rollback protocol

## Framework Integration & Usage

### 🔄 Process Flow
1. **Platform Loader:** Platform-specific file (`.cursorrules` for Cursor, `.github/copilot-instructions.md` for Copilot) loads framework
2. **Central Entry Point:** `core/entry-point.md` provides complete framework overview (platform-agnostic)
3. **Skills Framework:** `skills/README.md` details approach and getting started guide
4. **Target Selection:** Review `targets/README.md` and select appropriate target
5. **Execute Workflow:** Follow `skills/workflow-guide.md` for deterministic 6-stage execution
6. **Quality Validation:** Mandatory critic review after each stage (see `quality-assurance/README.md`)

### 🎯 Key Innovations

#### **Evidence-Based Quality Assurance**
- Separate Worker and Critic agent roles with quality-focused validation
- Analytical capability demonstration through systematic evidence-based review
- Multi-dimensional quality scoring with graduated approval system
- Elimination of forced iterations while maintaining rigorous standards

#### **Data Integrity Enforcement**
- Mandatory source documentation traceability for all claims
- Explicit prohibition of fabricated business metrics and technical details
- Appropriate confidence level documentation and uncertainty handling
- Clear distinction between documented evidence and analytical assumptions

#### **Systematic Methodology with Capability Gates**
- 6-stage threat modeling process with evidence-based quality validation
- Multi-framework integration (STRIDE + ATT&CK + Kill Chain)
- Systematic progression from architecture analysis through mitigation planning
- Quality-driven progression based on demonstrated analytical competence

## Key Framework Features

### **Platform Capabilities Leveraged**
- **Workspace Context:** Multi-file awareness for cross-stage consistency
- **Real-time Validation:** Integrated linting and preview for immediate feedback (platform-dependent)
- **Version Control:** Git integration to track changes and iterations
- **File Comparison:** Compare multiple outputs for validation
- **Diagram Rendering:** Mermaid diagram preview in markdown (platform-dependent)

### **Core Features**
- **Evidence-based validation** with analytical capability demonstration
- **Multi-dimensional quality scoring** with graduated approval system
- **Systematic methodology** with quality-driven progression eliminating forced iterations
- **Target-agnostic design** supporting diverse security research projects with scalable rigor

## Quick Start Guide

### **Getting Started:**

1. **Setup:** Open workspace in your AI platform (Cursor, GitHub Copilot, etc.) - platform loader loads automatically
2. **Review Framework:** Read `core/entry-point.md` for complete framework overview, then `skills/README.md` for detailed getting started guide
3. **Select Target:** Choose from `targets/` directory with target-specific instructions  
4. **Select Mode:** Agent will ask for Collaborative or Automatic mode (MANDATORY before Stage 1)
5. **Begin Stage 1:** Load `skills/documentation-specialist/stage-1-guide.md` to start
6. **Follow Workflow:** Use `skills/workflow-guide.md` for stage-by-stage progression with automatic critic validation

### **Platform Capabilities Utilized:**

- **Multi-File Context:** Workspace context for cross-file references and consistency
- **Markdown Rendering:** View Mermaid diagrams and formatted reports
- **File Operations:** Read source documentation, write analysis outputs
- **Conversation History:** Maintain context across multi-turn threat modeling sessions
- **Search Capabilities:** Find references across documentation and code

**Critical Principle:** All analytical claims must be evidence-based with appropriate uncertainty acknowledgment and source traceability.

## Framework Scope & Constraints

**Defensive Security Research Only** - No offensive capabilities or active system testing  
**User Approval Required** - All external documentation access requires explicit permission  
**Quality Through Evidence** - Systematic validation demonstrates analytical rigor without artificial iterations  
## Platform Implementation

**Platform-Agnostic Core:**
- `.ai-instructions/` directory contains all core instruction files
- Modular skills framework works across platforms
- Standard markdown, Mermaid, and file formats

**Platform-Specific Loaders:**
- **Cursor:** `.cursorrules` file at workspace root (automatically loaded)
- **GitHub Copilot:** `.github/copilot-instructions.md` for VS Code integration
- **Other Platforms:** Create similar loader file pointing to `core/entry-point.md`

**Required Platform Capabilities:**
- Custom instruction loading from files
- Multi-turn conversation support
- File reading and writing capabilities
- Workspace/directory context awareness
- Markdown rendering (for documentation and diagrams)

### **Updating Instructions:**

When updating framework instructions:
1. Make changes to `.ai-instructions/` core files (platform-agnostic)
2. Update platform loaders only if loading mechanism changes
3. Test changes in your platform environment
4. Update documentation if methodology changes
5. Keep platform-specific features optional and clearly marked

## Implementation Workflow

### **Project Initiation:**
1. **Open Workspace:** Open `owasp-training` workspace in your AI platform
2. **Load Instructions:** Platform loader automatically loads framework
3. **Select Target:** Navigate to `targets/` and choose target system
4. **Confirm Mode:** Agent will ask for Collaborative or Automatic mode
5. **Begin Analysis:** Follow 6-stage methodology with mandatory critic reviews

### **Workflow Capabilities:**
- **Conversational Interface:** Ask questions and request clarifications
- **File Preview:** View markdown files with rendered Mermaid diagrams
- **Version Control:** Track iterations and modifications via git
- **Multi-File Work:** Work with multiple stage outputs simultaneously

### **Quality Assurance:**
- **Cross-Reference:** Use search to validate source documentation claims
- **Consistency Check:** Compare multiple stage files for alignment
- **Visual Validation:** Preview diagrams and reports for presentation quality
- **Iterative Refinement:** Leverage conversation history to maintain context

## Framework Adaptation

If you wish to adapt this framework for other AI platforms:
- **Core methodology** - 6-stage process with quality assurance
- **File organization** - Instruction files and stage-specific guides
- **Skills framework** - Modular persona-based architecture
- **Adaptation required** - Instruction loading, file operations, and workflow patterns will need platform-specific implementation

## Troubleshooting

### **Instructions Not Loading:**
- Verify platform loader exists (`.cursorrules` for Cursor, `.github/copilot-instructions.md` for Copilot)
- Restart your AI platform if instructions were recently added
- Check platform settings for custom instruction file loading

### **Preview Issues:**
- Ensure markdown preview is enabled in your platform
- Verify Mermaid syntax is valid (check for syntax errors)
- Try refreshing preview if available

### **Consistency Issues:**
- Use workspace search to find conflicting instructions
- Review all `.ai-instructions/` instruction files
- Ensure stage requirements align across all guide files

## Contributing

When contributing to this framework:
1. **Test changes** in your platform environment before committing
2. **Maintain consistency** across all `.ai-instructions/` instruction files
3. **Keep platform-specific features optional** and clearly marked
4. **Update this README** with any new features or changes

## Platform Compatibility

### **Core Requirements:**
- Custom instruction loading from files
- Multi-turn conversation support
- File reading and writing capabilities
- Workspace/directory context awareness
- Markdown rendering (for diagrams and documentation)

### **Currently Supported Platforms:**
- **Cursor:** `.cursorrules` loader included
- **GitHub Copilot:** `.github/copilot-instructions.md` loader included

### **Adding New Platforms:**
- Create platform-specific loader file in appropriate location
- Point loader to `.ai-instructions/core/entry-point.md`
- Test 6-stage workflow with your platform
- Submit loader as contribution if working well

---

This enhanced framework enables systematic, high-quality security research across diverse systems while maintaining consistent methodology and rigorous evidence-based quality assurance standards.

