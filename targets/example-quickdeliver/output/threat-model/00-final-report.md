# Threat Model Report: QuickDeliver
**Date:** 2025-12-03 | **Mode:** Automatic

---

## Executive Summary

QuickDeliver is an on-demand food and item delivery platform connecting customers, delivery drivers, and merchants. This threat model identifies security risks across the platform's mobile applications, backend services, payment processing, and third-party integrations.

### Key Findings

| Metric | Value |
|--------|-------|
| **Total Threats Identified** | 30 |
| **Components Analyzed** | 21 |
| **Trust Boundaries** | 8 |
| **Data Flows Mapped** | 45+ |

**Threat Distribution:**
- **CRITICAL:** 5 threats requiring immediate action
- **HIGH:** 12 threats requiring near-term remediation  
- **MEDIUM:** 11 threats for planned improvement
- **LOW:** 2 threats to monitor

**Primary Risk Areas:**
1. Authentication and Session Management
2. Payment Processing Integrity
3. API Authorization (BOLA/IDOR vulnerabilities)
4. Administrative Access Controls
5. Third-Party Webhook Security

**Overall Risk Posture:** HIGH - The platform handles sensitive data (PII, payment information, real-time location) with significant attack surface exposure. While the architecture follows modern patterns, several security controls require verification or implementation.

### Critical Concerns

| # | Concern | Business Impact |
|---|---------|-----------------|
| 1 | **JWT Token Security** | Full platform compromise possible if tokens can be forged |
| 2 | **Payment Manipulation** | Direct financial losses through price/amount tampering |
| 3 | **Admin API Exposure** | Complete data breach risk from compromised admin account |
| 4 | **API Authorization Gaps** | Cross-user data access enabling privacy violations |
| 5 | **Webhook Spoofing** | Fraudulent transactions if signatures not verified |

### Priority Recommendations

**Immediate (CRITICAL):**
- Implement rate limiting on authentication endpoints
- Enforce strict JWT algorithm validation (RS256 only)
- Verify Stripe/Checkr webhook signatures
- Add server-side price validation for all orders

**Short-Term (HIGH):**
- Implement object-level authorization across all APIs
- Add role enforcement middleware
- Deploy input validation and parameterized queries
- Secure file upload handling for documents/images

**Strategic (MEDIUM/LOW):**
- Deploy fraud detection system for chargebacks
- Implement GPS anomaly detection for drivers
- Add immutable audit logging
- Enhance phone verification with TOTP option

### Limitations

- Security implementation details (rate limiting, input validation) not documented; analysis assumes industry-standard gaps
- Internal service communication security not fully documented
- Encryption at rest configuration unknown
- Logging and monitoring capabilities not documented

---

## 1. System Overview

### Business Purpose

QuickDeliver is an on-demand delivery platform competing with DoorDash, Uber Eats, and Grubhub in the food delivery market. The platform differentiates through lower merchant commission rates (15% vs industry 20-30%) and higher driver earnings retention (85% of delivery fees).

The platform connects three user populations: customers ordering food/items, drivers performing deliveries, and merchants providing products. Revenue comes from delivery fees ($3-7/order), merchant commissions, subscription service ($10/month), and advertising.

Security is critical due to:
- Payment card processing requiring PCI-DSS awareness
- Personal information handling under GDPR requirements
- Real-time location tracking raising privacy concerns
- Financial transactions across all three user types

### Primary Users

| User Type | Role | Access Level | Security Relevance |
|-----------|------|--------------|-------------------|
| **Customer** | Orders food/items, tracks delivery, makes payments | Own profile, orders, addresses, payment methods | PII and payment data owner; primary fraud target |
| **Driver** | Accepts deliveries, navigates, receives payouts | Own profile, assigned orders, earnings, GPS broadcast | Location tracking, financial access, document uploads |
| **Merchant** | Receives orders, manages menu, receives payouts | Own restaurant, menu, orders, analytics, payouts | Business data, financial transactions |
| **Admin** | Platform management, user approvals, support | All users, orders, refunds, promos | Privileged access to all data; highest-risk role |

### Key Functionality

- Browse merchants and place orders with customizations
- Real-time GPS tracking of deliveries via WebSocket
- Payment processing through Stripe (cards, Apple Pay, Google Pay)
- Driver and merchant onboarding with background checks (Checkr)
- Subscription service for unlimited free delivery
- Instant payout capability for drivers ($0.50 fee)
- In-app communication between customers and drivers

