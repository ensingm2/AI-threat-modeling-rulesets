# Core Terminology | Load: Stages 1-2, All Stages

**Scope:** Core architectural, data quality, and methodology concepts

---

## Core Architectural Concepts

### **Component (System Architecture)**
- **Definition:** A distinct architectural element with defined boundaries and responsibilities
- **Examples:** web server, database server, authentication service, message queue, external API, cache, file storage
- **Major Component:** Primary system elements that interact across trust boundaries or handle different data classification levels

### **Major Component Counting Criteria**

**Count as Major Component:**
- Application servers/services handling business logic
- Databases and primary data stores (relational, NoSQL, data warehouses)
- Authentication and authorization services
- External-facing APIs or API gateways
- Third-party services with which the system integrates (payment processors, cloud providers, external APIs)
- Message queues or event brokers handling inter-service communication
- Load balancers or reverse proxies serving as system entry points

**Generally DO NOT Count as Separate Major Components:**
- Caches (Redis, Memcached) supporting primary data stores - consider part of database component
- CDNs distributing static content - consider part of web server component
- Individual microservices within a tightly-coupled service mesh - count the service mesh as one component or group related microservices
- Monitoring/logging infrastructure (unless it's the system being analyzed)
- Container orchestration platforms (Kubernetes, Docker) - count orchestrated applications, not the platform itself

**Judgment Call - Context Dependent:**
- **Microservices:** If loosely coupled with independent data stores and trust boundaries, count separately. If tightly coupled sharing databases, count as single component or small group
- **Multiple Databases:** If serving different purposes with different access patterns (e.g., transactional DB + analytics DB), count separately. If read replicas of same DB, count as one
- **File Storage:** Object storage (S3, blob storage) counts as separate component if primary data repository; doesn't count if just storing application logs

**Rule of Thumb:** Focus on architectural elements that would require separate security analysis for STRIDE categories

### **Trust Boundary**
- **Definition:** A line separating different levels of trust or privilege in a system
- **Examples:** network perimeter, process boundaries, user/admin privilege separation, internal/external system interfaces
- **Security Implication:** Crossing trust boundaries typically requires authentication, authorization, or data validation

### **Attack Surface**
- **Definition:** The sum of all points where an unauthorized user could attempt to enter data or extract data from a system
- **Includes:** network interfaces, APIs, user inputs, file uploads, inter-process communications
- **Risk Correlation:** Larger attack surface generally indicates more potential vulnerabilities

### **Data Flow**
- **Definition:** Movement of data between components, processes, or external entities
- **Characterized By:** source, destination, data elements, protocol/mechanism, trust boundaries crossed
- **Usage:** Used in Data Flow Diagrams (DFDs) to visualize system interactions

### **External Entity (DFD)**
- **Definition:** A person, system, or organization outside the system boundary that interacts with the system
- **Examples:** end users, third-party services, external APIs, partner organizations
- **DFD Representation:** Typically represented as rectangles in Data Flow Diagrams

---

## Data Quality Concepts

### **Source Traceability**
- **Definition:** The ability to track a claim or assertion back to its original source documentation
- **Requirements:** Direct quote, document reference (file, section, line), confidence level
- **Purpose:** Prevents fabrication and enables validation of analytical claims

### **Assumption**
- **Definition:** A supposition or hypothesis about system characteristics not explicitly documented
- **Documentation:** Must be clearly marked (⚠️ ASSUMPTION) with confidence level and potential impact
- **Types:**
  - **Reasonable Inference:** Logical conclusion based on partial documentation
  - **Industry Standard:** Common practice assumption when specifics unavailable
  - **Critical Assumption:** Assumption that, if incorrect, could invalidate major findings

### **Data Gap**
- **Definition:** Missing information required for complete analysis
- **Documentation:** Must be explicitly identified with impact on analysis and recommendations for obtaining missing data
- **Handling:** Use qualitative assessment, document limitations, avoid fabrication

---

## Methodology Concepts

### **Graduated Approval**
- **Definition:** Quality assessment system with multiple approval levels based on demonstrated analytical competence
- **Levels:**
  - **Confident Approval:** ≥90% quality confidence, immediate progression
  - **Conditional Approval:** 70-89% quality confidence, minor guidance then progression
  - **Targeted Revision:** 40-69% quality confidence, focused rework on specific areas
  - **Major Rework:** <40% quality confidence, complete stage restart

### **Adversarial Validation**
- **Definition:** Quality assurance approach where critic actively seeks flaws rather than confirming work
- **Purpose:** Prevents rubber-stamping and ensures rigorous quality standards
- **Requirements:** Separate critic agent, mandatory problem-seeking, minimum issue identification standards

### **Evidence-Based Analysis**
- **Definition:** Analytical approach grounding all claims in documented evidence with appropriate uncertainty acknowledgment
- **Requirements:** Source traceability, assumption documentation, confidence calibration, data gap acknowledgment
- **Prohibition:** Fabrication of technical details, business metrics, or system characteristics

---

## Usage Guidelines

**When to Reference:**
- During system architecture analysis (Stages 1-2)
- When documenting trust boundaries and attack surfaces
- Throughout quality validation for terminology alignment

**Consistency Requirements:**
- All skills must use these definitions consistently
- Any deviation must be explicitly justified
- Cross-stage terminology must remain stable

---

**For threat modeling and risk assessment terms, see:** `threat-modeling-terms.md`, `risk-assessment-terms.md`

