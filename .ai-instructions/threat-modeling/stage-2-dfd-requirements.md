# DFD Multiple Format Requirements - Stage 2

## 📢 NOTICE: Documentation-Specialist Skill Available

**NEW SPECIALIZED SKILL:** The **documentation-specialist** skill is now available and is **recommended for Stage 2** data flow analysis and DFD creation.

**Why Documentation-Specialist for Stage 2:**
- ✅ Specialized in triple-format DFD creation (Text/Mermaid/Draw.io XML)
- ✅ Expert in content equivalency validation across formats
- ✅ Professional formatting and technical diagram organization
- ✅ Systematic data flow extraction from documentation
- ✅ Stage 2 is data organization work, not security analysis

**See:**
- **`.ai-instructions/skills/documentation-specialist/stage-2-guide.md`** - Primary Stage 2 guidance
- **`.ai-instructions/skills/workflow-guide.md`** - Complete Stage 2 skill loading pattern
- **`.ai-instructions/skills/README.md`** - Framework overview and getting started

**This File Provides:**
- Detailed DFD format specifications
- Triple-format requirements and validation criteria  
- Supplementary guidance referenced by documentation-specialist stage-2-guide

---

## MANDATORY DELIVERABLE FORMATS

For **Stage 2 - Data Flow Analysis**, agents MUST produce Data Flow Diagrams (DFDs) in THREE equivalent formats:

### **Format 1: Text-Based Markdown DFD** 📝
**Purpose:** Complete narrative description of all data flows
**Content Requirements:**
- Numbered list of all data flows
- Source and destination components
- Data elements for each flow
- Trust boundary identification
- Security considerations

### **Format 2: Mermaid Diagram** 📊
**Purpose:** Visual flowchart representation using Mermaid syntax
**Content Requirements:**
- All system components as nodes
- Data flows as labeled arrows
- Trust boundary grouping using subgraphs
- Valid Mermaid syntax that renders correctly

**Platform Note:** Many AI platforms can render Mermaid diagrams inline in markdown preview, allowing immediate visualization and validation.

### **Format 3: Draw.io XML Document** 🎨
**Purpose:** Import-ready professional diagram for draw.io/diagrams.net
**Content Requirements:**
- Valid XML structure for draw.io import
- Professional visual layout
- Proper shapes and connectors
- Trust boundary visual grouping
- Complete component and flow representation

## CRITICAL EQUIVALENCY REQUIREMENT

**ALL THREE FORMATS MUST CONTAIN IDENTICAL INFORMATION:**
- ✅ Same number of data flows
- ✅ Identical trust boundary definitions  
- ✅ Complete component coverage
- ✅ Consistent data element identification
- ✅ Equivalent security considerations

## VALIDATION CHECKLIST

**Critic Analysis Must Verify:**
- [ ] All data flows present in each format
- [ ] No missing components in any format
- [ ] Trust boundaries consistent across formats
- [ ] Mermaid syntax validates and renders
- [ ] Draw.io XML imports without errors
- [ ] Content equivalency maintained

## QUALITY STANDARD

**Zero tolerance for missing data flows or components in any format. Every element must be represented equivalently across all three outputs.**

---

## 🔧 PLATFORM-SPECIFIC ENHANCEMENTS (OPTIONAL)

### **Mermaid Syntax Validation**
- Use your platform's markdown preview to verify Mermaid diagrams render correctly
- Look for syntax errors in the preview
- Ensure all nodes, edges, and subgraphs display properly

### **XML Structure Validation**
- Open Draw.io XML in a text editor to verify structure
- Check for proper XML formatting and tag closure
- Validate against Draw.io XML schema if available

### **Cross-Format Consistency Check**
Use your platform's workspace search and file comparison capabilities to:
- Count data flows in each format
- Compare component names across files
- Verify trust boundary definitions match
- Ensure no missing security considerations

### **File Organization**
All three DFD files should be created simultaneously in the target's output directory:
```
[target-directory]/output/threat-model/
├── 02-data-flow-analysis.md
├── 02-data-flow-diagram.mermaid
└── 02-data-flow-diagram.drawio.xml
```

---

**REMINDER: When modifying this file, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