---

## 2. Architecture Summary

> *For detailed component definitions (C-XXX) and trust boundary specifications (TB-XXX), refer to `01-system-understanding.md`. For data flow details (DF-XXX) and attack surface analysis (AS-XXX), refer to `02-data-flow-analysis.md`.*

### System Components Overview

| Component | Type | Function | Security Criticality |
|-----------|------|----------|---------------------|
| Customer Mobile App | Mobile (React Native) | Order placement, tracking, payments | HIGH - Handles payment tokens |
| Driver Mobile App | Mobile (React Native) | Delivery management, GPS broadcast | HIGH - Location and earnings |
| Merchant Portal | Web (React) | Menu/order management | MEDIUM - Business data |
| Admin Portal | Web (React) | Platform administration | CRITICAL - Full data access |
| API Gateway | Infrastructure (AWS ALB) | Request routing | HIGH - All traffic passes through |
| User Service | Backend (Node.js) | Authentication, profiles | CRITICAL - Credential handling |
| Order Service | Backend (Node.js) | Order lifecycle | HIGH - Payment integration |
| Driver Service | Backend (Node.js) | Driver management, assignment | MEDIUM - Location handling |
| Merchant Service | Backend (Node.js) | Restaurant profiles, menus | MEDIUM - Business data |
| Payment Service | Backend (Node.js) | Stripe integration | CRITICAL - Financial transactions |
| Tracking Service | Backend (Node.js) | WebSocket real-time location | MEDIUM - Privacy sensitive |
| PostgreSQL | Database (AWS RDS) | Primary data store | CRITICAL - All persistent data |
| Redis | Cache (ElastiCache) | Sessions, location cache | HIGH - Session tokens |
| S3 | Storage (AWS) | Files, documents, images | HIGH - Sensitive documents |

### Trust Boundaries

**8 trust boundaries identified:**

1. **TB-01 Internet/VPC** - Public internet to AWS infrastructure (primary perimeter)
2. **TB-02 Client/API** - Mobile/web apps to backend services (application auth)
3. **TB-03 API/Database** - Backend services to data stores (data tier)
4. **TB-04 VPC/External** - AWS to third-party APIs (Stripe, Twilio, etc.)
5. **TB-05 Customer/Driver** - Role privilege boundary
6. **TB-06 User/Merchant** - Role privilege boundary
7. **TB-07 User/Admin** - Administrative privilege boundary
8. **TB-08 WebSocket** - Real-time tracking channel

### Data Flow Architecture

The platform follows a standard 3-tier architecture:

**Authentication Flow:** Users authenticate via email/password or OAuth (Google/Apple/Facebook). JWT tokens (15-minute expiry, 7-day refresh) are issued and required for all API calls.

**Order Flow:** Customer browses merchants → adds items to cart → submits order with payment method → Stripe authorizes payment → order assigned to driver → real-time tracking via WebSocket → delivery confirmed → payment captured and split.

**Real-Time Tracking:** Driver apps send GPS coordinates every 5 seconds via WebSocket → Tracking service stores in Redis → broadcasts to customer app → calculates ETA via Google Maps.

### Attack Surfaces

| Entry Point | Type | Auth Required | Risk Level |
|-------------|------|---------------|------------|
| AS-01 Auth API | REST | No (login/register) | HIGH |
| AS-02 Customer API | REST | Yes (JWT) | MEDIUM |
| AS-03 Driver API | REST | Yes (JWT + role) | MEDIUM |
| AS-04 Merchant API | REST | Yes (JWT + role) | MEDIUM |
| AS-05 Admin API | REST | Yes (JWT + admin) | CRITICAL |
| AS-06 WebSocket | WSS | Yes (token) | MEDIUM |
| AS-07 S3 Uploads | File | Yes (signed URL) | HIGH |
| AS-08 Stripe Webhooks | Webhook | Signature | HIGH |
| AS-09 Checkr Webhooks | Webhook | Signature | MEDIUM |

### External Dependencies

