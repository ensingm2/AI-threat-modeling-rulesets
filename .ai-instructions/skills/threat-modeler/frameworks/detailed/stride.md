# STRIDE Framework Reference

**Framework:** STRIDE Threat Categorization  
**Purpose:** Systematic threat identification by security property violated  
**Application:** Stage 3 - Threat Identification

---

## STRIDE Overview

**STRIDE** is a mnemonic for six threat categories, each representing a violation of a desired security property:

- **S** - Spoofing (Identity)
- **T** - Tampering (with Data)
- **R** - Repudiation (Actions)
- **I** - Information Disclosure
- **D** - Denial of Service
- **E** - Elevation of Privilege

## Mandatory Application Requirements

### **ALL Six Categories Per Component**

Each system component MUST be analyzed for ALL six STRIDE categories. Do not skip categories even if threats seem unlikely - systematic coverage is required.

### **Per-Component Application**

Apply STRIDE to each major component identified in Stage 1:
- User-facing interfaces (web, mobile, API)
- Backend services and APIs
- Databases and data stores
- Authentication/authorization services
- Third-party integrations
- IoT devices or embedded systems
- Infrastructure components

## STRIDE Category Definitions

### **S - Spoofing Identity**

**Security Property Violated:** Authentication  
**Definition:** Pretending to be something or someone other than yourself

**Common Threat Examples:**
- User identity spoofing (credential theft, session hijacking)
- Device identity spoofing (MAC address spoofing, IMEI cloning)
- Service identity spoofing (man-in-the-middle, DNS spoofing)
- API endpoint spoofing (fake services intercepting requests)
- Email/communication spoofing (phishing, sender impersonation)

**Application Questions:**
- Can an attacker impersonate a legitimate user?
- Can devices be cloned or their identity forged?
- Can services be impersonated to intercept communications?
- Are authentication mechanisms vulnerable to bypass?
- Can API clients be spoofed?

**Generic Threats (Implementation-Agnostic):**
- Weak password policies enabling credential guessing
- Session token prediction or theft
- Lack of mutual authentication in service-to-service communication
- Missing certificate validation in TLS connections
- Insufficient device attestation mechanisms

**Mitigation Categories:**
- Strong multi-factor authentication
- Certificate pinning and mutual TLS
- Cryptographic identity verification
- Device attestation and hardware-backed keys
- Session management security controls

---

### **T - Tampering with Data**

**Security Property Violated:** Integrity  
**Definition:** Malicious modification of data or code

**Common Threat Examples:**
- Data tampering in transit (man-in-the-middle modification)
- Data tampering at rest (database manipulation, file modification)
- Code tampering (binary patching, malicious code injection)
- Configuration tampering (unauthorized settings modification)
- Log tampering (audit trail manipulation)

**Application Questions:**
- Can data be modified in transit between components?
- Can stored data be altered without detection?
- Can application binaries be modified and redistributed?
- Can configuration files be tampered with?
- Can audit logs be modified or deleted?

**Generic Threats (Implementation-Agnostic):**
- Unencrypted communications enabling man-in-the-middle attacks
- Lack of input validation allowing injection attacks
- Missing integrity checks on stored data
- Insufficient access controls on configuration files
- No tamper-evident logging mechanisms
- Client-side data storage without integrity protection

**Mitigation Categories:**
- Encryption in transit (TLS/HTTPS)
- Digital signatures and message authentication codes
- Input validation and parameterized queries
- File integrity monitoring
- Immutable audit logging
- Database transaction controls

---

### **R - Repudiation**

**Security Property Violated:** Non-Repudiation  
**Definition:** Claiming not to have performed an action or denying responsibility

**Common Threat Examples:**
- Transaction repudiation (denying purchase or transaction)
- Action repudiation (denying administrative actions)
- Communication repudiation (denying sent messages)
- Data access repudiation (denying viewing sensitive data)
- Configuration change repudiation (denying system modifications)

**Application Questions:**
- Can users deny performing transactions?
- Are all security-relevant actions logged with attribution?
- Can administrators deny making configuration changes?
- Are audit logs tamper-evident and securely stored?
- Can data access be proven and attributed to specific users?

**Generic Threats (Implementation-Agnostic):**
- Insufficient audit logging of security-relevant events
- Missing user attribution in log entries
- Lack of transaction signing or confirmation mechanisms
- Inadequate log retention policies
- Missing timestamps or non-synchronized clocks
- No integrity protection for audit logs

**Mitigation Categories:**
- Comprehensive audit logging
- Cryptographic log signing
- Secure timestamp services
- Transaction confirmation mechanisms
- Non-repudiation protocols (digital signatures)
- Tamper-evident log storage

---

### **I - Information Disclosure**

**Security Property Violated:** Confidentiality  
**Definition:** Exposure of information to unauthorized individuals

**Common Threat Examples:**
- Database exposure (SQL injection, exposed databases)
- API data leaks (excessive data in responses, broken access control)
- Client-side data exposure (localStorage, cookies, caching)
- Network traffic exposure (unencrypted communications)
- Error message information leakage
- Backup and log file exposure
- Memory dump information disclosure

**Application Questions:**
- Can sensitive data be accessed without authorization?
- Is data encrypted in transit and at rest?
- Do error messages reveal system internals?
- Can API responses be manipulated to expose additional data?
- Are backups and logs protected from unauthorized access?
- Does client-side storage contain sensitive information?

**Generic Threats (Implementation-Agnostic):**
- Unencrypted data transmission exposing sensitive information
- Insecure direct object references (IDOR) in APIs
- Excessive data exposure in API responses
- Sensitive data in client-side storage
- Information leakage through error messages
- Unprotected log files containing PII
- Missing access controls on storage buckets
- Side-channel information disclosure

