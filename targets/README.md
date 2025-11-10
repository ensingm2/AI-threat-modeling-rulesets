# Threat Modeling Targets

This directory contains target systems for comprehensive threat modeling analysis using the security research framework defined in `../.ai-instructions/skills/`.

## Target Structure

Each target follows a standardized directory structure:

```
targets/
├── {target-name}/
│   ├── {target-name}-instructions.md    # Target-specific analysis guidance
│   ├── external-resources/              # Source code and documentation
│   │   └── code/                        # Source code directory
│   ├── output/                          # Generated analysis outputs
│   │   └── threat-model/               # Threat model analysis documents
│   │       ├── 01-scope-definition.md
│   │       ├── 02-architecture-dataflow.md
│   │       ├── 03-stride-analysis.md
│   │       ├── 04-killchain-attack-analysis.md
│   │       ├── 05-risk-assessment-mitigations.md
│   │       ├── 06-threat-summary.md
│   │       └── README.md
│   └── configurations/                  # Sample configurations (if applicable)
```

## Target Selection Guidance

This directory is designed to hold target systems for threat modeling analysis. Each target should be organized according to the standardized structure shown above.

### Example Target Types

The framework supports analysis of diverse system types, including but not limited to:

**Network Services & Infrastructure**
- Authentication systems, network daemons, proxies, load balancers

**Identity & Access Management**
- OAuth/SAML providers, directory services, PKI systems

**Web Applications & APIs**
- Web frameworks, REST/GraphQL APIs, microservices

**Data Storage Systems**
- Relational databases, NoSQL stores, in-memory caches, object storage

**Container & Orchestration Platforms**
- Container runtimes, orchestrators, service meshes

**IoT & Embedded Systems**
- Connected devices, firmware, communication protocols

**Cloud Services**
- Serverless functions, managed services, SaaS applications

## Analysis Framework Application

All targets are analyzed using the comprehensive security research framework that integrates:

- **STRIDE Threat Modeling** - Systematic threat categorization (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege)
- **MITRE ATT&CK Framework** - Adversarial technique mapping across attack lifecycle
- **Cyber Kill Chain** - Attack progression analysis from reconnaissance through exfiltration
- **Risk Assessment** - Dual approach using CVSS v4.0 for technical vulnerabilities and qualitative ratings for business threats (see detailed explanation below)
- **Compliance Considerations** - Alignment with industry standards (NIST, ISO 27001, PCI-DSS, GDPR, etc.)

### **Risk Scoring Approach:**

**When CVSS v4.0 IS Used:**
- **Threat Type:** Technical threats with exploitable vulnerabilities (e.g., SQL injection, authentication bypass, privilege escalation)
- **Data Requirements:** Sufficient documentation to determine all base metrics (Attack Vector, Attack Complexity, Attack Requirements, Privileges Required, User Interaction, Vulnerable/Subsequent System impacts)
- **Output:** Quantitative score (0.0-10.0) with severity rating (None/Low/Medium/High/Critical)
- **Example:** "CVSS 8.6 (High) - SQL Injection in user input validation"

**When CVSS is NOT Used:**
- **Threat Types:** 
  - Business process threats (discriminatory policies, unfair service allocation)
  - Organizational policy violations (inadequate data retention, missing incident response)
  - Regulatory compliance gaps (GDPR violations, PCI-DSS non-compliance)
  - Strategic/operational risks (insufficient training, documentation gaps)
  - Technical threats with insufficient data to determine CVSS metrics
- **Output:** Qualitative categories (CRITICAL / HIGH / MEDIUM / LOW) with explicit justification
- **Example:** "CRITICAL (Regulatory Risk) - GDPR Article 32 violation with potential 4% revenue fine"

**Hybrid Threats (Technical + Business Impact):**
- Threats combining technical exploitation WITH significant business consequences receive dual ratings
- **CVSS Score:** Applied to technical exploitation vector
- **Business Impact Rating:** Separate qualitative assessment of regulatory/financial/reputational consequences
- **Combined Priority:** Integrates both technical severity and business impact
- **Example:** "CVSS 8.6 (High) + CRITICAL Business Impact = CRITICAL Combined Priority"

**ALL threats receive risk ratings** - the methodology differs based on threat type and available data. This ensures comprehensive risk assessment regardless of whether quantitative CVSS scoring is applicable.

## Target Selection Criteria

When selecting systems for threat modeling analysis, consider:

✅ **Documentation Availability** - Comprehensive architecture documentation, API references, or source code  
✅ **Security Relevance** - Systems with significant security requirements or attack surface  
✅ **Complexity** - Sufficient architectural complexity for meaningful threat analysis  
✅ **Real-World Applicability** - Representative of actual production systems  
✅ **Analysis Value** - Findings applicable to broader security research or organizational needs

## Adding New Targets

When adding new targets to this directory:

1. **Create target directory:** `targets/{target-name}/`
2. **Add source materials:** Place documentation, code, diagrams, or specifications in `external-resources/`
3. **Include target overview:** Create a README describing the system architecture and scope
4. **(Optional) Add target-specific instructions:** Create `{target-name}-instructions.md` with any specialized analysis guidance
5. **Execute threat modeling:** Use the AI-assisted framework to generate analysis in `output/threat-model/`
6. **Review critically:** All AI-generated analysis requires expert validation before use

**Note:** Target-specific subdirectories are excluded from version control by default (`.gitignore`). This directory structure provides a consistent workspace organization for threat modeling projects.

## Usage Guidelines

- **Independent Analysis:** Each target can be analyzed using the framework in `../.ai-instructions/skills/`
- **Customization:** Target-specific instructions supplement the general methodology as needed
- **Iterative Refinement:** Threat models should be updated when systems undergo significant changes
- **Pattern Recognition:** Cross-target analysis can identify common vulnerability patterns and architectural best practices
- **Expert Validation Required:** All AI-generated outputs must be reviewed by security experts before use