| Service | Purpose | Data Shared | Risk |
|---------|---------|-------------|------|
| Stripe | Payments | Payment tokens, amounts | HIGH |
| Twilio | SMS/Voice | Phone numbers, messages | MEDIUM |
| Google Maps | Routing | Addresses, locations | MEDIUM |
| Firebase | Push notifications | Device tokens | LOW |
| Checkr | Background checks | Driver documents, SSN | HIGH |

---

## 3. Assumptions

> *For detailed assumption rationale and impact analysis, refer to `01-system-understanding.md`.*

| # | Assumption | Basis | Confidence | Impact if Wrong |
|---|------------|-------|------------|-----------------|
| 1 | JWT tokens validated on every API request | Industry standard; JWT mentioned in docs | MEDIUM | Unauthenticated access possible |
| 2 | Stripe handles all raw card data | Only stripe_payment_method_id stored | HIGH | PCI scope expansion |
| 3 | HTTPS enforced for all API communications | Best practice for payment apps | MEDIUM | Credentials exposed in transit |
| 4 | Password hashing uses modern algorithm | password_hash field in users table | MEDIUM | Easier credential compromise |
| 5 | Rate limiting exists on auth endpoints | Common defense; not documented | LOW | Brute force attacks feasible |
| 6 | Driver document uploads validated | Documents required for onboarding | MEDIUM | Malicious file uploads possible |
| 7 | Role-based access enforced at API level | Role field in users table | MEDIUM | Privilege escalation possible |
| 8 | WebSocket connections require auth tokens | Real-time tracking security | MEDIUM | Unauthorized location access |

---

## 4. Threat Inventory (Priority-Sorted)

> *For detailed threat descriptions, attack scenarios, and affected components for any threat (T-XXX), refer to `03-threat-identification.md`. For risk rating justifications, refer to `04-risk-assessment.md`.*

### Threat Summary

| Priority | Count | Percentage |
|----------|-------|------------|
| CRITICAL | 5 | 17% |
| HIGH | 12 | 40% |
| MEDIUM | 11 | 37% |
| LOW | 2 | 6% |
| **Total** | **30** | 100% |

**Verification:** Stage 3 Threat Count: 30 | Stage 6 Report Count: 30 | ✓ MATCH

### CRITICAL Priority Threats

| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
| T-003 | JWT Token Manipulation | API Gateway | Full platform compromise | M-002: JWT Security Hardening |
| T-008 | Payment Amount Tampering | Payment Service | Direct financial loss | M-004: Server-Side Price Validation |
| T-016 | Payment Token Leakage | Payment Service | PCI violation, fraud | Logging hygiene, error handling |
| T-018 | Admin API Mass Data Extraction | Admin Portal | Complete data breach | M-011: Admin Access Controls |
| T-024 | Privilege Escalation to Admin | Admin Portal | Complete system takeover | M-006: Role Enforcement Middleware |

#### T-003: JWT Token Manipulation
**Risk:** CRITICAL | **STRIDE:** Spoofing, Elevation of Privilege

JWT is the sole authentication mechanism for all API access. If JWT secret is weak, leaked, or algorithm confusion is possible (none/alg switching), attackers can forge tokens with arbitrary claims including admin role.

**Business Impact:** Attacker with forged admin token has unrestricted platform access - can extract all user data, issue refunds, suspend accounts, and manipulate financial transactions.

**Mitigation:** Enforce RS256 algorithm explicitly, use strong 2048-bit+ keys with quarterly rotation, validate all claims, implement token revocation.

#### T-008: Payment Amount Tampering
**Risk:** CRITICAL | **STRIDE:** Tampering

If payment intents are created with client-supplied amounts or if race conditions exist between order creation and payment capture, attackers can manipulate payment amounts.

**Business Impact:** Direct financial losses through reduced payments for orders or inflated driver/merchant payouts. Platform revenue directly impacted.

**Mitigation:** Recalculate all order totals server-side from menu prices. Never trust client-submitted totals. Use database transactions and idempotency keys.

#### T-016: Payment Token Leakage
**Risk:** CRITICAL | **STRIDE:** Information Disclosure

Stripe payment_method_ids could be leaked through verbose error messages, API responses, or debug logs. Combined with other data, could enable unauthorized charges.

**Business Impact:** PCI-DSS compliance violation, potential for unauthorized charges, regulatory penalties, customer trust damage.