**Mitigation Categories:**
- Encryption at rest and in transit
- Principle of least privilege in data access
- API response filtering and data minimization
- Secure error handling without information leakage
- Access controls on logs and backups
- Data loss prevention controls
- Secure data disposal and retention

---

### **D - Denial of Service**

**Security Property Violated:** Availability  
**Definition:** Denying or degrading service to legitimate users

**Common Threat Examples:**
- Resource exhaustion (CPU, memory, disk, network)
- Application crashes through malformed input
- Database connection pool exhaustion
- Network flooding (DDoS attacks)
- Algorithmic complexity attacks
- Storage exhaustion attacks
- Rate limiting bypass attacks

**Application Questions:**
- Can attackers exhaust system resources?
- Are there rate limits on API endpoints and user actions?
- Can malformed input cause crashes or hangs?
- Are there protections against amplification attacks?
- Can storage be filled to cause service disruption?
- Are database queries protected against performance degradation?

**Generic Threats (Implementation-Agnostic):**
- Missing rate limiting enabling resource exhaustion
- Unvalidated input causing application crashes
- Unbounded database queries causing performance degradation
- Missing timeout mechanisms allowing resource holding
- Lack of resource quotas per user/tenant
- No protection against amplification attacks
- Missing circuit breakers for external dependencies
- Algorithmic complexity vulnerabilities (ReDoS, hash collision)

**Mitigation Categories:**
- Rate limiting and throttling
- Input validation and sanitization
- Resource quotas and limits
- Timeout mechanisms
- DDoS protection services
- Circuit breakers and graceful degradation
- Query optimization and limits
- Monitoring and alerting

---

### **E - Elevation of Privilege**

**Security Property Violated:** Authorization  
**Definition:** Gaining capabilities without proper authorization

**Common Threat Examples:**
- Authentication bypass (gaining access without credentials)
- Authorization bypass (accessing resources beyond permissions)
- Privilege escalation (user to admin, user to root)
- Role manipulation (modifying assigned roles)
- API authorization flaws (accessing other users' data)
- Container escape (breaking out of sandboxed environment)
- SQL injection leading to database admin access

**Application Questions:**
- Can users access functionality beyond their role?
- Can authentication be bypassed entirely?
- Can users modify their own permissions?
- Are API endpoints properly protected with authorization checks?
- Can administrative interfaces be accessed by non-admins?
- Are privilege boundaries properly enforced?

**Generic Threats (Implementation-Agnostic):**
- Missing authorization checks on API endpoints
- Insecure direct object references allowing access to others' data
- Privilege escalation through parameter manipulation
- Role-based access control (RBAC) bypass vulnerabilities
- Horizontal privilege escalation (user A accessing user B's data)
- Vertical privilege escalation (user gaining admin privileges)
- Token manipulation to gain elevated access
- Injection attacks enabling privilege escalation

**Mitigation Categories:**
- Robust authentication mechanisms
- Comprehensive authorization checks
- Principle of least privilege
- Role-based or attribute-based access control
- Input validation and parameterization
- Secure session management
- Regular privilege reviews
- Secure API design with authorization enforcement

---

## Application Methodology

### **Per-Component Analysis Pattern:**

```markdown
## Component: [Component Name]

### S - Spoofing Threats
#### T-XXX: [Specific Spoofing Threat]
[Threat details, attack scenario, impact]

### T - Tampering Threats
#### T-XXX: [Specific Tampering Threat]
[Threat details, attack scenario, impact]

### R - Repudiation Threats
#### T-XXX: [Specific Repudiation Threat]
[Threat details, attack scenario, impact]

### I - Information Disclosure Threats
#### T-XXX: [Specific Information Disclosure Threat]
[Threat details, attack scenario, impact]

### D - Denial of Service Threats
#### T-XXX: [Specific DoS Threat]
[Threat details, attack scenario, impact]

### E - Elevation of Privilege Threats
#### T-XXX: [Specific Privilege Escalation Threat]
[Threat details, attack scenario, impact]
```

### **Generic vs. Specific Threats:**

**Generic Threats (60-70% of threats):**
- Implementation-agnostic
- Applicable across technology stacks
- Based on common vulnerability patterns
- Example: "API authentication bypass through missing authorization checks"

**Specific Threats (20-30% of threats):**
- Based on documented system characteristics
- Technology or architecture-specific
- Example: "GPS spoofing in documented IoT bike lock location tracking"

**Operational Threats (10-20% of threats):**
- Business process and policy related
- May not fit cleanly into STRIDE categories
- Example: "Discriminatory bike allocation policies"

## STRIDE to Mitigation Mapping

| STRIDE Category | Mitigation Focus | Common Controls |
|-----------------|------------------|-----------------|
| **Spoofing** | Authentication | MFA, certificates, cryptographic identity |
| **Tampering** | Integrity | Encryption, signatures, input validation |
| **Repudiation** | Non-repudiation | Audit logging, digital signatures |
| **Information Disclosure** | Confidentiality | Encryption, access controls, data minimization |
| **Denial of Service** | Availability | Rate limiting, input validation, resource quotas |
| **Elevation of Privilege** | Authorization | RBAC, least privilege, authorization checks |

## Quality Validation

**Critic Must Verify:**
- ALL six STRIDE categories applied to each component
- Both generic and system-specific threats identified
- Threat descriptions include attack scenarios
- No category skipped with justification if truly no applicable threats
- Systematic coverage rather than ad-hoc threat identification

---

**REMINDER: When modifying this framework guidance, ensure equivalent changes are made to ALL supported AI platform instruction sets to maintain cross-system ruleset consistency.**

