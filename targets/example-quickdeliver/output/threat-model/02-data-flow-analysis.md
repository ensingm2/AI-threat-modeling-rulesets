# Stage 2: Data Flow Analysis
**Target:** QuickDeliver | **Date:** 2025-12-03 | **Mode:** Automatic

## 1. Stage 1 References

**Components:** C-001 to C-021 (see 01-system-understanding.md)
**Trust Boundaries:** TB-01 to TB-08

## 2. Data Flow Inventory

### Authentication Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-001 | C-001/C-002 Customer/Driver App | C-006 User Service | email, password | HTTPS | TB-01, TB-02 | No |
| DF-002 | C-006 User Service | C-013 PostgreSQL | credentials, user data | TCP | TB-03 | Yes |
| DF-003 | C-006 User Service | C-014 Redis | session token | TCP | TB-03 | Yes |
| DF-004 | C-001/C-002 Apps | External OAuth (Google/Apple/FB) | OAuth token | HTTPS | TB-01, TB-04 | No |
| DF-005 | C-006 User Service | C-001/C-002 Apps | JWT token | HTTPS | TB-02, TB-01 | No |
| DF-006 | C-001/C-002/C-003/C-004 Apps | C-005 API Gateway | JWT Bearer token | HTTPS | TB-01 | Yes |

### Customer Order Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-010 | C-001 Customer App | C-009 Merchant Service | merchant_id, location | HTTPS | TB-01, TB-02 | Yes |
| DF-011 | C-009 Merchant Service | C-013 PostgreSQL | menu query | TCP | TB-03 | Yes |
| DF-012 | C-001 Customer App | C-007 Order Service | order details, payment_method_id | HTTPS | TB-01, TB-02 | Yes |
| DF-013 | C-007 Order Service | C-010 Payment Service | order total, payment_method_id | Internal | None | Yes |
| DF-014 | C-010 Payment Service | C-017 Stripe | payment intent | HTTPS | TB-04 | Yes |
| DF-015 | C-017 Stripe | C-010 Payment Service | payment confirmation | HTTPS (webhook) | TB-04 | Yes |
| DF-016 | C-007 Order Service | C-013 PostgreSQL | order record | TCP | TB-03 | Yes |
| DF-017 | C-007 Order Service | C-008 Driver Service | order assignment request | Internal | None | Yes |
| DF-018 | C-007 Order Service | C-011 Notification Service | order confirmation | Internal | None | Yes |
| DF-019 | C-011 Notification Service | C-020 Firebase | push notification | HTTPS | TB-04 | Yes |

### Real-Time Tracking Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-020 | C-002 Driver App | C-012 Tracking Service | GPS coordinates | WSS | TB-01, TB-08 | Yes |
| DF-021 | C-012 Tracking Service | C-014 Redis | driver location | TCP | TB-03 | Yes |
| DF-022 | C-012 Tracking Service | C-001 Customer App | driver location, ETA | WSS | TB-08, TB-01 | Yes |
| DF-023 | C-012 Tracking Service | C-019 Google Maps | coordinates | HTTPS | TB-04 | Yes |
| DF-024 | C-019 Google Maps | C-012 Tracking Service | route, ETA | HTTPS | TB-04 | Yes |

### Driver Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-030 | C-002 Driver App | C-008 Driver Service | online/offline status | HTTPS | TB-01, TB-02, TB-05 | Yes |
| DF-031 | C-008 Driver Service | C-014 Redis | driver status, location | TCP | TB-03 | Yes |
| DF-032 | C-002 Driver App | C-008 Driver Service | accept/decline delivery | HTTPS | TB-01, TB-02 | Yes |
| DF-033 | C-002 Driver App | C-008 Driver Service | pickup/delivery confirmation | HTTPS | TB-01, TB-02 | Yes |
| DF-034 | C-002 Driver App | C-015 S3 | delivery proof photo | HTTPS | TB-01, TB-02 | Yes |
| DF-035 | C-008 Driver Service | C-021 Checkr | driver application | HTTPS | TB-04 | Yes |
| DF-036 | C-021 Checkr | C-008 Driver Service | background check result | HTTPS (webhook) | TB-04 | Yes |
| DF-037 | C-002 Driver App | C-010 Payment Service | instant payout request | HTTPS | TB-01, TB-02 | Yes |
| DF-038 | C-010 Payment Service | C-017 Stripe | payout transfer | HTTPS | TB-04 | Yes |