**Mitigation:** Sanitize error responses, implement structured logging without sensitive data, regular log audits.

#### T-018: Admin API Mass Data Extraction
**Risk:** CRITICAL | **STRIDE:** Information Disclosure

Compromised admin account has access to all users, orders, and financial data via `/admin/*` endpoints. No documented rate limiting or data export controls.

**Business Impact:** Complete platform data breach affecting all users. GDPR penalties, notification requirements, reputational damage.

**Mitigation:** Require MFA for admin accounts, implement admin action rate limiting, log all admin API access, add data export limits.

#### T-024: Privilege Escalation to Admin
**Risk:** CRITICAL | **STRIDE:** Elevation of Privilege

Weak admin role assignment, JWT claim modification, or API authorization flaws could allow regular users to access admin functionality.

**Business Impact:** Unauthorized user gaining admin access has full platform control including ability to suspend users, issue refunds, and access all data.

**Mitigation:** Create role-checking middleware, define permissions matrix in configuration, enforce role checks on all role-specific endpoints.

### HIGH Priority Threats

| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
| T-001 | Credential Stuffing Attack | User Service | Account takeovers | M-001: Rate Limiting |
| T-002 | OAuth Token Hijacking | User Service | Account takeovers | M-010: OAuth Flow Hardening |
| T-004 | Session Fixation/Hijacking | Redis | Account takeovers | M-009: Session Security |
| T-006 | Order Price Manipulation | Order Service | Revenue loss | M-004: Server-Side Validation |
| T-012 | Payment Chargeback Fraud | Stripe | Financial loss | M-012: Fraud Detection |
| T-014 | User PII Exposure via IDOR | User Service | GDPR violations | M-005: Object-Level Auth |
| T-019 | Auth Endpoint Brute Force | User Service | Service degradation | M-001: Rate Limiting |
| T-023 | BOLA - Cross-User Data Access | All Services | Data breaches | M-005: Object-Level Auth |
| T-025 | Role Boundary Bypass | User Service | Unauthorized access | M-006: Role Enforcement |
| T-026 | Stripe Webhook Spoofing | Payment Service | Financial fraud | M-003: Webhook Signatures |
| T-028 | Malicious File Upload (RCE) | S3 | System compromise | M-008: Secure Upload Handler |
| T-029 | SQL Injection | PostgreSQL | Database compromise | M-007: Input Validation |

### MEDIUM Priority Threats

| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
| T-005 | Phone Number Spoofing | Twilio | Account takeover | M-017: Phone Verification Hardening |
| T-007 | Driver GPS Location Spoofing | Tracking Service | Fraud, poor service | M-013: GPS Anomaly Detection |
| T-009 | Menu Price Injection | Merchant Service | Customer overcharge | M-004: Server-Side Validation |
| T-011 | Delivery Non-Receipt Disputes | Order Service | Refund fraud | M-012: Fraud Detection |
| T-013 | Driver Activity Log Tampering | Driver Service | Audit failures | M-014: Immutable Audit Logging |
| T-015 | Driver Location Privacy Breach | Tracking Service | Privacy violations | M-015: WebSocket Rate Limiting |
| T-017 | Merchant Sales Data Exposure | Merchant Service | Business intel theft | M-005: Object-Level Auth |
| T-020 | WebSocket Connection Exhaustion | Tracking Service | Tracking unavailable | M-015: WebSocket Rate Limiting |
| T-021 | Order Processing Flood | Order Service | Service disruption | M-001: Rate Limiting |
| T-027 | Checkr Webhook Forgery | Driver Service | Unsafe driver approval | M-003: Webhook Signatures |
| T-030 | Stored XSS in User Content | Merchant Portal | Session theft | M-007: Input Validation, M-016: CSP |

### LOW Priority Threats

| ID | Threat | Component | Impact | Mitigation |
|----|--------|-----------|--------|------------|
| T-010 | Review/Rating Manipulation | PostgreSQL | Reputation gaming | M-018: Review Anti-Gaming |
| T-022 | Driver Assignment Queue Saturation | Driver Service | Minor disruption | Monitoring |

### Threat Coverage by STRIDE Category

