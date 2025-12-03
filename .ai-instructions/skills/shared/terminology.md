# Threat Modeling Terminology | Load: All Stages

**Purpose:** Core architectural and data quality concepts for all stages

**Framework-specific terms:** See `../threat-modeler/references/frameworks/quick-reference.md`  
**Risk assessment details:** See `../threat-modeler/references/stage-4-risk-assessment.md`  
**Methodology details:** See `../quality-critic/references/core-principles.md`

---

## 1. Architectural Concepts

### **Component**
A distinct architectural element with defined boundaries and responsibilities (web server, database, auth service, API, etc.)

**Major Component Criteria:**
- Count: Application servers, databases, auth services, external APIs, message queues, load balancers
- Don't count: Caches, CDNs, monitoring infrastructure, container orchestration platforms
- Judgment: Microservices (count if loosely coupled), multiple DBs (count if different purposes)

### **Trust Boundary**
A line separating different levels of trust/privilege. Crossing requires authentication, authorization, or validation.

### **Attack Surface**
All points where unauthorized users could enter/extract data (APIs, user inputs, file uploads, network interfaces).

### **Data Flow**
Movement of data between components. Characterized by: source, destination, data elements, protocol, boundaries crossed.

### **External Entity**
Person, system, or organization outside system boundary that interacts with the system.

---

## 2. Data Quality Concepts

### **Confidence Level**
| Level | Range | Criteria |
|-------|-------|----------|
| **HIGH** | 85-95% | Direct source documentation with quotes |
| **MEDIUM** | 70-<85% | Reasonable inference with documented assumptions |
| **LOW** | 50-<70% | Industry patterns with explicit limitations |
| **INSUFFICIENT** | <50% | Inadequate data; use qualitative approach |

**Details:** See `confidence-calibration.md`

### **Source Traceability**
Ability to track claims to source documentation. Requires: direct quote, document reference, confidence level.

### **Assumption**
Supposition about system characteristics not explicitly documented. Mark with ⚠️ ASSUMPTION + confidence level + impact if wrong.

### **Data Gap**
Missing information for complete analysis. Document: what's missing, impact on analysis, how to obtain.

---

## 3. Quick Reference Tables

### **Risk Ratings** (Details: `../threat-modeler/references/stage-4-risk-assessment.md`)
| Rating | Criteria |
|--------|----------|
| **CRITICAL** | Immediate business impact; regulatory violations; complete compromise |
| **HIGH** | Significant impact; major data exposure; service disruption |
| **MEDIUM** | Moderate impact; limited scope; standard remediation |
| **LOW** | Minor impact; unlikely exploitation; acceptable residual risk |

### **STRIDE Categories** (Details: `../threat-modeler/references/frameworks/quick-reference.md`)
| Category | Property Violated |
|----------|-------------------|
| **S**poofing | Authentication |
| **T**ampering | Integrity |
| **R**epudiation | Non-repudiation |
| **I**nfo Disclosure | Confidentiality |
| **D**enial of Service | Availability |
| **E**levation of Privilege | Authorization |

### **Control Types**
| Type | Purpose |
|------|---------|
| **Preventive** | Blocks before occurrence (input validation, encryption) |
| **Detective** | Identifies during occurrence (logging, IDS) |
| **Corrective** | Responds after occurrence (incident response, backups) |