### Merchant Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-040 | C-003 Merchant Portal | C-009 Merchant Service | menu items, availability | HTTPS | TB-01, TB-02, TB-06 | Yes |
| DF-041 | C-009 Merchant Service | C-013 PostgreSQL | menu data | TCP | TB-03 | Yes |
| DF-042 | C-007 Order Service | C-003 Merchant Portal | new order alert | WSS | TB-08, TB-01 | Yes |
| DF-043 | C-003 Merchant Portal | C-007 Order Service | accept/reject order | HTTPS | TB-01, TB-02 | Yes |
| DF-044 | C-003 Merchant Portal | C-015 S3 | menu images | HTTPS | TB-01, TB-02 | Yes |
| DF-045 | C-010 Payment Service | C-017 Stripe | merchant payout | HTTPS | TB-04 | Yes |

### Admin Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-050 | C-004 Admin Portal | C-006 User Service | user search, suspend | HTTPS | TB-01, TB-02, TB-07 | Yes |
| DF-051 | C-004 Admin Portal | C-008 Driver Service | driver approval | HTTPS | TB-01, TB-02, TB-07 | Yes |
| DF-052 | C-004 Admin Portal | C-009 Merchant Service | merchant approval | HTTPS | TB-01, TB-02, TB-07 | Yes |
| DF-053 | C-004 Admin Portal | C-010 Payment Service | refund request | HTTPS | TB-01, TB-02, TB-07 | Yes |

### Notification Flows

| Flow ID | Source | Destination | Data Elements | Protocol | Trust Boundary | Auth |
|---------|--------|-------------|---------------|----------|----------------|------|
| DF-060 | C-011 Notification Service | C-018 Twilio | phone number, SMS | HTTPS | TB-04 | Yes |
| DF-061 | C-011 Notification Service | C-020 Firebase | device token, message | HTTPS | TB-04 | Yes |

## 3. Trust Boundary Crossings

| Boundary | Flows Crossing | Auth Required | Security Notes |
|----------|----------------|---------------|----------------|
| TB-01 Internet/VPC | DF-001,006,010,012,020,030-038,040-044,050-053 | Yes (JWT) | Primary attack surface; all external traffic |
| TB-02 Client/API | DF-001,006,010,012,030-038,040-044,050-053 | Yes (JWT) | Application-level auth enforcement critical |
| TB-03 API/Database | DF-002,003,011,016,021,031,041 | Yes (connection) | Internal but sensitive data access |
| TB-04 VPC/External | DF-004,014,015,019,023,024,035,036,038,045,060,061 | Yes (API keys) | Third-party API security dependencies |
| TB-05 Customer/Driver | DF-030-038 | Yes (role) | Driver-specific endpoints require role check |
| TB-06 User/Merchant | DF-040-045 | Yes (role) | Merchant-specific endpoints require role check |
| TB-07 User/Admin | DF-050-053 | Yes (admin role) | Highest privilege operations |
| TB-08 WebSocket | DF-020,022,042 | Yes (token) | Real-time channels require auth validation |

## 4. Attack Surfaces

| Entry Point | Type | Component | Boundary | Auth | Key Flows |
|-------------|------|-----------|----------|------|-----------|
| AS-01 Auth API | REST API | C-006 | TB-01,02 | No (login) | DF-001,004,005 |
| AS-02 Customer API | REST API | C-007,009 | TB-01,02 | Yes | DF-010,012 |
| AS-03 Driver API | REST API | C-008 | TB-01,02,05 | Yes | DF-030-038 |
| AS-04 Merchant API | REST API | C-009 | TB-01,02,06 | Yes | DF-040-044 |
| AS-05 Admin API | REST API | C-006-009 | TB-01,02,07 | Yes | DF-050-053 |
| AS-06 WebSocket | WSS | C-012 | TB-01,08 | Yes | DF-020,022 |
| AS-07 S3 Uploads | File Upload | C-015 | TB-01,02 | Yes | DF-034,044 |
| AS-08 Stripe Webhooks | Webhook | C-010 | TB-04 | Signature | DF-015 |
| AS-09 Checkr Webhooks | Webhook | C-008 | TB-04 | Signature | DF-036 |
| AS-10 Public Browse | REST API | C-009 | TB-01,02 | Partial | DF-010 |

## 5. Critical Data Paths

| Path Name | Flows | Data Sensitivity | Security Notes |
|-----------|-------|------------------|----------------|
| Authentication | DF-001→002→003→005 | HIGH (credentials) | Password handling, token issuance |
| Payment Processing | DF-012→013→014→015→016 | HIGH (financial) | PCI-relevant, Stripe integration |
| Driver Location | DF-020→021→022 | MEDIUM (location) | Real-time broadcast to customers |
| Instant Payout | DF-037→038 | HIGH (financial) | Driver earnings disbursement |
| Document Upload | DF-034,044 | HIGH (PII docs) | License, insurance documents |
| Admin Operations | DF-050-053 | HIGH (all data) | Privileged access to all resources |

**Confidence:** HIGH - API endpoints and data model well documented; some internal service flows inferred.

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