| STRIDE Category | Total | CRITICAL | HIGH | MEDIUM | LOW |
|-----------------|-------|----------|------|--------|-----|
| Spoofing | 5 | 1 | 3 | 1 | 0 |
| Tampering | 5 | 1 | 2 | 2 | 0 |
| Repudiation | 3 | 0 | 1 | 2 | 0 |
| Information Disclosure | 5 | 2 | 2 | 1 | 0 |
| Denial of Service | 4 | 0 | 1 | 2 | 1 |
| Elevation of Privilege | 8 | 1 | 3 | 3 | 1 |
| **Total** | **30** | **5** | **12** | **11** | **2** |

---

## 5. Implementation Roadmap

> *For detailed implementation steps, success criteria, and control specifications, refer to `05-mitigation-strategy.md`. For risk rating justifications, refer to `04-risk-assessment.md`.*

### Roadmap Overview

| Phase | Priority | Controls | Threats Addressed |
|-------|----------|----------|-------------------|
| Phase 0 | CRITICAL | 4 | 9 |
| Phase 1 | HIGH | 7 | 15 |
| Phase 2 | MEDIUM | 5 | 10 |
| Phase 3 | LOW | 2 | 2 |
| **Total** | - | **18** | **30** (100%) |

### Phase 0: Immediate Actions

| Control | Threats | Effort | Expected Outcome |
|---------|---------|--------|------------------|
| M-001 Rate Limiting | T-001, T-019, T-021 | LOW | Block brute force attacks |
| M-002 JWT Security Hardening | T-003, T-024 | LOW | Prevent token forgery |
| M-003 Webhook Signature Verification | T-026, T-027 | LOW | Block fraudulent webhooks |
| M-004 Server-Side Price Validation | T-006, T-008, T-009 | MEDIUM | Eliminate price manipulation |

**Phase 0 Quick Wins:**
- Rate limiting requires only Redis configuration (already in stack)
- JWT algorithm lock is a single configuration line
- Stripe/Checkr provide signature verification libraries

### Phase 1: Short-Term Improvements

| Control | Threats | Effort | Expected Outcome |
|---------|---------|--------|------------------|
| M-005 Object-Level Authorization | T-014, T-023 | MEDIUM | Block cross-user access |
| M-006 Role Enforcement Middleware | T-024, T-025 | MEDIUM | Enforce role boundaries |
| M-007 Input Validation | T-029, T-030 | MEDIUM | Prevent injection attacks |
| M-008 Secure File Upload Handler | T-028 | MEDIUM | Block malicious uploads |
| M-009 Session Security Enhancement | T-004 | MEDIUM | Protect session tokens |
| M-010 OAuth Flow Hardening | T-002 | MEDIUM | Secure OAuth implementation |
| M-011 Admin Access Controls | T-018 | MEDIUM | Protect admin functions |

### Phase 2: Medium-Term Improvements

| Control | Threats | Effort | Expected Outcome |
|---------|---------|--------|------------------|
| M-012 Fraud Detection System | T-011, T-012 | HIGH | Detect fraud patterns |
| M-013 GPS Anomaly Detection | T-007 | MEDIUM | Catch location spoofing |
| M-014 Immutable Audit Logging | T-013 | MEDIUM | Tamper-evident logs |
| M-015 WebSocket Rate Limiting | T-020 | LOW | Prevent connection exhaustion |
| M-016 Content Security Policy | T-030 | LOW | XSS defense layer |

### Phase 3: Long-Term Enhancements

| Control | Threats | Effort | Expected Outcome |
|---------|---------|--------|------------------|
| M-017 Phone Verification Hardening | T-005 | MEDIUM | Stronger authentication |
| M-018 Review Anti-Gaming | T-010 | MEDIUM | Reputation integrity |

### Expected Risk Reduction

| Priority | Before | After | Reduction |
|----------|--------|-------|-----------|
| CRITICAL | 5 | 0 | -5 (100%) |
| HIGH | 12 | 3 | -9 (75%) |
| MEDIUM | 11 | 8 | -3 (27%) |
| LOW | 2 | 2 | 0 (0%) |

---

## 6. Conclusion

### Analysis Completeness

**Methodology Applied:**
- ✅ 6-stage systematic threat modeling framework
- ✅ STRIDE threat categorization
- ✅ MITRE ATT&CK technique mapping
- ✅ Cyber Kill Chain stage identification
- ✅ Evidence-based confidence assessment

**Coverage Assessment:**

| Metric | Count |
|--------|-------|
| System Components Analyzed | 21 |
| Trust Boundaries Assessed | 8 |
| Data Flows Mapped | 45+ |
| Threats Identified | 30 |
| Security Controls Recommended | 18 |

### Analysis Confidence

**Overall Confidence:** MEDIUM-HIGH

**High Confidence Areas:**
- Architecture and technology stack (well-documented)
- Data model and API endpoints (comprehensive documentation)
- Third-party integrations (clearly specified)
- User roles and functionality (detailed user stories)

**Limited Confidence Areas:**
- Rate limiting configuration (not documented)
- Input validation implementation (assumed standard practices)
- Encryption at rest settings (AWS defaults assumed)
- Logging and monitoring capabilities (not documented)

### Known Limitations

**Documentation Gaps:**
1. Security implementation details (rate limiting, input validation) not documented
2. Internal service-to-service authentication not specified
3. Encryption configuration not documented
4. Monitoring and alerting capabilities unknown

**Analytical Constraints:**
1. Analysis based on provided documentation only
2. No code review or penetration testing performed
3. Business metrics (user counts, transaction volumes) not available for quantitative risk assessment
4. Technology-specific vulnerabilities require implementation review

### Recommended Next Steps

**Immediate (This Week):**
1. Verify JWT algorithm configuration - single highest-impact quick fix
2. Implement rate limiting on `/auth/*` endpoints
3. Confirm Stripe webhook signature verification is enabled
4. Review price calculation logic for server-side enforcement

**Short-Term (This Month):**
1. Conduct authorization audit across all API endpoints
2. Implement object-level authorization middleware
3. Deploy role enforcement for all role-specific endpoints
4. Add input validation schema for all user inputs

**Ongoing:**
- Update threat model quarterly or with significant architecture changes
- Monitor for new vulnerabilities in technology stack
- Track security metrics (failed logins, authorization failures, fraud rates)
- Integrate threat model findings into security testing

### Final Remarks

QuickDeliver's architecture follows modern best practices with React Native mobile apps, Node.js backend, and AWS infrastructure. However, handling payment data, PII, and real-time location tracking creates significant security responsibilities.

The 5 CRITICAL threats identified require immediate attention - all are addressable with LOW to MEDIUM effort controls. Implementing Phase 0 controls (rate limiting, JWT hardening, webhook verification, server-side validation) would address the most severe risks quickly.

The platform's security posture can be significantly improved by systematic implementation of the recommended controls, prioritized by the roadmap provided in this report.

---

## Appendices

### Appendix A: Detailed Stage Outputs

| Stage | Output File | Content |
|-------|-------------|---------|
| 1 | `01-system-understanding.md` | Component inventory, trust boundaries, data assets, assumptions |
| 2 | `02-data-flow-analysis.md` | Data flow inventory, attack surfaces, critical paths |
| 3 | `03-threat-identification.md` | Full threat details with STRIDE/ATT&CK/Kill Chain mappings |
| 4 | `04-risk-assessment.md` | Risk ratings with justifications |
| 5 | `05-mitigation-strategy.md` | Detailed control implementation guidance |

### Appendix B: Glossary

| Term | Definition |
|------|------------|
| BOLA | Broken Object Level Authorization - API vulnerability allowing cross-user data access |
| IDOR | Insecure Direct Object Reference - accessing resources by manipulating identifiers |
| JWT | JSON Web Token - standard for secure authentication tokens |
| STRIDE | Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege |
| TOCTOU | Time-of-Check to Time-of-Use - race condition vulnerability class |
| PCI-DSS | Payment Card Industry Data Security Standard |
| MFA | Multi-Factor Authentication |
| CSP | Content Security Policy - browser security header |

---

## Report Generation Details

> **⚠️ AI-Generated Content Disclaimer**
> 
> This report was generated using the [AI Threat Modeling Framework](https://github.com/ensingm2/AI-threat-modeling-rulesets). AI-generated security analysis should be reviewed by qualified security professionals before use. No guarantees of accuracy or completeness are provided. This report is intended as a starting point for security analysis, not a definitive security assessment.

| Field | Value |
|-------|-------|
| **Generated** | 2025-12-03 |
| **Framework Version** | 1ea9259 |
| **Model** | Claude Opus 4 |
