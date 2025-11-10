# Stage 1: System Understanding & Scoping
**Target System:** QuickDeliver - On-Demand Delivery Platform  
**Analysis Date:** 2025-11-08  
**Operational Mode:** Automatic (Critic Stages Disabled)  
**Documentation Specialist:** Stage 1 - System Analysis

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Source Documentation Inventory](#2-source-documentation-inventory)
3. [System Description](#3-system-description)
4. [Component Inventory](#4-component-inventory)
5. [Trust Boundaries](#5-trust-boundaries)
6. [Data Asset Catalog](#6-data-asset-catalog)
7. [Analysis Scope](#7-analysis-scope)
8. [Assumptions & Constraints](#8-assumptions--constraints)
9. [Documentation Gaps](#9-documentation-gaps)
10. [Confidence Assessment](#10-confidence-assessment)
11. [Source Documentation References](#11-source-documentation-references)

---

## 1. Executive Summary

QuickDeliver is a three-sided marketplace platform connecting customers, delivery drivers, and merchants for on-demand food and goods delivery. The system operates as a simplified competitor to DoorDash and Uber Eats, with a focus on lower commission rates (15% vs. 20-30%) and better driver compensation (85% of delivery fees).

The platform comprises React Native mobile applications for customers and drivers, React web portals for merchants and administrators, and a Node.js backend API infrastructure hosted on AWS. The system leverages PostgreSQL for primary data storage, Redis for caching and session management, and integrates with critical third-party services including Stripe (payments), Google Maps (navigation/geocoding), Twilio (SMS), Firebase (push notifications), and Checkr (background checks).

**Key Security-Relevant Characteristics:**
- **Multi-actor architecture:** Three distinct user types (customers, drivers, merchants) with different privilege levels and data access requirements
- **Payment processing:** Handles customer payments, driver payouts, and merchant settlements through Stripe integration
- **Real-time tracking:** WebSocket-based GPS tracking with location data broadcast every 5 seconds
- **Sensitive data:** Processes PII, payment information, location data, and identity verification documents
- **Regulatory scope:** Subject to PCI-DSS (payment data), GDPR (EU users if applicable), and background check data regulations

**Documentation Quality:** Comprehensive business and technical documentation provided (8 files) covering business model, user stories, product roadmap, architecture, API specifications, data model, mobile app features, and third-party integrations. Technology stack explicitly documented with clear architectural patterns.

**Critical Assumptions:** Automated analysis performed without user clarification - key assumptions documented regarding deployment security configurations, authentication implementation details, and operational scale characteristics (Section 8).

## 2. Source Documentation Inventory

**Total Files Provided:** 8 documentation files  
**Documentation Location:** `/targets/example-quickdeliver/external-resources/`

### File Inventory

| File | Type | Content Summary | Lines |
|------|------|----------------|-------|
| `README.md` | Overview | System overview and documentation index | 34 |
| `business-overview.md` | Business | Business model, revenue, costs, market positioning | 57 |
| `user-stories.md` | Functional | User workflows for customers, drivers, and merchants | 91 |
| `product-roadmap.md` | Planning | Feature timeline across 3 phases (MVP, Growth, Scale) | 59 |
| `architecture-overview.md` | Technical | Tech stack, services, deployment, data flow | 130 |
| `api-endpoints.md` | Technical | REST API and WebSocket specifications | 192 |
| `data-model.md` | Technical | PostgreSQL tables, Redis cache, S3 storage | 116 |
| `mobile-app-features.md` | Functional | iOS/Android app feature descriptions | 70 |
| `third-party-integrations.md` | Technical | External service integrations and usage | 106 |

**Total Documentation Lines:** 855 lines

### Documentation Quality Assessment

**Comprehensive Coverage:**
- ✅ Business context and revenue model clearly documented
- ✅ Technology stack explicitly specified (React Native, Node.js, PostgreSQL, Redis, AWS)
- ✅ API specifications with endpoints and WebSocket events
- ✅ Data model with table structures and relationships
- ✅ Third-party integrations with purpose and features
- ✅ User workflows and feature descriptions

**Partial Coverage:**
- ⚠️ Authentication mechanisms mentioned (JWT tokens, OAuth) but implementation details limited
- ⚠️ Deployment configuration described (Docker, AWS ECS) but security hardening not specified
- ⚠️ Data flow patterns described but encryption/security controls not detailed

**Limited Coverage:**
- ⚠️ Security controls and security architecture not explicitly documented
- ⚠️ Network architecture and segmentation not detailed beyond high-level AWS services
- ⚠️ Operational scale (user counts, transaction volumes) provided as targets but not current state
- ⚠️ Incident response, logging, and monitoring implementation not specified

**Overall Assessment:** HIGH quality functional and architectural documentation; MEDIUM coverage of security-specific implementation details

## 3. System Description

### 3.1 Business Purpose

**Description:** QuickDeliver is an on-demand delivery platform connecting three parties: customers who order food/items, delivery drivers who transport orders, and merchants who fulfill orders.

**Source:** "QuickDeliver connects customers, delivery drivers, and merchants for fast on-demand delivery. Think Uber Eats or DoorDash but simpler." (README.md, lines 5-6)

**Market Positioning:** The platform competes with established players (DoorDash, Uber Eats, Grubhub) by offering lower fees and better compensation:
- Merchant commission: 15% vs. competitors' 20-30%
- Driver compensation: 85% of delivery fees
- Value proposition: Fast delivery, fair prices, low commissions

**Source:** "Our edge: Lower fees for restaurants (15% vs 20-30%), Drivers keep more money" (business-overview.md, lines 15-17)

**Confidence:** HIGH (95%) - Explicitly documented business purpose and positioning

### 3.2 Primary Users

#### User Type 1: Customers
**Description:** End users who order food/items via mobile app for delivery to their address

**Key Activities:**
- Browse restaurants by cuisine, rating, distance
- Place orders with customization (size, toppings, modifiers)
- Track orders in real-time with GPS
- Rate food and drivers
- Subscribe to QuickDeliver Plus ($10/month unlimited free delivery)

**Source:** "Customers order food/items from local merchants via mobile app" (README.md, line 9); User Stories section (user-stories.md, lines 3-36)

**Confidence:** HIGH (95%) - Explicitly documented workflows

#### User Type 2: Delivery Drivers
**Description:** Independent contractors who accept delivery requests, pick up orders, and deliver to customers

**Key Activities:**
- Go online/offline to receive delivery requests
- Accept/decline deliveries (15 seconds to decide)
- Navigate to merchant and customer locations
- Take proof-of-delivery photos
- Track earnings in real-time
- Cash out instantly ($0.50 fee) or weekly payout

**Onboarding Requirements:**
- Driver's license and vehicle information
- Insurance and registration documents
- Background check (via Checkr integration)
- Bank account for payouts

**Source:** "Drivers pick up and deliver orders" (README.md, line 10); Driver Stories section (user-stories.md, lines 39-65); Checkr integration (third-party-integrations.md, lines 63-73)

**Confidence:** HIGH (95%) - Explicitly documented workflows and requirements

#### User Type 3: Merchants
**Description:** Restaurants and businesses that receive and fulfill customer orders

**Key Activities:**
- Manage menu items with photos and prices
- Receive and accept/reject incoming orders
- Mark orders ready for driver pickup
- Track sales and payout history (weekly deposits)
- Set hours and pause/resume order acceptance

**Onboarding Requirements:**
- Business license
- Profile setup (logo, hours, delivery area)
- Bank account for payouts

**Source:** "Merchants receive and fulfill orders" (README.md, line 11); Merchant Stories section (user-stories.md, lines 68-91)

**Confidence:** HIGH (95%) - Explicitly documented workflows and requirements

#### User Type 4: Administrators
**Description:** Platform operators who approve/manage users and handle system operations

**Key Activities:**
- Approve/reject driver and merchant applications
- Suspend/ban users
- Issue refunds
- Create promo codes
- View all orders and users

**Source:** Admin Endpoints section (api-endpoints.md, lines 140-154)

**Confidence:** HIGH (90%) - API endpoints documented but admin workflows less detailed than other user types

### 3.3 Key Functionality

#### 1. Order Management
**Description:** Core ordering workflow from browsing to delivery completion

**Process Flow:**
1. Customer browses merchants and menu items
2. Adds items to cart with modifiers
3. Applies promo codes (optional)
4. Chooses ASAP or scheduled delivery
5. Adds tip and submits order with payment
6. Stripe authorizes payment
7. System assigns order to available driver
8. Driver accepts and picks up from merchant
9. Driver delivers to customer
10. Payment captured and split between parties

**Source:** "Ordering Flow" section (architecture-overview.md, lines 89-100)

**Confidence:** HIGH (95%) - Complete workflow documented

#### 2. Real-Time Order Tracking
**Description:** Live GPS-based tracking of driver location and delivery status

**Technical Implementation:**
- Driver app sends GPS coordinates every 5 seconds
- Tracking service broadcasts location to customer via WebSocket
- ETA calculated and updated dynamically
- Order status transitions: Pending → Confirmed → Preparing → Picked Up → Delivered

**Source:** "Real-Time Tracking" section (architecture-overview.md, lines 101-104); "Driver app sends GPS every 5 seconds" (architecture-overview.md, line 102)

**Confidence:** HIGH (95%) - Technical implementation explicitly documented

#### 3. Payment Processing
**Description:** Multi-party payment flow handling customer charges, platform fees, and payouts

**Stripe Integration:**
- Customer payments via credit card, Apple Pay, Google Pay
- Payment intents for order authorization/capture
- Connected accounts for drivers and merchants
- Automatic payouts (weekly for merchants, instant option for drivers with $0.50 fee)
- Subscription billing for QuickDeliver Plus

**Money Split:**
- Merchant receives order subtotal minus 15% commission
- Driver receives delivery fee + tip (85% of delivery fees to driver)
- Platform retains commission and delivery fee portion

**Source:** Payment Service description (architecture-overview.md, lines 69-73); Stripe integration details (third-party-integrations.md, lines 3-14); Business model (business-overview.md, lines 20-24)

**Confidence:** HIGH (95%) - Payment architecture and business model documented

#### 4. Multi-Actor Authentication & Authorization
**Description:** Role-based access control for four user types with different privilege levels

**Authentication Mechanisms:**
- Email/password authentication
- OAuth via Google, Apple, Facebook
- JWT tokens (15-minute expiration)
- Refresh tokens (7-day expiration)

**Source:** "Authentication" section (architecture-overview.md, lines 108-114); Auth endpoints (api-endpoints.md, lines 9-17)

**Confidence:** MEDIUM (75%) - Token types and OAuth providers documented, but authorization logic and role enforcement mechanisms not detailed

#### 5. Background Checks & Onboarding
**Description:** Driver vetting process via Checkr integration

**Process:**
- Driver submits license, vehicle info, insurance during application
- Checkr runs background check and driving record verification (3-5 days)
- Webhook notification of results
- Auto-approve or manual admin review

**Source:** Checkr integration section (third-party-integrations.md, lines 63-73)

**Confidence:** HIGH (90%) - Process flow documented

#### 6. Location Services & Navigation
**Description:** Google Maps integration for geocoding, routing, and real-time navigation

**Features:**
- Address autocomplete for customers
- Geocoding (address to coordinates conversion)
- Distance/duration calculations
- Turn-by-turn navigation for drivers
- Real-time route optimization

**APIs Used:** Places API, Geocoding API, Directions API, Distance Matrix API

**Source:** Google Maps Platform section (third-party-integrations.md, lines 32-46)

**Confidence:** HIGH (95%) - API usage explicitly documented

#### 7. Notifications & Communications
**Description:** Multi-channel alerting via push notifications, SMS, and in-app messaging

**Channels:**
- Firebase Cloud Messaging: Push notifications to mobile apps
- Twilio: SMS for verification codes and order alerts
- Phone number masking for customer-driver calls (privacy protection)

**Notification Types:**
- Order status changes (all parties)
- Driver assignment and arrival (customers)
- New order alerts (drivers, merchants)
- Promotional messages

**Source:** Notification Service (architecture-overview.md, lines 75-78); Firebase section (third-party-integrations.md, lines 48-60); Twilio section (third-party-integrations.md, lines 17-29)

**Confidence:** HIGH (95%) - Notification architecture documented

### 3.4 Operational Context

**Deployment Environment:** AWS cloud infrastructure

**Geographic Scope:**
- Phase 1 (MVP, months 1-6): Launch in 2 cities with 50k+ population
- Phase 2 (months 7-18): Expand to 3-5 additional cities
- Phase 3 (months 19-36): 20+ cities, potentially international (Canada, Mexico)

**Source:** Market description (business-overview.md, lines 9-11); Product roadmap (product-roadmap.md, lines 1-58)

**Scale Targets:**
- Phase 1: 500 drivers and 200 restaurants per city, 1,000 orders/day across 2 cities
- Phase 2: 50,000 orders/day total
- Phase 3: 200,000+ orders/day

**Source:** Launch targets (product-roadmap.md, lines 18-21, 40, 58)

**Performance Requirements:**
- API response time: < 200ms
- Real-time updates: < 2 second delay
- Uptime: 99.9%

**Source:** "Performance Targets" (architecture-overview.md, lines 126-130)

**Confidence:** HIGH (90%) - Operational targets documented; actual current scale not specified (these are future targets)

## 4. Component Inventory

### Component 1: Customer Mobile Application

**Type:** User-facing mobile application (iOS/Android)

**Primary Function:** Customer interface for browsing merchants, placing orders, tracking deliveries, and managing account

**Source:** "Customer & Driver Apps: React Native (iOS + Android)" (architecture-overview.md, line 16); Customer App features (mobile-app-features.md, lines 3-35)

#### Technology Stack
- **Documented:** 
  - React Native framework (architecture-overview.md, line 16)
  - Google Maps SDK for map display (architecture-overview.md, line 18)
  - Firebase Cloud Messaging for push notifications (architecture-overview.md, line 19)
  - iOS and Android distribution via App Store/Google Play
- **Inferred:** None
- **Unknown:** 
  - Specific React Native version
  - State management library
  - Local data persistence mechanism
  - Security libraries for certificate pinning or jailbreak detection

**Confidence:** HIGH (90%) - Core technology explicitly documented

#### Data Handled
- **User credentials:** Email, password (for authentication)
  - **Source:** Sign up/login features (user-stories.md, lines 5-9)
- **Personal information:** Name, phone number, profile photo
  - **Source:** User profile features (user-stories.md, lines 6-9)
- **Delivery addresses:** Street address, city, state, postal code, delivery instructions
  - **Source:** Save addresses feature (user-stories.md, line 9; data-model.md, lines 11-15)
- **Payment methods:** Tokenized card data (via Stripe SDK)
  - **Source:** Save payment methods feature (user-stories.md, line 8; data-model.md, lines 17-21)
- **Order data:** Cart contents, order history, tracking information
  - **Source:** Browse & Order, Track Order sections (user-stories.md, lines 11-25)
- **Location data:** User's current location for address suggestions and merchant proximity
  - **Source:** Browse restaurants by distance (user-stories.md, line 12)

#### Interactions
- **Backend API:** RESTful API calls for all business operations (authentication, browsing, orders)
  - **Source:** API endpoints for customer operations (api-endpoints.md, lines 34-68)
- **WebSocket Server:** Real-time order tracking and status updates
  - **Source:** WebSocket events for customers (api-endpoints.md, lines 161-167)
- **Stripe SDK:** Payment method tokenization (does not transmit raw card data)
  - **Source:** Stripe handles payments (user-stories.md, line 8)
- **Google Maps SDK:** Map display and location services
  - **Source:** Maps integration (architecture-overview.md, line 18)
- **Firebase:** Push notification receipt
  - **Source:** Push notifications (architecture-overview.md, line 19; third-party-integrations.md, lines 48-60)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - Core framework and integrations specified
- **Functionality Understanding:** HIGH (95%) - Comprehensive feature documentation

---

### Component 2: Driver Mobile Application

**Type:** User-facing mobile application (iOS/Android)

**Primary Function:** Driver interface for receiving delivery requests, navigating to pickup/delivery locations, and managing earnings

**Source:** "Customer & Driver Apps: React Native (iOS + Android)" (architecture-overview.md, line 16); Driver App features (mobile-app-features.md, lines 38-60)

#### Technology Stack
- **Documented:**
  - React Native framework (architecture-overview.md, line 16)
  - Google Maps SDK for navigation (architecture-overview.md, line 18)
  - Firebase Cloud Messaging for delivery alerts (architecture-overview.md, line 19)
  - GPS location services for continuous tracking
- **Inferred:** None
- **Unknown:**
  - Background location tracking implementation
  - Photo capture library for delivery proof
  - Offline operation capabilities

**Confidence:** HIGH (90%) - Core technology explicitly documented

#### Data Handled
- **Driver credentials:** Email, password, OAuth tokens
  - **Source:** Apply/login features (user-stories.md, lines 42-46)
- **Driver identity documents:** License number, vehicle info, insurance, registration
  - **Source:** Driver onboarding (user-stories.md, lines 42-45; data-model.md, lines 49-55)
- **Real-time location:** GPS coordinates updated every 5 seconds
  - **Source:** "Driver app sends GPS every 5 seconds" (architecture-overview.md, line 102)
- **Earnings data:** Real-time earnings, payout history, performance stats
  - **Source:** Earnings and Stats sections (user-stories.md, lines 57-65)
- **Order details:** Delivery requests, merchant/customer addresses, order contents
  - **Source:** Delivery workflow (user-stories.md, lines 47-56)
- **Delivery proof:** Photos of completed deliveries
  - **Source:** "Take photo of delivery" (user-stories.md, line 54)

#### Interactions
- **Backend API:** Driver-specific endpoints for status, deliveries, earnings
  - **Source:** Driver endpoints (api-endpoints.md, lines 72-100)
- **WebSocket Server:** Real-time delivery request notifications
  - **Source:** Driver WebSocket events (api-endpoints.md, lines 169-172)
- **Google Maps SDK:** Turn-by-turn navigation
  - **Source:** Navigate to restaurant/customer (user-stories.md, lines 51, 53)
- **Tracking Service:** Continuous GPS location transmission
  - **Source:** Track driver location (architecture-overview.md, line 62)
- **S3:** Upload delivery proof photos
  - **Source:** Delivery proof photos storage (data-model.md, line 114)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - Core framework and integrations specified
- **Functionality Understanding:** HIGH (95%) - Comprehensive feature documentation

---

### Component 3: Merchant Web Portal

**Type:** User-facing web application

**Primary Function:** Restaurant/business interface for managing menus, receiving orders, and tracking sales

**Source:** "Merchant & Admin Portal: React web app" (architecture-overview.md, line 17); Merchant features (user-stories.md, lines 68-91)

#### Technology Stack
- **Documented:**
  - React web application (architecture-overview.md, line 17)
  - Browser-based (implied by "web app")
- **Inferred:** None
- **Unknown:**
  - React version and state management
  - Hosting/serving mechanism (CDN, S3 static hosting)
  - Authentication persistence (cookies, localStorage)

**Confidence:** MEDIUM (75%) - Technology specified but deployment details limited

#### Data Handled
- **Merchant credentials:** Email, password, OAuth tokens
  - **Source:** Merchant authentication (api-endpoints.md, lines 9-17)
- **Business information:** Business name, license, address, hours, delivery area
  - **Source:** Merchant profile (user-stories.md, lines 70-73; data-model.md, lines 23-29)
- **Menu data:** Items, categories, prices, photos, modifiers, availability
  - **Source:** Menu management (user-stories.md, lines 75-80; data-model.md, lines 31-47)
- **Order data:** Incoming orders, order history
  - **Source:** Order management (user-stories.md, lines 81-86)
- **Financial data:** Sales reports, payout history
  - **Source:** Money & Stats (user-stories.md, lines 87-91)

#### Interactions
- **Backend API:** Merchant-specific endpoints
  - **Source:** Merchant endpoints (api-endpoints.md, lines 103-138)
- **WebSocket Server:** Real-time new order notifications
  - **Source:** Merchant WebSocket events (api-endpoints.md, lines 174-176)
- **S3:** Upload merchant logos and menu item photos
  - **Source:** Merchant logos and menu photos (data-model.md, line 113)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** MEDIUM (75%) - Framework specified, deployment unclear
- **Functionality Understanding:** HIGH (95%) - Comprehensive feature documentation

---

### Component 4: Admin Web Portal

**Type:** User-facing web application

**Primary Function:** Platform operations interface for approving users, managing system, handling refunds

**Source:** "Merchant & Admin Portal: React web app" (architecture-overview.md, line 17); Admin endpoints (api-endpoints.md, lines 140-154)

#### Technology Stack
- **Documented:**
  - React web application (architecture-overview.md, line 17)
  - Shared technology with Merchant Portal
- **Inferred:** None
- **Unknown:**
  - Whether this is a separate application or same codebase as Merchant Portal with different views
  - Admin authentication mechanisms
  - Authorization enforcement details

**Confidence:** MEDIUM (70%) - Functionality documented via API endpoints, but UI implementation less detailed

#### Data Handled
- **Admin credentials:** Email, password (elevated privileges)
  - **Source:** Admin endpoints require authentication (api-endpoints.md, line 5)
- **User data:** All users' information for search and suspension
  - **Source:** Search users, ban user endpoints (api-endpoints.md, lines 145-146)
- **Applications:** Driver and merchant approval requests with submitted documents
  - **Source:** Applications endpoints (api-endpoints.md, lines 147-150)
- **System-wide orders:** All order data for refund processing
  - **Source:** All orders endpoint (api-endpoints.md, line 151)
- **Promo codes:** Discount configuration
  - **Source:** Create promo endpoint (api-endpoints.md, line 153)

#### Interactions
- **Backend API:** Admin-specific endpoints
  - **Source:** Admin endpoints section (api-endpoints.md, lines 140-154)
- **Backend services:** Direct access to user, order, and payment services
  - **Source:** Inferred from admin operations on all system entities

**Confidence Assessment:**
- **Component Existence:** HIGH (90%) - API endpoints documented
- **Technology Details:** MEDIUM (70%) - Framework specified, implementation unclear
- **Functionality Understanding:** MEDIUM (80%) - Inferred from API capabilities

---

### Component 5: API Gateway / Load Balancer

**Type:** Infrastructure component

**Primary Function:** Route incoming traffic to backend services, distribute load across instances

**Source:** "Load Balancer: Route traffic" (architecture-overview.md, line 37); Architecture diagram (architecture-overview.md, line 8)

#### Technology Stack
- **Documented:**
  - AWS Load Balancer (architecture-overview.md, line 37)
  - Receives traffic from mobile apps (architecture-overview.md, line 8)
- **Inferred:** 
  - Likely AWS Application Load Balancer (ALB) based on AWS ECS deployment context
  - **Basis:** ECS deployments typically use ALB for HTTP/HTTPS routing
  - **Confidence:** MEDIUM (75%)
- **Unknown:**
  - TLS termination configuration
  - WAF integration
  - Rate limiting implementation
  - Health check configuration

**Confidence:** MEDIUM (75%) - Component type documented, specific configuration unknown

#### Data Handled
- **All API traffic:** All HTTP/HTTPS requests from clients to backend
- **WebSocket connections:** Initial WebSocket handshake traffic
- **Authentication tokens:** JWT tokens in Authorization headers (pass-through)
  - **Source:** All endpoints need Authorization header (api-endpoints.md, line 5)

#### Interactions
- **Clients:** Receives requests from mobile apps and web portals
  - **Source:** Architecture flow (architecture-overview.md, line 8)
- **Backend Services:** Routes to Node.js services
  - **Source:** "[Mobile Apps] → [Load Balancer] → [Node.js Services]" (architecture-overview.md, line 8)

**Confidence Assessment:**
- **Component Existence:** HIGH (90%) - Explicitly documented
- **Technology Details:** MEDIUM (75%) - AWS Load Balancer specified, type inferred
- **Functionality Understanding:** MEDIUM (75%) - Standard load balancing pattern assumed

---

### Component 6: Backend API Services

**Type:** Application server / Microservices

**Primary Function:** Business logic execution, data processing, orchestration of external services

**Source:** "Language: Node.js + Express" (architecture-overview.md, line 22); "API: REST + WebSocket" (architecture-overview.md, line 23)

#### Technology Stack
- **Documented:**
  - Node.js programming language (architecture-overview.md, line 22)
  - Express web framework (architecture-overview.md, line 22)
  - REST API pattern (architecture-overview.md, line 23)
  - WebSocket support for real-time features (architecture-overview.md, line 23)
  - JWT tokens for authentication (architecture-overview.md, line 24)
  - Docker containers (architecture-overview.md, line 119)
  - AWS ECS container orchestration (architecture-overview.md, line 32)
- **Inferred:** None
- **Unknown:**
  - Node.js version
  - Specific Express version
  - WebSocket library (ws, socket.io, etc.)
  - Process manager (PM2, clustering)
  - Logging framework
  - Input validation libraries

**Confidence:** HIGH (85%) - Core stack explicitly documented

#### Service Architecture

The backend consists of multiple services handling different domains:

**User Service**
- **Function:** Login/signup, user profiles, password management
- **Source:** User Service description (architecture-overview.md, lines 49-52)
- **Endpoints:** `/auth/*`, `/users/*` (api-endpoints.md, lines 9-30)

**Order Service**
- **Function:** Create orders, track status, order history
- **Source:** Order Service description (architecture-overview.md, lines 54-57)
- **Endpoints:** `/orders/*` (api-endpoints.md, lines 44-54)

**Driver Service**
- **Function:** Driver signup, assignment algorithm, location tracking
- **Source:** Driver Service description (architecture-overview.md, lines 59-62)
- **Endpoints:** `/drivers/*` (api-endpoints.md, lines 72-100)

**Merchant Service**
- **Function:** Restaurant profiles, menus, hours and availability
- **Source:** Merchant Service description (architecture-overview.md, lines 64-67)
- **Endpoints:** `/merchants/*` (api-endpoints.md, lines 36-42, 103-138)

**Payment Service**
- **Function:** Stripe integration, payment processing, money split, refunds
- **Source:** Payment Service description (architecture-overview.md, lines 69-73)
- **Endpoints:** Payment operations embedded in order/user flows

**Notification Service**
- **Function:** Push notifications, SMS alerts, emails
- **Source:** Notification Service description (architecture-overview.md, lines 75-78)
- **Integration:** Firebase, Twilio (third-party-integrations.md)

**Tracking Service**
- **Function:** WebSocket server for real-time location, ETA calculation, route optimization
- **Source:** Tracking Service description (architecture-overview.md, lines 80-83)
- **WebSocket:** `wss://ws.quickdeliver.com` (api-endpoints.md, line 159)

#### Data Handled
- **All business data:** Users, orders, merchants, drivers, payments, menus, reviews, promotions
- **Credentials:** Password hashes, OAuth tokens, JWT tokens
  - **Source:** Authentication section (architecture-overview.md, lines 108-114)
- **Payment data:** Stripe tokens and payment intent IDs (not raw card data)
  - **Source:** Payment methods table (data-model.md, lines 17-21)
- **Sensitive documents:** Driver licenses, insurance, business licenses
  - **Source:** Driver/merchant onboarding (data-model.md, line 115)

#### Interactions
- **PostgreSQL Database:** Read/write all persistent data
  - **Source:** PostgreSQL main database (architecture-overview.md, line 27)
- **Redis Cache:** Session storage, online driver tracking, menu caching
  - **Source:** Redis cache and session (architecture-overview.md, line 28); Redis keys (data-model.md, lines 100-107)
- **S3:** Upload/retrieve images and documents
  - **Source:** S3 file storage (architecture-overview.md, line 29); S3 storage list (data-model.md, lines 110-116)
- **Stripe API:** Payment processing, payouts, subscriptions
  - **Source:** Stripe integration (third-party-integrations.md, lines 3-14)
- **Google Maps API:** Geocoding, directions, distance calculations
  - **Source:** Google Maps Platform (third-party-integrations.md, lines 32-46)
- **Twilio API:** SMS sending, phone number masking
  - **Source:** Twilio integration (third-party-integrations.md, lines 17-29)
- **Firebase API:** Send push notifications
  - **Source:** Firebase Cloud Messaging (third-party-integrations.md, lines 48-60)
- **Checkr API:** Background check processing
  - **Source:** Checkr integration (third-party-integrations.md, lines 63-73)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (85%) - Core stack specified, libraries/versions unknown
- **Functionality Understanding:** HIGH (95%) - Comprehensive service breakdown

---

### Component 7: PostgreSQL Database

**Type:** Database (Relational)

**Primary Function:** Primary persistent storage for all business entities and transactional data

**Source:** "PostgreSQL: Main database (users, orders, merchants, menus)" (architecture-overview.md, line 27); "RDS: Managed PostgreSQL database" (third-party-integrations.md, line 89)

#### Technology Stack
- **Documented:**
  - PostgreSQL RDBMS (architecture-overview.md, line 27)
  - AWS RDS managed service (third-party-integrations.md, line 89)
- **Inferred:** None
- **Unknown:**
  - PostgreSQL version
  - RDS instance type/size
  - Multi-AZ configuration
  - Backup retention policy
  - Encryption at rest configuration
  - Read replicas

**Confidence:** HIGH (85%) - Database type and hosting explicitly documented

#### Data Schema

**Tables (from data-model.md, lines 5-97):**
1. **users** - User accounts (all roles), email, password_hash, phone, role
2. **addresses** - Delivery addresses with coordinates
3. **payment_methods** - Tokenized payment references (Stripe IDs)
4. **merchants** - Restaurant/business profiles, ratings
5. **menu_categories** - Menu organization
6. **menu_items** - Items with prices, photos, availability
7. **item_modifiers** - Customization options (size, toppings)
8. **modifier_options** - Specific choices with price adjustments
9. **drivers** - Driver profiles, status, location, ratings
10. **orders** - Order lifecycle tracking, payment status, timestamps
11. **order_items** - Order line items with quantities
12. **order_item_modifiers** - Selected customizations per item
13. **reviews** - Ratings and comments for merchants/drivers
14. **promotions** - Promo codes with discount rules
15. **subscriptions** - QuickDeliver Plus memberships
16. **payouts** - Payment history for drivers/merchants

**Source:** Data Model section (data-model.md, lines 5-97)

#### Data Handled
- **Authentication:** Password hashes, email addresses
- **PII:** Names, phone numbers, addresses
- **Financial:** Order totals, commission rates, payout amounts, Stripe IDs
- **Location:** Latitude/longitude for merchants and delivery addresses
- **Business:** Menus, pricing, availability
- **Operational:** Order status, ratings, timestamps

#### Interactions
- **Backend Services:** All services read/write to PostgreSQL
  - **Source:** Primary database for business logic (architecture-overview.md, line 27)
- **Redis:** Cache layer sits in front for performance
  - **Source:** Redis cache (architecture-overview.md, line 28)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (85%) - Database and hosting specified
- **Functionality Understanding:** HIGH (95%) - Complete schema documented

---

### Component 8: Redis Cache

**Type:** Database (In-memory cache)

**Primary Function:** Session storage, driver location tracking, menu caching for performance

**Source:** "Redis: Cache and session storage" (architecture-overview.md, line 28); "ElastiCache: Managed Redis" (third-party-integrations.md, line 92)

#### Technology Stack
- **Documented:**
  - Redis in-memory data store (architecture-overview.md, line 28)
  - AWS ElastiCache managed service (third-party-integrations.md, line 92)
- **Inferred:** None
- **Unknown:**
  - Redis version
  - Persistence configuration (RDB/AOF)
  - Cluster configuration
  - Eviction policies
  - Backup strategy

**Confidence:** HIGH (85%) - Cache type and hosting explicitly documented

#### Data Handled

**Cached Keys (from data-model.md, lines 102-107):**
- `session:{user_id}` - JWT session data
- `driver:location:{driver_id}` - Real-time GPS coordinates
- `drivers:online:{city}` - Set of available driver IDs per city
- `menu:{merchant_id}` - Cached menu data for performance

**Source:** Redis Cache section (data-model.md, lines 100-107)

**Data Characteristics:**
- Temporary/ephemeral data
- Performance optimization layer
- Real-time operational state (online drivers, current locations)

#### Interactions
- **Backend Services:** All services use Redis for session validation and caching
  - **Source:** Cache and session storage (architecture-overview.md, line 28)
- **PostgreSQL:** Cache sits in front of database
  - **Source:** Implied by caching architecture pattern

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (85%) - Technology and hosting specified
- **Functionality Understanding:** HIGH (90%) - Cache keys and usage documented

---

### Component 9: AWS S3 Storage

**Type:** Object Storage

**Primary Function:** Store images, photos, and documents

**Source:** "S3: Images and files" (architecture-overview.md, line 29); S3 Storage list (data-model.md, lines 110-116)

#### Technology Stack
- **Documented:**
  - AWS S3 object storage (architecture-overview.md, line 29)
  - CloudFront CDN for distribution (architecture-overview.md, line 36; third-party-integrations.md, line 86)
- **Inferred:** None
- **Unknown:**
  - Bucket configuration (public/private)
  - Access control mechanisms (IAM, bucket policies)
  - Encryption at rest settings
  - Versioning enabled
  - Lifecycle policies

**Confidence:** HIGH (85%) - Storage service explicitly documented

#### Data Handled

**File Types (from data-model.md, lines 112-115):**
- User profile photos
- Merchant logos and menu item photos
- Delivery proof photos
- Driver/merchant documents (licenses, permits, insurance, business licenses)

**Source:** S3 Storage section (data-model.md, lines 110-116)

**Data Sensitivity:**
- **Public:** Menu photos, merchant logos (served via CloudFront CDN)
- **Private:** Identity documents, delivery proof photos, user profile photos

#### Interactions
- **Backend Services:** Upload and retrieve files via AWS SDK
  - **Source:** S3 file storage (architecture-overview.md, line 29)
- **CloudFront CDN:** Serves public images for performance
  - **Source:** CDN for images/static files (architecture-overview.md, line 36)
- **Mobile Apps:** Direct upload of photos (delivery proof, profile photos)
  - **Source:** Photo upload features (user-stories.md, line 54; mobile-app-features.md, line 52)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (85%) - Service specified, configuration unknown
- **Functionality Understanding:** HIGH (90%) - File types and usage documented

---

### Component 10: Stripe Payment Gateway

**Type:** External Integration (Payment Processor)

**Primary Function:** Payment processing, payout management, subscription billing

**Source:** "Stripe: Payments" (README.md, line 32); Stripe integration (third-party-integrations.md, lines 3-14)

#### Technology Stack
- **Documented:**
  - Stripe API integration (third-party-integrations.md, lines 3-14)
  - Payment Intents API for orders
  - Connected Accounts for drivers/merchants
  - Subscription API for QuickDeliver Plus
  - Webhook notifications for payment events
- **Inferred:** None
- **Unknown:**
  - Stripe SDK version
  - PCI compliance implementation (Stripe.js vs. server-side)
  - Webhook signature verification implementation

**Confidence:** HIGH (90%) - Integration explicitly documented

#### Data Handled
- **Customer payment methods:** Credit cards, Apple Pay, Google Pay (tokenized)
- **Payment transactions:** Payment intents, charges, refunds
- **Connected accounts:** Driver and merchant payout account information
- **Subscription data:** QuickDeliver Plus memberships

**Source:** Stripe features (third-party-integrations.md, lines 10-14)

**Data Flow:**
- **Customer → Stripe:** Payment method tokenization (card data never touches QuickDeliver servers)
- **QuickDeliver → Stripe:** Payment intent creation, capture, transfers
- **Stripe → QuickDeliver:** Webhook notifications for payment events

#### Interactions
- **Payment Service:** Create payment intents, process refunds, manage subscriptions
  - **Source:** Payment Service (architecture-overview.md, lines 69-73)
- **Backend API:** Webhook receiver for payment status updates
  - **Source:** Webhook notifications (third-party-integrations.md, line 14)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - API features specified
- **Functionality Understanding:** HIGH (90%) - Payment flows documented

---

### Component 11: Google Maps Platform

**Type:** External Integration (Location Services)

**Primary Function:** Geocoding, routing, navigation, address autocomplete

**Source:** "Maps: Google Maps" (README.md, line 33); Google Maps Platform (third-party-integrations.md, lines 32-46)

#### Technology Stack
- **Documented:**
  - Places API (autocomplete)
  - Geocoding API (address to coordinates)
  - Directions API (routing)
  - Distance Matrix API (distance/duration calculations)
- **Inferred:** None
- **Unknown:**
  - API key management and restrictions
  - Rate limiting handling
  - Fallback mechanisms for API failures

**Confidence:** HIGH (95%) - API usage explicitly documented

#### Data Handled
- **Addresses:** Customer delivery addresses, merchant locations
- **Coordinates:** Latitude/longitude pairs
- **Routes:** Turn-by-turn navigation instructions
- **Location searches:** User location queries

**Source:** Google Maps features (third-party-integrations.md, lines 37-40)

#### Interactions
- **Backend Services:** Geocode addresses, calculate distances/ETAs
  - **Source:** Geocoding, distance calculations (third-party-integrations.md, lines 37-40)
- **Driver App:** Turn-by-turn navigation
  - **Source:** Navigate to restaurant/customer (user-stories.md, lines 51, 53)
- **Customer App:** Address autocomplete, merchant proximity
  - **Source:** Browse by distance (user-stories.md, line 12)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (95%) - Specific APIs listed
- **Functionality Understanding:** HIGH (95%) - Use cases documented

---

### Component 12: Twilio Communication Service

**Type:** External Integration (SMS/Voice)

**Primary Function:** SMS verification, notifications, phone number masking for calls

**Source:** "Twilio: SMS" (README.md, line 32); Twilio integration (third-party-integrations.md, lines 17-29)

#### Technology Stack
- **Documented:**
  - Programmable SMS API
  - Phone number masking service
- **Inferred:** None
- **Unknown:**
  - Twilio SDK version
  - SMS template management
  - Rate limiting and retry logic

**Confidence:** HIGH (90%) - Integration explicitly documented

#### Data Handled
- **Phone numbers:** User phone numbers for SMS delivery
- **SMS content:** Verification codes, order status notifications
- **Call routing:** Masked numbers for customer-driver calls

**Source:** Twilio features (third-party-integrations.md, lines 24-28)

#### Interactions
- **Notification Service:** Send SMS for verification and alerts
  - **Source:** SMS verification codes, order status notifications (third-party-integrations.md, lines 21-23)
- **Backend API:** Initiate calls and SMS
  - **Source:** Customer support calls (third-party-integrations.md, line 24)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - API features specified
- **Functionality Understanding:** HIGH (90%) - Use cases documented

---

### Component 13: Firebase Cloud Messaging

**Type:** External Integration (Push Notifications)

**Primary Function:** Deliver push notifications to iOS and Android mobile apps

**Source:** "Notifications: Firebase Cloud Messaging" (architecture-overview.md, line 19); Firebase section (third-party-integrations.md, lines 48-60)

#### Technology Stack
- **Documented:**
  - Firebase Cloud Messaging (FCM) service
  - Mobile app integration for notification receipt
- **Inferred:** None
- **Unknown:**
  - FCM SDK version
  - Notification payload structure
  - Topic-based vs. device token implementation

**Confidence:** HIGH (90%) - Integration explicitly documented

#### Data Handled
- **Device tokens:** FCM registration tokens for mobile devices
- **Notification payloads:** Order updates, delivery alerts, promotional messages

**Notification Types (from third-party-integrations.md, lines 55-59):**
- Order status changes
- New order alerts (drivers/merchants)
- Promotional messages
- Chat messages

#### Interactions
- **Notification Service:** Send push notifications via FCM API
  - **Source:** Push notifications to mobile apps (third-party-integrations.md, lines 51-52)
- **Mobile Apps:** Receive and display notifications
  - **Source:** Push notifications feature (mobile-app-features.md, line 66)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - Service specified
- **Functionality Understanding:** HIGH (90%) - Notification types documented

---

### Component 14: Checkr Background Check Service

**Type:** External Integration (Identity Verification)

**Primary Function:** Driver background checks and driving record verification

**Source:** Checkr integration (third-party-integrations.md, lines 63-73)

#### Technology Stack
- **Documented:**
  - Checkr API integration
  - Webhook notifications for check results
- **Inferred:** None
- **Unknown:**
  - Checkr API version
  - Check types configured
  - Data retention policy

**Confidence:** HIGH (90%) - Integration explicitly documented

#### Data Handled
- **Driver identity information:** Name, address, driver's license number, SSN (likely)
- **Background check results:** Criminal records, driving history
- **Verification status:** Pass/fail, pending status

**Source:** Background check process (third-party-integrations.md, lines 69-72)

#### Interactions
- **Driver Service:** Submit driver information for background checks
  - **Source:** Driver submits info during onboarding (third-party-integrations.md, line 70)
- **Backend API:** Webhook receiver for check completion
  - **Source:** Webhook notifies of results (third-party-integrations.md, line 71)
- **Admin Portal:** Manual review of borderline cases
  - **Source:** Auto-approve or manual review (third-party-integrations.md, line 72)

**Confidence Assessment:**
- **Component Existence:** HIGH (95%) - Explicitly documented
- **Technology Details:** HIGH (90%) - API and webhook documented
- **Functionality Understanding:** HIGH (90%) - Process flow specified

---

## 5. Trust Boundaries

### Trust Boundary 1: Public Internet ↔ Load Balancer

**Type:** Network Boundary

**Separates:** Untrusted public internet (users, attackers) ↔ QuickDeliver infrastructure entry point

**Identification Basis:**
**Source:** Architecture diagram shows mobile apps connecting to load balancer (architecture-overview.md, line 8); All endpoints require authentication except login/signup (api-endpoints.md, line 5)

**Confidence:** HIGH (90%) - Standard internet-facing application boundary

**Security Implications:**
- **Authentication Required:** YES (except public endpoints: `/auth/register`, `/auth/login`, `/auth/login/social`)
  - **Source:** "All endpoints need `Authorization: Bearer <token>` header except login/signup" (api-endpoints.md, line 5)
- **Data Validation Required:** YES - All user inputs must be validated (untrusted source)
  - **Basis:** Standard security practice for internet-facing applications
  - **Confidence:** MEDIUM (75%) - Not explicitly documented
- **Encryption Required:** YES - HTTPS/TLS for all API communications
  - **Source:** API base URL uses HTTPS (api-endpoints.md, line 3)
  - **Confidence:** HIGH (90%)

**Attack Surface:**
- REST API endpoints (34+ documented endpoints)
- WebSocket connection endpoint
- OAuth callback endpoints
- Webhook receivers (Stripe, Checkr)

---

### Trust Boundary 2: Mobile Apps ↔ Backend Services

**Type:** Process Boundary

**Separates:** Client-side execution environment (user devices) ↔ Server-side business logic

**Identification Basis:**
**Source:** React Native apps communicate via API (architecture-overview.md, line 8); JWT authentication enforced (architecture-overview.md, line 24)

**Confidence:** HIGH (95%) - Explicitly documented client-server architecture

**Security Implications:**
- **Authentication Required:** YES - JWT tokens for all authenticated operations
  - **Source:** "Auth: JWT tokens" (architecture-overview.md, line 24); "Token required for all API calls" (architecture-overview.md, line 112)
- **Data Validation Required:** YES - Cannot trust client-side validation
  - **Basis:** Standard security practice; client environment is untrusted
  - **Confidence:** MEDIUM (75%)
- **Encryption Required:** YES - HTTPS for data in transit
  - **Source:** HTTPS API base URL (api-endpoints.md, line 3)

**Trust Level Change:**
- **Before boundary:** User-controlled device, manipulable requests, visible data
- **After boundary:** Server-controlled environment, validated operations, secure data handling

---

### Trust Boundary 3: Authenticated Users ↔ Elevated Privileges (Admin)

**Type:** Privilege Boundary

**Separates:** Regular users (customers, drivers, merchants) ↔ Administrators

**Identification Basis:**
**Source:** User roles in database (data-model.md, line 7); Admin-specific endpoints (api-endpoints.md, lines 140-154)

**Confidence:** HIGH (90%) - Role-based access control evident from data model and API structure

**Security Implications:**
- **Authorization Required:** YES - Admin operations restricted to admin role
  - **Source:** Separate admin endpoints for privileged operations (api-endpoints.md, lines 140-154)
  - **Confidence:** MEDIUM (75%) - Endpoint separation documented, enforcement mechanism not detailed
- **Audit Logging Required:** YES (assumed for compliance)
  - **Basis:** Admin operations (suspend users, refunds, promo creation) require audit trails
  - **Confidence:** LOW (60%) - Not explicitly documented

**Privileged Operations:**
- User suspension/banning
- Driver/merchant approval
- System-wide order access and refunds
- Promo code creation

**Risk:** Privilege escalation, unauthorized administrative access

---

### Trust Boundary 4: User Roles - Customer vs. Driver vs. Merchant

**Type:** Privilege Boundary

**Separates:** Different user role contexts with different data access permissions

**Identification Basis:**
**Source:** User role field (data-model.md, line 7); Separate API endpoint namespaces for each role (api-endpoints.md)

**Confidence:** HIGH (90%) - Clear role separation in data model and API design

**Security Implications:**
- **Authorization Required:** YES - Users can only access data/operations for their role
  - **Examples:**
    - Drivers see delivery opportunities, not all orders
    - Merchants see only their menu and orders, not other merchants
    - Customers see only their own order history
  - **Source:** Separate endpoint namespaces `/drivers/*`, `/merchants/*`, `/customers` implied by merchant-specific `/merchants/me/*` (api-endpoints.md)
  - **Confidence:** MEDIUM (75%) - API structure implies authorization, but enforcement not detailed

**Cross-Role Access Requirements:**
- Order data: All three roles need access to same order (different views)
  - Customer: Order status, tracking
  - Driver: Pickup/delivery details
  - Merchant: Preparation instructions
- User data: Limited cross-role visibility
  - Customer sees driver name/photo during delivery
  - Driver sees customer delivery address (but phone masked via Twilio)
  - Merchant sees order details but not customer payment info

---

### Trust Boundary 5: Backend Services ↔ PostgreSQL Database

**Type:** Process Boundary

**Separates:** Application logic layer ↔ Data persistence layer

**Identification Basis:**
**Source:** Node.js services read/write to PostgreSQL (architecture-overview.md, lines 22-27)

**Confidence:** HIGH (90%) - Standard application-database architecture

**Security Implications:**
- **Authentication Required:** YES - Database credentials required
  - **Basis:** Standard RDS security; not publicly accessible
  - **Confidence:** MEDIUM (75%) - Not explicitly documented
- **Data Validation Required:** YES - SQL injection prevention
  - **Basis:** Standard security practice for database interactions
  - **Confidence:** MEDIUM (75%) - Not explicitly documented
- **Encryption Required:** Unknown - Encryption in transit to RDS not documented
  - **Confidence:** INSUFFICIENT

**Trust Level Change:**
- **Before boundary:** Application logic with business rules
- **After boundary:** Raw data storage without business logic enforcement

---

### Trust Boundary 6: Backend Services ↔ Redis Cache

**Type:** Process Boundary

**Separates:** Application logic ↔ Session/cache storage

**Identification Basis:**
**Source:** Backend uses Redis for cache and session storage (architecture-overview.md, line 28)

**Confidence:** HIGH (90%) - Explicitly documented caching layer

**Security Implications:**
- **Authentication Required:** YES (assumed) - Redis connection authentication
  - **Basis:** Standard ElastiCache security
  - **Confidence:** MEDIUM (70%) - Not explicitly documented
- **Data Sensitivity:** HIGH - Contains JWT sessions and driver locations
  - **Source:** Session keys and location data (data-model.md, lines 103-104)
- **Encryption Required:** Unknown - TLS to ElastiCache not documented
  - **Confidence:** INSUFFICIENT

**Risk:** Session hijacking if cache compromised

---

### Trust Boundary 7: Backend Services ↔ S3 Storage

**Type:** Process Boundary / Organizational Boundary

**Separates:** Application logic ↔ AWS managed storage service

**Identification Basis:**
**Source:** Backend uploads/retrieves files from S3 (architecture-overview.md, line 29)

**Confidence:** HIGH (90%) - Explicitly documented integration

**Security Implications:**
- **Authentication Required:** YES - IAM credentials or roles for S3 access
  - **Basis:** Standard AWS security model
  - **Confidence:** MEDIUM (75%) - Not explicitly documented
- **Authorization Required:** YES - Bucket policies and IAM permissions
  - **Basis:** S3 stores sensitive documents (licenses, insurance)
  - **Source:** Driver/merchant documents (data-model.md, line 115)
  - **Confidence:** MEDIUM (75%)
- **Encryption Required:** YES (recommended) - Documents contain PII
  - **Basis:** Identity documents are sensitive
  - **Confidence:** LOW (60%) - Encryption not documented

**Public vs. Private Data:**
- **Public (via CloudFront):** Menu photos, merchant logos
- **Private:** Identity documents, delivery proof, profile photos

---

### Trust Boundary 8: Backend Services ↔ External APIs (Stripe, Google Maps, Twilio, Firebase, Checkr)

**Type:** Organizational Boundary

**Separates:** QuickDeliver-controlled infrastructure ↔ Third-party service providers

**Identification Basis:**
**Source:** Multiple third-party integrations documented (third-party-integrations.md, lines 1-106)

**Confidence:** HIGH (95%) - Explicitly documented integrations

**Security Implications:**

**For Each Integration:**

**Stripe:**
- **Authentication:** API keys required
- **Data Transmitted:** Payment tokens, customer/merchant IDs, transaction amounts
- **Trust Level:** HIGH - PCI-compliant payment processor
- **Risk:** API key exposure, webhook spoofing

**Google Maps:**
- **Authentication:** API keys required
- **Data Transmitted:** Addresses, coordinates, routes
- **Trust Level:** HIGH - Established provider
- **Risk:** API key abuse, rate limiting, location data exposure

**Twilio:**
- **Authentication:** API keys required
- **Data Transmitted:** Phone numbers, SMS content
- **Trust Level:** HIGH - Communications provider
- **Risk:** SMS interception, phone number enumeration

**Firebase (FCM):**
- **Authentication:** Server keys required
- **Data Transmitted:** Device tokens, notification payloads
- **Trust Level:** HIGH - Google service
- **Risk:** Notification spoofing, device token exposure

**Checkr:**
- **Authentication:** API keys required
- **Data Transmitted:** Driver PII, SSN, license numbers
- **Trust Level:** HIGH - Specialized background check provider
- **Risk:** PII exposure, webhook spoofing

**Common Security Controls:**
- **API Key Management:** Secure storage required (not documented)
- **Webhook Verification:** Signature validation required (not documented)
- **TLS/HTTPS:** Required for all external API calls (implied by service standards)
- **Rate Limiting:** Handling required (not documented)

**Confidence:** MEDIUM (75%) - Integrations documented, security controls not detailed

---

### Trust Boundary 9: WebSocket Connections - Real-Time Tracking

**Type:** Network Boundary / Session Boundary

**Separates:** Stateless HTTP/REST ↔ Stateful WebSocket connections

**Identification Basis:**
**Source:** WebSocket server for real-time location tracking (architecture-overview.md, line 23); WebSocket events (api-endpoints.md, lines 157-177)

**Confidence:** HIGH (90%) - Explicitly documented WebSocket usage

**Security Implications:**
- **Authentication Required:** YES - Auth token required on WebSocket connection
  - **Source:** "Connect: `wss://ws.quickdeliver.com` with auth token" (api-endpoints.md, line 159)
  - **Confidence:** HIGH (90%)
- **Authorization Required:** YES - Users should only receive events for their orders
  - **Basis:** Customer shouldn't see other customers' driver locations
  - **Confidence:** MEDIUM (70%) - Not explicitly documented
- **Encryption Required:** YES - WSS (WebSocket Secure) protocol
  - **Source:** "wss://" prefix (api-endpoints.md, line 159)
  - **Confidence:** HIGH (90%)

**Risk:** Unauthorized location tracking, event injection

---

### Trust Boundary 10: Driver Mobile App ↔ Location Services

**Type:** Process Boundary

**Separates:** Application process ↔ Device GPS/location services

**Identification Basis:**
**Source:** Driver app sends GPS every 5 seconds (architecture-overview.md, line 102); GPS tracking feature (mobile-app-features.md, line 66)

**Confidence:** HIGH (90%) - Location tracking explicitly documented

**Security Implications:**
- **Permission Required:** YES - iOS/Android location permissions
  - **Basis:** Standard mobile OS security model
  - **Confidence:** HIGH (90%)
- **Privacy Considerations:** HIGH - Continuous driver location tracking
  - **Basis:** 5-second GPS updates while driver is working
  - **Source:** Architecture overview (architecture-overview.md, line 102)
- **Data Sensitivity:** HIGH - Real-time geolocation data
  - **Risk:** Driver surveillance, location history exposure

---

## 6. Data Asset Catalog

### Data Asset 1: User Authentication Credentials

**Type:** Credentials

**Description:** User login credentials for all user roles (customers, drivers, merchants, administrators)

**Components:**
- Email addresses (username)
- Password hashes (bcrypt/scrypt/pbkdf2 assumed)
- OAuth tokens (Google, Apple, Facebook)
- JWT access tokens (15-minute expiration)
- Refresh tokens (7-day expiration)

**Source:** "Users log in with email/password or OAuth" (architecture-overview.md, line 110); "Token expires after 15 min, refresh token for 7 days" (architecture-overview.md, line 113); Users table (data-model.md, lines 5-9)

**Sensitivity Classification:** RESTRICTED

**Basis:** Compromise enables account takeover; credential data requires highest protection level

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **GDPR:** Applicable - Email addresses are PII
  - **Justification:** Email is directly identifiable personal information
- **PCI-DSS:** Not Applicable - Passwords are not payment card data
- **Data Breach Notification Laws:** Applicable - Most jurisdictions require notification for credential breaches

**Storage Locations:**
- **PostgreSQL `users` table:** email, password_hash (data-model.md, line 6)
- **Redis cache:** `session:{user_id}` keys store JWT session data (data-model.md, line 103)

**Transmission Paths:**
- Client (Mobile App/Web Portal) → Load Balancer → Backend API (login/signup/refresh)
- Backend API → OAuth providers (Google, Apple, Facebook) for social login
- Backend API → Redis (session storage)
- Backend API → PostgreSQL (credential storage)

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** User accounts and credentials retained indefinitely unless user deletes account
- **Confidence:** MEDIUM (70%)

---

### Data Asset 2: Personal Identifiable Information (PII) - User Profiles

**Type:** PII

**Description:** Personal information for all users

**Components:**
- First name, last name
- Phone numbers
- Email addresses
- Profile photos (S3 URLs)
- User ID (internal identifier)

**Source:** Users table (data-model.md, lines 5-9); Profile features (user-stories.md, lines 6-9, 23-24)

**Sensitivity Classification:** CONFIDENTIAL

**Basis:** Personal data subject to privacy regulations; unauthorized disclosure causes privacy harm

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **GDPR:** Applicable (if EU users)
  - **Justification:** Names, phone, email are directly identifiable personal data
  - **Rights:** Access, rectification, erasure, portability
- **CCPA:** Applicable (if California users)
  - **Justification:** Personal information of California residents
- **Data Breach Notification Laws:** Applicable

**Storage Locations:**
- **PostgreSQL `users` table:** first_name, last_name, email, phone (data-model.md, lines 5-9)
- **S3:** User profile photos (data-model.md, line 112)

**Transmission Paths:**
- Mobile Apps/Web Portals → Backend API (profile management)
- Backend API → PostgreSQL (storage)
- Mobile Apps → S3 (profile photo upload, possibly via backend pre-signed URLs)

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Retained as long as account is active; must support deletion per GDPR Article 17 (Right to Erasure)
- **Confidence:** MEDIUM (70%)

---

### Data Asset 3: Location Data

**Type:** PII / Location Data

**Description:** Geographic coordinates and addresses

**Components:**
- **Customer delivery addresses:** Street, city, state, postal code, latitude/longitude, delivery instructions
- **Merchant locations:** Business address, coordinates
- **Driver real-time location:** GPS coordinates updated every 5 seconds
- **Driver location history:** Implicit from order delivery routes

**Source:** Addresses table (data-model.md, lines 11-15); Merchants table (data-model.md, line 26); Drivers table (data-model.md, line 53); "Driver app sends GPS every 5 seconds" (architecture-overview.md, line 102)

**Sensitivity Classification:** CONFIDENTIAL

**Basis:** Location data reveals home addresses, movement patterns, and personal routines; subject to privacy regulations

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **GDPR:** Applicable - Location data is personal data (Article 4.1)
  - **Justification:** Can identify individuals through home/work addresses and movement patterns
  - **Special Consideration:** Real-time tracking requires legitimate interest or consent
- **CCPA:** Applicable - Geolocation is sensitive personal information
- **Surveillance Concerns:** Driver tracking raises employment law and privacy issues

**Storage Locations:**
- **PostgreSQL `addresses` table:** Customer delivery addresses with coordinates (data-model.md, lines 11-15)
- **PostgreSQL `merchants` table:** Business locations (data-model.md, line 26)
- **PostgreSQL `drivers` table:** current_latitude, current_longitude (data-model.md, line 53)
- **Redis cache:** `driver:location:{driver_id}` - Real-time GPS (data-model.md, line 104)

**Transmission Paths:**
- **Driver App → Backend API → Redis:** GPS updates every 5 seconds
- **Backend API → Customer App (via WebSocket):** Driver location during delivery
- **Customer App → Backend API:** Delivery address entry
- **Backend API → Google Maps API:** Geocoding, routing

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** 
  - Current driver location in Redis: Ephemeral, cleared when driver goes offline
  - Delivery addresses: Retained with order history
  - Driver location history: Not explicitly stored but reconstructable from order pickups/deliveries
- **Confidence:** MEDIUM (70%)

---

### Data Asset 4: Payment Information

**Type:** Financial / Payment Card Data

**Description:** Payment-related information for transactions

**Components:**
- **Customer payment methods:** Tokenized via Stripe (Stripe payment_method_id), last 4 digits, expiry month/year, card type
- **Order payment data:** Subtotal, tax, delivery fee, tip, total amounts, payment status
- **Stripe identifiers:** payment_intent_id, subscription_id, transfer_id
- **Bank account information:** For driver/merchant payouts (stored by Stripe, not QuickDeliver)

**Source:** Payment_methods table (data-model.md, lines 17-21); Orders table (data-model.md, lines 56-65); Stripe integration (third-party-integrations.md, lines 3-14)

**Sensitivity Classification:** RESTRICTED

**Basis:** Payment data subject to PCI-DSS; high value for fraud; financial privacy concerns

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **PCI-DSS:** Applicable
  - **Scope:** QuickDeliver does not store/process raw card data (Stripe handles tokenization)
  - **Justification:** "Stripe handles it" (user-stories.md, line 8); Only tokens and last 4 digits stored
  - **Compliance Level:** Likely SAQ A or SAQ A-EP (depending on Stripe integration method)
- **GDPR:** Applicable - Financial data is personal data
- **PSD2 (EU):** Applicable if operating in EU - Payment services regulation

**Storage Locations:**
- **PostgreSQL `payment_methods` table:** Stripe token references, last_four, expiry (data-model.md, lines 17-21)
- **PostgreSQL `orders` table:** Transaction amounts, payment status, Stripe IDs (data-model.md, lines 56-65)
- **Stripe (external):** Actual payment card data, bank accounts (PCI-compliant vault)

**Transmission Paths:**
- **Customer App → Stripe (direct):** Card tokenization via Stripe SDK (data never touches QuickDeliver servers)
- **Backend API → Stripe:** Payment intent creation, capture, refunds
- **Stripe → Backend API (webhook):** Payment status updates

**Retention Requirements:**
- **Documented:** Not specified
- **PCI-DSS Requirement:** Card data retention must follow PCI standards (tokens can be retained, raw data cannot)
- **Assumption:** Payment method tokens retained until customer deletes; transaction records retained for accounting/dispute resolution
- **Confidence:** MEDIUM (75%)

---

### Data Asset 5: Driver Identity and Background Check Data

**Type:** PII / Sensitive Personal Information

**Description:** Identity verification and background check information for drivers

**Components:**
- Driver's license number
- Vehicle information (make, model, license plate)
- Insurance policy details
- Vehicle registration
- Background check results (criminal records, driving history via Checkr)
- SSN or equivalent (likely required by Checkr, not explicitly documented)

**Source:** Drivers table (data-model.md, lines 49-55); Driver onboarding (user-stories.md, lines 42-45); Checkr integration (third-party-integrations.md, lines 63-73); Driver/merchant documents (data-model.md, line 115)

**Sensitivity Classification:** RESTRICTED

**Basis:** Highly sensitive identity documents; background check data regulated; SSN is protected under multiple laws

**Confidence:** HIGH (90%)

**Regulatory Considerations:**
- **FCRA (Fair Credit Reporting Act):** Applicable - Background checks for employment
  - **Justification:** Checkr background checks subject to FCRA requirements
  - **Requirements:** Adverse action procedures, candidate rights notification
- **GDPR:** Applicable - Special category data (criminal records under Article 10)
  - **Requirements:** Enhanced protections for criminal record data
- **State ID Protection Laws:** Applicable - Driver's license numbers are protected PII
- **Data Breach Notification:** HIGH priority - Identity document breaches require notification

**Storage Locations:**
- **PostgreSQL `drivers` table:** license_number, vehicle_info, status (data-model.md, lines 49-55)
- **S3:** Scanned documents (license, insurance, registration) (data-model.md, line 115)
- **Checkr (external):** Background check details and results

**Transmission Paths:**
- **Driver App → Backend API:** License info, vehicle details
- **Driver App → S3:** Document uploads (likely via backend pre-signed URLs)
- **Backend API → Checkr:** Background check initiation
- **Checkr → Backend API (webhook):** Check results

**Retention Requirements:**
- **Documented:** Not specified
- **FCRA Requirement:** Background check records must be retained for compliance with adverse action procedures
- **Assumption:** Driver documents retained as long as driver account is active; may need retention post-termination for legal/compliance purposes
- **Confidence:** LOW (60%) - Regulatory requirements suggest retention policies needed

---

### Data Asset 6: Merchant Business Information

**Type:** Business Data / PII (for sole proprietors)

**Description:** Business and operational information for merchant partners

**Components:**
- Business name, business type
- Business license number
- Business address and geolocation
- Operating hours, delivery area
- Commission rate
- Rating and total reviews
- Bank account information (stored by Stripe as Connected Accounts)

**Source:** Merchants table (data-model.md, lines 23-29); Merchant onboarding (user-stories.md, lines 70-73)

**Sensitivity Classification:** CONFIDENTIAL

**Basis:** Business information may be proprietary; business licenses and financial arrangements are sensitive

**Confidence:** HIGH (90%)

**Regulatory Considerations:**
- **GDPR:** Applicable if sole proprietor (business owner is an individual)
  - **Justification:** Sole proprietor data is personal data
- **Business Confidentiality:** Commission rates and financial arrangements may be subject to NDAs
- **Tax Reporting:** Financial data (payouts) may be subject to 1099 reporting (US) or equivalent

**Storage Locations:**
- **PostgreSQL `merchants` table:** Business info, address, rates, status (data-model.md, lines 23-29)
- **S3:** Business licenses, permits (data-model.md, line 115)
- **Stripe Connected Accounts:** Bank account information (external)

**Transmission Paths:**
- **Merchant Portal → Backend API:** Business profile management
- **Backend API → PostgreSQL:** Storage
- **Backend API → Stripe:** Connected account setup for payouts

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Business records retained for duration of partnership and potentially longer for financial/legal compliance
- **Confidence:** MEDIUM (70%)

---

### Data Asset 7: Order Transaction Data

**Type:** Business Data / Transaction Records

**Description:** Complete order lifecycle information

**Components:**
- Order number (unique identifier)
- Customer, merchant, and driver IDs (foreign keys)
- Order items with quantities and modifiers
- Pricing breakdown (subtotal, tax, delivery fee, tip, total)
- Delivery address reference
- Order status and timestamps
- Payment status and Stripe payment intent ID
- Reviews and ratings

**Source:** Orders table (data-model.md, lines 56-65); Order_items table (data-model.md, lines 67-69); Reviews table (data-model.md, lines 74-78)

**Sensitivity Classification:** INTERNAL

**Basis:** Business-critical operational data; contains references to personal data but not directly sensitive on its own; required for service operation

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **GDPR:** Applicable - Order history linked to personal data (customer PII)
  - **Right to Access:** Customers can request order history
  - **Right to Erasure:** Complex due to financial record retention requirements
- **Financial Record Retention:** Tax and accounting regulations may require retention (typically 7 years in US)
- **Dispute Resolution:** Order records needed for customer complaints and refunds

**Storage Locations:**
- **PostgreSQL `orders` table:** Order metadata and status (data-model.md, lines 56-65)
- **PostgreSQL `order_items` table:** Line item details (data-model.md, lines 67-69)
- **PostgreSQL `order_item_modifiers` table:** Customizations (data-model.md, lines 71-73)
- **PostgreSQL `reviews` table:** Ratings and comments (data-model.md, lines 74-78)

**Transmission Paths:**
- **Customer App → Backend API:** Order creation
- **Backend API → Merchant Portal (WebSocket):** New order notification
- **Backend API → Driver App:** Delivery request assignment
- **Backend API → Customer App (WebSocket):** Order status updates

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Order history retained indefinitely for business analytics and customer convenience; financial regulations may mandate minimum retention periods
- **Confidence:** MEDIUM (70%)

---

### Data Asset 8: Menu and Pricing Data

**Type:** Business Data

**Description:** Merchant menu items, categories, pricing, and modifiers

**Components:**
- Menu categories and display order
- Menu items (name, description, price)
- Item photos (S3 URLs)
- Modifiers and modifier options with price adjustments
- Item availability flags

**Source:** Menu tables (data-model.md, lines 31-47); Menu management (user-stories.md, lines 75-80)

**Sensitivity Classification:** INTERNAL

**Basis:** Business data with competitive value; pricing may be confidential to merchants

**Confidence:** HIGH (95%)

**Regulatory Considerations:**
- **None directly applicable:** Menu data is generally not regulated
- **Business Confidentiality:** Merchants may consider pricing proprietary
- **Consumer Protection:** Pricing must be accurate and transparent (various consumer protection laws)

**Storage Locations:**
- **PostgreSQL:** `menu_categories`, `menu_items`, `item_modifiers`, `modifier_options` tables (data-model.md, lines 31-47)
- **S3:** Menu item photos (data-model.md, line 113)
- **Redis cache:** `menu:{merchant_id}` for performance (data-model.md, line 106)

**Transmission Paths:**
- **Merchant Portal → Backend API:** Menu management
- **Backend API → PostgreSQL:** Persistent storage
- **Backend API → Redis:** Caching
- **Backend API → Customer App:** Menu browsing

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Current menu data retained as long as merchant active; historical pricing may be retained for order history integrity
- **Confidence:** MEDIUM (75%)

---

### Data Asset 9: Promotional and Discount Data

**Type:** Business Data

**Description:** Promo codes and subscription information

**Components:**
- **Promo codes:** Code string, discount type/value, validity period, usage limits
- **Subscriptions:** QuickDeliver Plus memberships, status, billing cycle, Stripe subscription ID

**Source:** Promotions table (data-model.md, lines 80-85); Subscriptions table (data-model.md, lines 86-91); Subscription features (user-stories.md, lines 32-36)

**Sensitivity Classification:** INTERNAL

**Basis:** Business-sensitive marketing data; promo codes may be targeted and not for public distribution

**Confidence:** HIGH (90%)

**Regulatory Considerations:**
- **Consumer Protection:** Promo terms must be clear and enforceable
- **Tax Implications:** Discounts affect transaction taxable amounts
- **GDPR:** Subscription data linked to user PII

**Storage Locations:**
- **PostgreSQL `promotions` table:** Promo code details (data-model.md, lines 80-85)
- **PostgreSQL `subscriptions` table:** Membership status (data-model.md, lines 86-91)
- **Stripe (external):** Subscription billing management

**Transmission Paths:**
- **Customer App → Backend API:** Promo code application, subscription management
- **Admin Portal → Backend API:** Promo code creation
- **Backend API → Stripe:** Subscription creation/cancellation

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Active promos and subscriptions retained; expired promos may be archived or deleted
- **Confidence:** MEDIUM (70%)

---

### Data Asset 10: Earnings and Payout Data

**Type:** Financial Data

**Description:** Driver and merchant earnings, payout history, and performance metrics

**Components:**
- Real-time earnings tracking for drivers
- Payout records (amount, status, period, Stripe transfer ID)
- Driver performance stats (rating, acceptance rate, total deliveries)
- Merchant sales analytics

**Source:** Payouts table (data-model.md, lines 93-97); Driver earnings features (user-stories.md, lines 57-65); Merchant analytics (user-stories.md, lines 87-91)

**Sensitivity Classification:** CONFIDENTIAL

**Basis:** Financial information revealing income patterns; privacy-sensitive for drivers/merchants

**Confidence:** HIGH (90%)

**Regulatory Considerations:**
- **Tax Reporting:** Payouts may trigger 1099/tax reporting requirements (US) or equivalent
  - **Threshold:** Typically $600+ annual earnings in US
- **GDPR:** Applicable - Financial data linked to personal information
- **Labor Law:** Driver earnings may be relevant to independent contractor vs. employee classification

**Storage Locations:**
- **PostgreSQL `payouts` table:** Payout history (data-model.md, lines 93-97)
- **PostgreSQL `drivers` table:** Performance stats (data-model.md, line 54)
- **Backend services:** Real-time earnings calculations (not persistently stored in separate table)

**Transmission Paths:**
- **Backend API → Driver/Merchant Apps:** Earnings display
- **Backend API → Stripe:** Payout initiation (Connected Accounts transfers)
- **Stripe → Driver/Merchant Bank Accounts:** Actual funds transfer

**Retention Requirements:**
- **Documented:** Not specified
- **Tax Reporting Requirement:** Earnings records must be retained for tax purposes (typically 7 years in US)
- **Assumption:** Payout history retained indefinitely for financial compliance
- **Confidence:** MEDIUM (75%)

---

### Data Asset 11: Communication and Notification Data

**Type:** Communication Metadata

**Description:** Messages, notifications, and communication logs

**Components:**
- SMS content (verification codes, order notifications)
- Push notification payloads
- Phone call logs (masked numbers for customer-driver calls)
- Email notifications (if implemented)

**Source:** Twilio integration (third-party-integrations.md, lines 17-29); Firebase notifications (third-party-integrations.md, lines 48-60)

**Sensitivity Classification:** INTERNAL

**Basis:** Communication metadata reveals usage patterns; notification content may contain order details

**Confidence:** MEDIUM (75%) - Notification content not fully documented

**Regulatory Considerations:**
- **GDPR:** Communication metadata is personal data (Article 4.1)
- **Telecommunications Privacy:** SMS and call logs may be subject to telecom privacy laws
- **TCPA (US):** SMS/call notifications require consent

**Storage Locations:**
- **Twilio (external):** SMS and call logs
- **Firebase (external):** Notification delivery logs
- **QuickDeliver Backend:** Unclear if notification history is persisted (not documented)

**Transmission Paths:**
- **Backend API → Twilio:** SMS sending
- **Backend API → Firebase:** Push notification sending
- **Twilio → User phones:** SMS delivery
- **Firebase → Mobile apps:** Push notification delivery

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Communication logs retained by third-party services per their policies; QuickDeliver may not persist notification history
- **Confidence:** LOW (60%) - Notification logging architecture not documented

---

### Data Asset 12: Delivery Proof Photos

**Type:** Evidence / Media

**Description:** Photos taken by drivers as proof of delivery

**Components:**
- Photos of delivered orders at customer doorstep
- Associated metadata (timestamp, driver ID, order ID, GPS coordinates potentially)

**Source:** "Take photo of delivery" (user-stories.md, line 54); Delivery proof photos in S3 (data-model.md, line 114)

**Sensitivity Classification:** CONFIDENTIAL

**Basis:** Photos may inadvertently capture private property, individuals, or sensitive information

**Confidence:** HIGH (90%)

**Regulatory Considerations:**
- **GDPR:** Photos of individuals are personal data (if people are identifiable)
  - **Basis:** Doorstep photos may capture individuals or property details
- **Privacy Law:** Photography of private property without explicit consent may raise privacy issues in some jurisdictions
- **Dispute Resolution:** Photos serve as evidence for delivery disputes

**Storage Locations:**
- **S3:** Delivery proof photos (data-model.md, line 114)
- **Database reference:** Likely order record links to S3 URL (not explicitly documented in schema)

**Transmission Paths:**
- **Driver App → Backend API → S3:** Photo upload after delivery

**Retention Requirements:**
- **Documented:** Not specified
- **Assumption:** Retained for dispute resolution period (30-90 days typical); may be deleted after dispute window closes
- **Recommendation:** Implement retention policy to minimize privacy risk
- **Confidence:** LOW (60%) - Retention policy not documented

---

## 7. Analysis Scope

### 7.1 In-Scope Components

#### 1. Customer Mobile Application (React Native)
- **Justification:** Primary user interface handling PII, payment tokens, and location data; crosses trust boundaries from untrusted client to backend
- **Security Relevance:** Authentication, data storage, API communication security, payment tokenization
- **Documentation Quality:** Excellent - Features comprehensively documented

#### 2. Driver Mobile Application (React Native)
- **Justification:** Handles sensitive location tracking (GPS every 5 seconds), driver PII, earnings data; unique privacy concerns
- **Security Relevance:** Background location tracking, photo uploads, real-time communication, driver surveillance implications
- **Documentation Quality:** Excellent - Features and workflows well-documented

#### 3. Merchant Web Portal (React)
- **Justification:** Business-critical interface for order management and menu configuration; handles merchant financial data
- **Security Relevance:** Authentication, authorization (merchant can only access own data), business data protection
- **Documentation Quality:** Excellent - Functionality documented via API and user stories

#### 4. Admin Web Portal (React)
- **Justification:** Highest privilege level with system-wide access; critical for privilege escalation threat analysis
- **Security Relevance:** Admin authentication, authorization enforcement, audit logging, privileged operations
- **Documentation Quality:** Good - API endpoints documented, UI workflows less detailed

#### 5. Backend API Services (Node.js/Express)
- **Justification:** Core business logic layer; handles authentication, authorization, data validation; orchestrates all system operations
- **Security Relevance:** Input validation, SQL injection prevention, authentication/authorization logic, API security, rate limiting
- **Documentation Quality:** Excellent - Services and endpoints comprehensively documented

#### 6. PostgreSQL Database (AWS RDS)
- **Justification:** Stores all sensitive data (credentials, PII, financial records); primary data protection target
- **Security Relevance:** Data-at-rest encryption, access controls, SQL injection (via backend), backup security
- **Documentation Quality:** Excellent - Complete schema documented

#### 7. Redis Cache (AWS ElastiCache)
- **Justification:** Stores JWT sessions and real-time driver locations; compromise enables session hijacking
- **Security Relevance:** Session security, cache poisoning, data-in-transit encryption
- **Documentation Quality:** Good - Cache keys and usage documented

#### 8. AWS S3 Storage
- **Justification:** Stores identity documents (licenses, insurance), delivery photos; contains highly sensitive PII
- **Security Relevance:** Access controls, encryption at rest, public vs. private bucket configuration, pre-signed URL security
- **Documentation Quality:** Good - File types documented, access patterns less detailed

#### 9. API Gateway / Load Balancer (AWS ALB)
- **Justification:** Entry point for all external traffic; enforces HTTPS; potential DDoS target
- **Security Relevance:** TLS termination, DDoS protection, rate limiting, WAF integration
- **Documentation Quality:** Limited - Component type documented, security configuration not specified

#### 10. WebSocket Server (Real-Time Tracking)
- **Justification:** Persistent connections for location streaming; different threat model than REST API
- **Security Relevance:** WebSocket authentication, authorization per connection, event injection, location data privacy
- **Documentation Quality:** Good - WebSocket events documented

#### 11. Third-Party Integrations (Stripe, Google Maps, Twilio, Firebase, Checkr)
- **Justification:** External trust boundaries; handle sensitive data (payments, location, PII); webhook security critical
- **Security Relevance:** API key management, webhook signature verification, data transmission security, third-party risk
- **Documentation Quality:** Excellent - Integration purposes and data flows documented

### 7.2 Out-of-Scope Components

#### 1. AWS Infrastructure Platform (ECS, EC2, VPC, IAM)
- **Justification:** Infrastructure-as-a-Service; AWS responsible for underlying platform security; configuration review would require infrastructure-as-code artifacts not provided
- **Impact on Analysis:** Assumes AWS best practices followed (VPC network isolation, IAM least privilege, security groups); will document as assumptions
- **Dependencies:** Backend services rely on proper AWS IAM role configuration; S3 buckets rely on proper bucket policies

#### 2. CI/CD Pipeline (GitHub Actions)
- **Justification:** Deployment tooling; supply chain security important but distinct threat model from runtime application security
- **Impact on Analysis:** Assumes secure deployment practices; will note as documentation gap if deployment security relevant to runtime threats
- **Dependencies:** Application security depends on secure deployment (no credential leaks, signed containers)

#### 3. Monitoring and Logging Infrastructure
- **Justification:** Not specified in documentation; operational tooling rather than application functionality
- **Impact on Analysis:** Logging is critical for incident detection and response; will document as gap and recommend implementation
- **Dependencies:** Security monitoring depends on comprehensive logging (authentication events, authorization failures, suspicious patterns)

#### 4. Stripe Internal Systems
- **Justification:** Third-party service; Stripe responsible for internal security; QuickDeliver's responsibility limited to integration security
- **Impact on Analysis:** Will analyze Stripe integration points (API keys, webhooks) but not Stripe's internal architecture
- **Dependencies:** Payment security depends on Stripe's PCI-compliant infrastructure

#### 5. Google Maps, Twilio, Firebase, Checkr Internal Systems
- **Justification:** Same rationale as Stripe; third-party responsibility
- **Impact on Analysis:** Focus on integration security (API keys, data transmitted, webhook verification)
- **Dependencies:** Service availability and security depends on third-party providers

#### 6. End-User Devices (iOS/Android devices, web browsers)
- **Justification:** User-controlled environments; application has limited control over device security
- **Impact on Analysis:** Will consider mobile app security controls (certificate pinning, jailbreak detection) but not device-level threats (malware, keyloggers)
- **Dependencies:** Application security assumes users take basic device precautions (OS updates, lock screens)

#### 7. Network Infrastructure Between Components (AWS internal networking)
- **Justification:** AWS managed networking; VPC security groups and network ACLs managed at infrastructure level
- **Impact on Analysis:** Will assume network segmentation best practices; document encryption-in-transit requirements
- **Dependencies:** East-west traffic security depends on AWS VPC configuration

### 7.3 Scope Boundaries Rationale

**Inclusion Criteria Applied:**
- Component is part of QuickDeliver application code or configuration
- Component handles sensitive data (PII, credentials, payment, location)
- Component crosses trust boundaries (client-server, user roles, external integrations)
- Component functionality sufficiently documented for threat analysis

**Exclusion Criteria Applied:**
- Infrastructure managed by AWS or third-party providers (below application layer)
- Tooling infrastructure (CI/CD, monitoring) with separate threat model
- End-user controlled environments (devices, networks)
- Insufficient documentation for meaningful analysis

**Gray Areas:**
- **AWS Services (RDS, ElastiCache, S3):** INCLUDED because configuration impacts application security (encryption, access controls)
- **Load Balancer:** INCLUDED because it's the entry point and TLS termination point
- **Monitoring/Logging:** EXCLUDED but documented as critical gap
- **OAuth Providers (Google/Apple/Facebook):** EXCLUDED except for integration callback security

### 7.4 Analysis Focus Areas

Based on in-scope components and data assets, the threat modeling analysis will prioritize:

1. **Authentication and Authorization:** Multi-role system with different privilege levels; JWT token security; OAuth integration
2. **Data Protection:** Encryption in transit and at rest for PII, payment, location, identity documents
3. **Payment Security:** PCI-DSS scope boundaries; Stripe integration security; webhook verification
4. **Location Privacy:** Real-time driver tracking; customer address protection; surveillance implications
5. **API Security:** Input validation, injection attacks, rate limiting, authorization enforcement
6. **Third-Party Integration Security:** API key management, webhook signature verification, data minimization
7. **Mobile App Security:** Secure storage, certificate pinning, reverse engineering protection
8. **Real-Time Communication Security:** WebSocket authentication, authorization, event injection

## 8. Assumptions & Constraints

### Assumption 1: HTTPS/TLS Encryption for All API Communications

**Category:** Security / Network

**Assumption Statement:** All client-to-server API communications occur over HTTPS/TLS 1.2 or higher

**Basis for Assumption:**
- **Evidence:** API base URL documented as `https://api.quickdeliver.com/v1` (api-endpoints.md, line 3)
- **Evidence:** WebSocket URL documented as `wss://ws.quickdeliver.com` (api-endpoints.md, line 159)
- **Reasoning:** Modern web applications default to HTTPS; documented URLs use https:// and wss:// schemes

**Confidence Level:** MEDIUM (80%)

**Rationale:** URLs suggest HTTPS/WSS, but TLS version, cipher suites, and certificate validation are not documented

**Alternative Interpretations:**
1. **HTTP also supported:** Load balancer might accept both HTTP and HTTPS, with HTTP not explicitly disabled
   - **Implications:** Downgrade attacks possible; credentials transmitted in plaintext if HTTP used
2. **TLS misconfiguration:** Outdated TLS versions (1.0, 1.1) or weak ciphers might be enabled
   - **Implications:** Protocol downgrade attacks, cryptographic weaknesses

**Impact if Assumption Incorrect:**
- **Technical Impact:** All data in transit (credentials, PII, payment tokens, location) exposed to interception
- **Risk Impact:** Information Disclosure and Tampering threats become HIGH severity; credential theft enabled
- **Mitigation Impact:** Encryption-in-transit controls become CRITICAL priority

**Validation Recommendation:**
- **Recommended Action:** Verify load balancer TLS configuration; confirm HTTP-to-HTTPS redirect enforced
- **Information Needed:** AWS ALB listener configuration, TLS policy settings, HSTS header implementation
- **Testing:** Attempt HTTP connection to API endpoints; check TLS version negotiation

---

### Assumption 2: Authorization Enforcement at API Layer

**Category:** Security / Authorization

**Assumption Statement:** Backend API enforces role-based authorization, preventing users from accessing resources belonging to other users or accessing operations outside their role

**Basis for Assumption:**
- **Evidence:** Separate API endpoint namespaces for roles: `/drivers/*`, `/merchants/me/*`, `/admin/*` (api-endpoints.md)
- **Evidence:** User role field in database (data-model.md, line 7)
- **Reasoning:** API structure suggests role-based access control; common pattern for multi-tenant systems

**Confidence Level:** MEDIUM (75%)

**Rationale:** API design implies authorization, but enforcement mechanism not documented; no mention of authorization middleware or checks

**Alternative Interpretations:**
1. **Authorization gaps:** Some endpoints may lack proper authorization checks (e.g., IDOR vulnerabilities)
   - **Implications:** Customer A could access Customer B's orders; drivers could view other drivers' earnings
2. **Client-side authorization only:** Role checks performed in mobile apps/web portals but not enforced server-side
   - **Implications:** API manipulation allows privilege escalation and unauthorized data access

**Impact if Assumption Incorrect:**
- **Technical Impact:** Broken Access Control (OWASP #1); massive data breach potential
- **Risk Impact:** Information Disclosure, Tampering, and Elevation of Privilege threats become CRITICAL
- **Mitigation Impact:** Authorization controls become top priority; comprehensive review required

**Validation Recommendation:**
- **Recommended Action:** Review authorization middleware implementation; perform IDOR testing; verify token role claims checked
- **Information Needed:** Authorization code review, authentication/authorization architecture documentation
- **Testing:** Attempt cross-user resource access (e.g., customer accessing another customer's order via ID manipulation)

---

### Assumption 3: Password Hashing with Strong Algorithm

**Category:** Security / Cryptography

**Assumption Statement:** User passwords are hashed using a strong, modern algorithm (bcrypt, scrypt, or Argon2) with appropriate work factors

**Basis for Assumption:**
- **Evidence:** Database stores `password_hash` not `password` (data-model.md, line 6)
- **Reasoning:** Modern Node.js applications typically use bcrypt; explicit `password_hash` naming suggests proper hashing
- **Industry Standard:** Password hashing is a fundamental security control

**Confidence Level:** MEDIUM (75%)

**Rationale:** Database schema suggests hashing (not plaintext or reversible encryption), but algorithm not specified

**Alternative Interpretations:**
1. **Weak hashing:** Older algorithms like MD5 or SHA-1 without salt
   - **Implications:** Password database compromises allow rapid brute-force cracking
2. **Insufficient work factor:** bcrypt with low rounds (< 10) vulnerable to modern GPU cracking
   - **Implications:** Reduced but still present brute-force vulnerability

**Impact if Assumption Incorrect:**
- **Technical Impact:** Credential compromise on database breach; mass account takeovers
- **Risk Impact:** Information Disclosure severity increased; credential stuffing attacks more effective
- **Mitigation Impact:** Password policy and hashing algorithm upgrade become urgent priorities

**Validation Recommendation:**
- **Recommended Action:** Review password hashing implementation in authentication code
- **Information Needed:** Authentication module code, password hashing library and configuration
- **Testing:** Code review of user registration and authentication functions

---

### Assumption 4: JWT Token Signature Verification

**Category:** Security / Authentication

**Assumption Statement:** Backend API verifies JWT token signatures on every authenticated request, preventing token forgery

**Basis for Assumption:**
- **Evidence:** JWT tokens used for authentication (architecture-overview.md, line 24)
- **Evidence:** All endpoints require Authorization header except public ones (api-endpoints.md, line 5)
- **Reasoning:** JWT signature verification is fundamental to JWT security; assumed as standard practice

**Confidence Level:** MEDIUM (75%)

**Rationale:** JWT usage documented, but implementation details (signing algorithm, key management, verification enforcement) not specified

**Alternative Interpretations:**
1. **No signature verification:** Tokens accepted without validation (none algorithm vulnerability)
   - **Implications:** Attackers can forge tokens with arbitrary claims; complete authentication bypass
2. **Weak signing:** HS256 with exposed secret or predictable key
   - **Implications:** Token forgery possible if secret compromised

**Impact if Assumption Incorrect:**
- **Technical Impact:** Complete authentication bypass; arbitrary user impersonation
- **Risk Impact:** Spoofing, Tampering, and Elevation of Privilege threats become CRITICAL
- **Mitigation Impact:** Authentication system requires immediate remediation

**Validation Recommendation:**
- **Recommended Action:** Review JWT middleware implementation; verify signature algorithm (prefer RS256 over HS256)
- **Information Needed:** JWT library configuration, signing key management, verification enforcement code
- **Testing:** Attempt to use unsigned JWT (alg: none) or JWT with invalid signature

---

### Assumption 5: AWS Security Best Practices Followed

**Category:** Infrastructure / Cloud Configuration

**Assumption Statement:** AWS resources configured following security best practices (VPC isolation, security groups, IAM least privilege, encryption at rest for RDS/S3)

**Basis for Assumption:**
- **Evidence:** AWS services documented (RDS, ElastiCache, S3, ECS, ALB) (architecture-overview.md, third-party-integrations.md)
- **Reasoning:** AWS recommends security configurations; managed services encourage best practices
- **Industry Standard:** Cloud security frameworks (AWS Well-Architected) widely adopted

**Confidence Level:** LOW (60%)

**Rationale:** AWS usage documented but no infrastructure configuration details provided; assumes best practices without evidence

**Alternative Interpretations:**
1. **Overly permissive configuration:** S3 buckets publicly readable, RDS publicly accessible, wide-open security groups
   - **Implications:** Data exposure, unauthorized database access, lateral movement
2. **No encryption at rest:** RDS and S3 encryption not enabled
   - **Implications:** Data breach severity increased if physical media or backups compromised

**Impact if Assumption Incorrect:**
- **Technical Impact:** Infrastructure-level vulnerabilities; defense-in-depth failures
- **Risk Impact:** Information Disclosure, Denial of Service threats elevated
- **Mitigation Impact:** Infrastructure hardening becomes priority; comprehensive AWS security review required

**Validation Recommendation:**
- **Recommended Action:** Conduct AWS infrastructure security review; review Terraform/CloudFormation templates
- **Information Needed:** Infrastructure-as-code configurations, AWS account security audit
- **Testing:** AWS Config rules evaluation, S3 bucket policy review, RDS public accessibility check

---

### Assumption 6: Input Validation and SQL Injection Prevention

**Category:** Security / Data Validation

**Assumption Statement:** Backend API performs comprehensive input validation and uses parameterized queries (or ORM) to prevent SQL injection

**Basis for Assumption:**
- **Evidence:** Node.js with Express framework (architecture-overview.md, line 22)
- **Reasoning:** Modern Node.js ORMs (Sequelize, TypeORM, Prisma) provide SQL injection protection by default
- **Industry Standard:** Input validation and parameterized queries are fundamental controls

**Confidence Level:** MEDIUM (70%)

**Rationale:** Technology stack suggests modern practices, but implementation details not documented

**Alternative Interpretations:**
1. **Raw SQL queries:** String concatenation used instead of parameterized queries
   - **Implications:** SQL injection vulnerabilities enabling data exfiltration and tampering
2. **Insufficient input validation:** User inputs not sanitized, allowing injection attacks (SQL, NoSQL, command injection)
   - **Implications:** Multiple injection vulnerability classes present

**Impact if Assumption Incorrect:**
- **Technical Impact:** Injection vulnerabilities (OWASP #3); database compromise
- **Risk Impact:** Tampering, Information Disclosure, Elevation of Privilege threats become HIGH/CRITICAL
- **Mitigation Impact:** Comprehensive code review and remediation required; input validation framework needed

**Validation Recommendation:**
- **Recommended Action:** Review database query implementation; identify ORM/query builder usage
- **Information Needed:** Database access layer code, ORM configuration, input validation middleware
- **Testing:** SQL injection testing on all API endpoints accepting user input

---

### Assumption 7: API Rate Limiting Implemented

**Category:** Security / Availability

**Assumption Statement:** API endpoints have rate limiting to prevent brute-force attacks and DoS

**Basis for Assumption:**
- **Evidence:** None directly documented
- **Reasoning:** High-traffic consumer applications typically implement rate limiting for stability and security
- **Industry Standard:** Rate limiting is a common API security control

**Confidence Level:** LOW (50%)

**Rationale:** Not documented; assuming based on typical application patterns; could be absent

**Alternative Interpretations:**
1. **No rate limiting:** All endpoints accept unlimited requests
   - **Implications:** Brute-force attacks on authentication, credential stuffing, API abuse, DoS
2. **Inadequate limits:** Rate limits set too high to prevent attacks
   - **Implications:** Reduced but still present abuse potential

**Impact if Assumption Incorrect:**
- **Technical Impact:** Brute-force and DoS vulnerabilities
- **Risk Impact:** Denial of Service threats elevated; Spoofing (via credential brute-force) enabled
- **Mitigation Impact:** Rate limiting becomes priority; WAF rules or application-layer limiting required

**Validation Recommendation:**
- **Recommended Action:** Review API middleware for rate limiting; check ALB/WAF configuration
- **Information Needed:** Express middleware stack, AWS WAF rules, CloudFront rate limit policies
- **Testing:** Rapid-fire API requests to test for rate limiting enforcement

---

### Assumption 8: Secure Mobile App Data Storage

**Category:** Security / Mobile

**Assumption Statement:** Mobile apps store sensitive data (tokens, credentials) using platform secure storage (iOS Keychain, Android KeyStore)

**Basis for Assumption:**
- **Evidence:** React Native framework documented (architecture-overview.md, line 16)
- **Reasoning:** React Native security libraries (react-native-keychain) provide secure storage; standard practice for mobile apps
- **Industry Standard:** Mobile app security guidelines require secure credential storage

**Confidence Level:** MEDIUM (70%)

**Rationale:** Technology stack supports secure storage, but implementation not documented

**Alternative Interpretations:**
1. **Insecure storage:** Tokens stored in AsyncStorage (plaintext) instead of secure storage
   - **Implications:** Device compromise or app reverse engineering exposes credentials
2. **No certificate pinning:** Mobile apps don't validate server certificate
   - **Implications:** Man-in-the-middle attacks possible despite HTTPS

**Impact if Assumption Incorrect:**
- **Technical Impact:** Mobile app security vulnerabilities; credential theft via device access
- **Risk Impact:** Information Disclosure, Spoofing threats elevated for mobile users
- **Mitigation Impact:** Mobile app security hardening required; secure storage migration needed

**Validation Recommendation:**
- **Recommended Action:** Review React Native app code for secure storage library usage
- **Information Needed:** Mobile app authentication module code, dependencies (react-native-keychain)
- **Testing:** Static analysis of mobile app binary, runtime inspection of data storage locations

---

### Assumption 9: Webhook Signature Verification for Third-Party Callbacks

**Category:** Security / Integration

**Assumption Statement:** Backend verifies webhook signatures from Stripe and Checkr to prevent webhook spoofing

**Basis for Assumption:**
- **Evidence:** Stripe and Checkr send webhook notifications (third-party-integrations.md, lines 14, 72)
- **Reasoning:** Webhook signature verification is documented best practice for these services
- **Industry Standard:** Webhook security requires signature validation

**Confidence Level:** MEDIUM (65%)

**Rationale:** Webhooks documented, but verification implementation not specified

**Alternative Interpretations:**
1. **No signature verification:** Webhooks accepted without validation
   - **Implications:** Attackers can spoof webhooks to manipulate payment status or approve drivers without background checks
2. **Weak verification:** Signatures checked but secrets stored insecurely
   - **Implications:** Signature bypass if secrets compromised

**Impact if Assumption Incorrect:**
- **Technical Impact:** Payment manipulation, background check bypass, business logic tampering
- **Risk Impact:** Tampering and Elevation of Privilege threats become HIGH severity
- **Mitigation Impact:** Webhook verification becomes critical; comprehensive audit of webhook handlers required

**Validation Recommendation:**
- **Recommended Action:** Review webhook handler code for signature verification implementation
- **Information Needed:** Stripe and Checkr webhook handler implementations, secret management
- **Testing:** Send test webhooks without valid signatures to verify rejection

---

### Assumption 10: Operational Scale is MVP/Small Deployment

**Category:** Operational / Business

**Assumption Statement:** System currently operating at or below Phase 1 targets (2 cities, 1,000 orders/day, hundreds of users)

**Basis for Assumption:**
- **Evidence:** Phase 1 MVP targets documented (product-roadmap.md, lines 18-21)
- **Reasoning:** Documentation describes launch plan; implies system not yet at scale phases 2-3
- **Industry Standard:** Startup platforms typically launch in limited markets before scaling

**Confidence Level:** MEDIUM (70%)

**Rationale:** Roadmap suggests phased growth; actual current state not documented

**Alternative Interpretations:**
1. **Already at scale:** System operating at Phase 2/3 levels (50k-200k orders/day)
   - **Implications:** Scalability and DoS risks more severe; incident impact affects more users
2. **Pre-launch:** System not yet in production
   - **Implications:** Threat model is predictive rather than current-state analysis

**Impact if Assumption Incorrect:**
- **Technical Impact:** Scale affects DoS threat severity and business impact calculations
- **Risk Impact:** Business impact assessments may be significantly underestimated
- **Mitigation Impact:** Scalability and availability controls priority affected by scale

**Validation Recommendation:**
- **Recommended Action:** Clarify current operational status (pre-launch, Phase 1, or scaled)
- **Information Needed:** Current user counts, daily order volume, geographic deployment
- **Note:** In Automatic Mode, will use conservative assumptions for risk assessment (assume Phase 1 scale)

---

### Constraint 1: Automatic Mode - Limited User Clarification

**Category:** Methodological

**Description:** Threat modeling conducted in Automatic Mode without user clarification during analysis

**Implications:**
- Cannot resolve ambiguities through stakeholder questions
- Must make reasonable assumptions where documentation gaps exist
- Risk assessments may be more conservative due to uncertainty
- Some threat scenarios may have multiple interpretations without decisive resolution

**Mitigation:**
- Document all assumptions with alternative interpretations
- Provide clear validation recommendations for assumption verification
- Use conservative risk assessments when in doubt
- Flag critical decisions requiring stakeholder input in final report

---

### Constraint 2: No Security-Specific Documentation Provided

**Category:** Documentation

**Description:** Source documentation focuses on functionality and architecture; security controls, threat models, and security requirements not explicitly documented

**Implications:**
- Security controls must be inferred from architecture and industry standards
- Cannot assess security posture against documented security requirements (none provided)
- Threat analysis is comprehensive for typical controls but cannot assess against organization-specific policies

**Mitigation:**
- Apply industry standard security frameworks (OWASP Top 10, STRIDE)
- Document where security controls are assumed vs. documented
- Recommend security documentation as output of this threat modeling process

---

### Constraint 3: Implementation Details Limited

**Category:** Documentation

**Description:** High-level architecture documented; code-level implementation details (libraries, frameworks, versions, configurations) not specified

**Implications:**
- Cannot perform version-specific vulnerability assessment
- Cannot assess configuration security (TLS settings, password hashing rounds, JWT algorithms)
- Threat analysis focuses on architectural threats rather than implementation-specific vulnerabilities

**Mitigation:**
- Recommend follow-up code review and configuration audit
- Focus threat modeling on design-level threats applicable regardless of implementation specifics
- Document implementation assumptions requiring validation

---

## 9. Documentation Gaps

### Critical Gaps (Potentially Blocking Analysis)

#### Gap 1: Security Controls and Architecture Not Documented

**Missing Information:** Authentication implementation details (JWT signing algorithm, key management), authorization enforcement mechanisms, encryption configurations (TLS versions, RDS/ElastiCache encryption), input validation frameworks

**Impact:** Cannot assess actual security posture; must assume industry best practices; cannot identify implementation-specific vulnerabilities; threat analysis limited to architectural level

**Blocks:** Detailed vulnerability assessment in Stages 3-4; specific mitigation recommendations in Stage 5

**Workaround:** Apply generic security threats (STRIDE); assume industry-standard controls; document assumptions requiring validation; recommend code review and configuration audit as follow-up

**Recommendation:** Obtain security architecture documentation, authentication/authorization implementation details, AWS infrastructure-as-code configurations, security control inventory

**Priority:** HIGH - Security control assumptions significantly impact threat model accuracy

---

#### Gap 2: Logging, Monitoring, and Incident Response Not Specified

**Missing Information:** Application logging framework, log aggregation/analysis, security monitoring (SIEM), alerting, incident response procedures, audit logging for privileged operations

**Impact:** Cannot assess detective and responsive security controls; threat analysis focuses on preventive controls only; incident detection and response capabilities unknown

**Blocks:** Complete security posture assessment; recommendations for security monitoring and alerting

**Workaround:** Assume logging and monitoring not implemented or insufficient; recommend comprehensive logging and monitoring as mitigation strategy

**Recommendation:** Obtain logging architecture, SIEM configuration (if exists), incident response playbooks, audit log specifications

**Priority:** HIGH - Logging and monitoring critical for detection and response; absence significantly increases risk

---

### Significant Gaps (Limiting Analysis Quality)

#### Gap 3: Network Architecture and Segmentation Not Detailed

**Missing Information:** VPC design, subnet structure, security groups, network ACLs, inter-component network paths, network segmentation between services

**Impact:** Cannot assess network-level isolation and segmentation; lateral movement threats difficult to evaluate; defense-in-depth analysis incomplete

**Affects:** Network-based threats (lateral movement, man-in-the-middle on internal networks); trust boundary analysis for internal components

**Workaround:** Assume standard AWS VPC best practices (public subnets for ALB, private subnets for ECS, isolated data layer); document as assumption

**Recommendation:** Obtain VPC design diagrams, security group rules, network architecture documentation

**Priority:** MEDIUM - Network segmentation important for defense-in-depth but less critical than application-layer controls for internet-facing services

---

#### Gap 4: Operational Security Procedures Not Documented

**Missing Information:** Secret management (API keys, database credentials, JWT signing keys), deployment procedures, access control for infrastructure, backup and recovery procedures, security patching process

**Impact:** Cannot assess operational security risks; secret exposure threats difficult to quantify; business continuity and disaster recovery assessment incomplete

**Affects:** Risk assessment for operational threats (insider threats, credential exposure, data loss); mitigation recommendations for operational controls

**Workaround:** Assume secrets stored in environment variables or AWS Secrets Manager (industry standard); recommend operational security best practices

**Recommendation:** Obtain secret management procedures, deployment automation documentation, infrastructure access controls, backup/recovery documentation

**Priority:** MEDIUM - Operational security important but outside core application threat model scope

---

#### Gap 5: Compliance Requirements and Security Policies Not Specified

**Missing Information:** Regulatory compliance targets (confirmed GDPR/CCPA scope, PCI-DSS evidence), organizational security policies, data retention policies, acceptable use policies, privacy policies

**Impact:** Cannot assess compliance posture; data retention recommendations lack policy basis; privacy threat analysis limited to generic privacy principles

**Affects:** Risk assessment (compliance violations), mitigation prioritization (compliance-driven controls), data handling recommendations

**Workaround:** Assume major regulations apply (GDPR if EU presence, PCI-DSS via Stripe, CCPA if California users); apply industry-standard privacy practices

**Recommendation:** Obtain compliance documentation, security policies, privacy policy, data retention policy, acceptable use policy

**Priority:** MEDIUM - Compliance critical for business but requirements can be inferred from data types and industry

---

### Minor Gaps (Documentation Enhancements)

#### Gap 6: Technology Versions and Dependencies Not Specified

**Missing Information:** Node.js version, Express version, PostgreSQL version, React Native version, specific libraries (ORM, JWT library, validation frameworks), dependency management

**Impact:** Cannot perform version-specific vulnerability assessment (CVE analysis); cannot assess dependency security; supply chain security analysis incomplete

**Enhancement:** Version-specific vulnerability scanning, dependency audit recommendations, supply chain risk assessment

**Priority:** LOW - Architectural threats independent of versions; version analysis typically part of separate vulnerability assessment process

---

#### Gap 7: Current Operational Status and Scale Unknown

**Missing Information:** Current deployment status (pre-launch, MVP, scaled), actual user counts, transaction volumes, geographic deployment, fleet metrics (driver/merchant counts)

**Impact:** Business impact assessments are qualitative rather than quantitative; cannot calculate financial impact of breaches; scale-dependent threats (DoS severity) difficult to assess

**Enhancement:** Quantitative risk assessment with specific financial impact calculations; tailored DoS mitigation based on actual traffic

**Priority:** LOW - Can proceed with qualitative risk assessment; scale assumptions documented (Phase 1 MVP assumed)

---

#### Gap 8: Mobile App Security Features Not Detailed

**Missing Information:** Certificate pinning implementation, jailbreak/root detection, reverse engineering protections (obfuscation, anti-tampering), secure coding practices

**Impact:** Mobile app threat assessment limited to generic threats; cannot validate specific mobile security controls

**Enhancement:** Detailed mobile app security assessment; specific mobile threat scenarios; mobile-specific mitigation recommendations

**Priority:** LOW - Generic mobile threats sufficient for threat model; detailed mobile security assessment typically separate from architecture threat modeling

---

#### Gap 9: Third-Party Integration Security Details Limited

**Missing Information:** API key storage and rotation procedures, webhook signature verification implementation, third-party service SLAs and security certifications, data processing agreements (DPAs)

**Impact:** Integration security assessment limited to generic recommendations; cannot validate actual implementation

**Enhancement:** Detailed integration security review; API key management audit; webhook handler security testing

**Priority:** LOW - Integration security principles clear; implementation verification separate activity

---

#### Gap 10: Error Handling and Information Disclosure Not Documented

**Missing Information:** Error handling strategy, error messages exposed to clients, stack traces in responses, debugging information leakage

**Impact:** Information disclosure threats difficult to assess; error handling security recommendations generic

**Enhancement:** Error handling security review; information leakage testing

**Priority:** LOW - Error handling best practices can be recommended generically; implementation testing separate from threat modeling

---

## 10. Confidence Assessment

### Overall Confidence: MEDIUM (75%)

The system understanding developed in Stage 1 is based on comprehensive functional and architectural documentation. Technology stack, business model, user workflows, data model, and third-party integrations are well-documented, providing high confidence in system functionality. However, security-specific implementation details are not documented, requiring assumptions about security controls. Overall confidence is MEDIUM - sufficient for architectural threat modeling but requiring validation for implementation-specific assessments.

---

### Confidence Breakdown by Category

#### Component Inventory: HIGH (88%)

**HIGH Confidence Elements (11 components):**
- Customer Mobile App, Driver Mobile App, Merchant Web Portal, Admin Web Portal: Features and workflows comprehensively documented
- Backend API Services: Service architecture and endpoints detailed
- PostgreSQL Database: Complete schema documented
- Redis Cache: Cache keys and usage specified
- S3 Storage: File types and purpose clear
- Stripe, Google Maps, Twilio, Firebase, Checkr integrations: Purposes and data flows documented

**MEDIUM Confidence Elements (3 components):**
- Load Balancer: Type documented but security configuration unknown
- WebSocket Server: Events documented but authentication/authorization details limited
- AWS Infrastructure: Services identified but configurations not specified

**LOW Confidence Elements:** None

**Rationale:** Core application components and their functionality are explicitly documented; infrastructure configuration details missing but components themselves clearly identified

---

#### Trust Boundaries: HIGH (85%)

**Well-Documented Boundaries (6 boundaries):**
- Public Internet ↔ Load Balancer: Clear architectural entry point
- Mobile Apps ↔ Backend: Client-server boundary explicit
- User Roles (Customer/Driver/Merchant/Admin): Role field and API structure clear
- Backend ↔ Third-Party APIs: Integrations documented
- WebSocket Connections: Separate protocol documented
- Driver App ↔ Location Services: GPS tracking explicit

**Inferred Boundaries (4 boundaries):**
- Authenticated ↔ Admin privilege: Admin endpoints suggest boundary
- Backend ↔ Database: Standard application-database separation
- Backend ↔ Redis: Caching layer separation
- Backend ↔ S3: Storage service boundary

**Ambiguous Boundaries:** None critical; all major trust transitions identified

**Rationale:** Architectural trust boundaries clear from component interactions; privilege boundaries evident from API structure and data model; security enforcement mechanisms not detailed but boundaries themselves well-defined

---

#### Data Assets: HIGH (90%)

**Explicitly Documented (8 assets):**
- User credentials: Authentication fields in database
- PII: User profile data specified
- Location data: Addresses and GPS tracking documented
- Payment information: Payment methods and Stripe integration clear
- Driver identity documents: Onboarding requirements explicit
- Merchant business information: Merchant profiles specified
- Order transaction data: Complete order schema documented
- Earnings and payout data: Payout tables and features documented

**Inferred from Context (4 assets):**
- Menu and pricing data: Menu schema complete
- Promotional/discount data: Promo and subscription tables documented
- Communication/notification data: Notification features described but logging unclear
- Delivery proof photos: Photo capture mentioned, storage implied

**Unknown Sensitivity:** None - all data types classifiable based on content

**Rationale:** Data model comprehensively documented; data flows clear from API specifications; sensitivity classification straightforward from data content and regulations

---

#### Security Controls: MEDIUM (65%)

**Documented Controls (3 controls):**
- HTTPS API URLs: https:// scheme in documentation
- JWT authentication: Token usage specified
- Stripe tokenization: Payment handling via Stripe SDK

**Inferred Controls (7 controls):**
- Password hashing: `password_hash` field suggests proper hashing
- Authorization: API structure and roles suggest RBAC
- TLS for databases/cache: AWS managed services encourage encryption
- S3 access controls: Document sensitivity requires access control
- WebSocket authentication: Token required on connection
- OAuth integration: Social login features documented
- Input validation: Modern framework suggests validation

**Unknown Controls:**
- Rate limiting, WAF, DDoS protection
- Logging and monitoring
- Audit logging
- Encryption at rest (RDS, ElastiCache, S3)
- Certificate pinning (mobile apps)
- Secret management
- Webhook signature verification

**Rationale:** Security controls must be inferred from architecture and industry standards; explicit security documentation absent; sufficient for threat identification but requires validation for accurate risk assessment

---

### Factors Limiting Confidence

1. **Security Implementation Gap (HIGH impact):** No security architecture documentation; must assume industry best practices for authentication, authorization, encryption, and input validation

2. **Configuration Unknown (MEDIUM impact):** AWS infrastructure configurations not specified; cannot validate encryption at rest, network segmentation, access controls

3. **Operational Security Not Documented (MEDIUM impact):** Secret management, deployment security, monitoring, and incident response procedures unknown

4. **Versions Not Specified (LOW impact):** Cannot perform CVE analysis or dependency vulnerability assessment

5. **Current Scale Unknown (LOW impact):** Business impact quantification limited; qualitative risk assessment required

---

### Recommendations for Improving Confidence

1. **Security Architecture Documentation (CRITICAL):**
   - Authentication and authorization implementation details
   - Encryption configurations (TLS, at-rest encryption for RDS/S3/ElastiCache)
   - Input validation framework and approach
   - Security control inventory

2. **Infrastructure-as-Code Review (HIGH):**
   - Terraform/CloudFormation templates for AWS resources
   - Network architecture diagrams
   - Security group and IAM policy configurations

3. **Security Operations Documentation (HIGH):**
   - Logging and monitoring architecture
   - Incident response procedures
   - Secret management procedures
   - Backup and disaster recovery plans

4. **Compliance and Policy Documentation (MEDIUM):**
   - Confirmed regulatory scope (GDPR, PCI-DSS, CCPA)
   - Data retention policies
   - Privacy policy and data processing agreements

5. **Dependency and Version Information (LOW):**
   - Package.json and dependencies
   - Dockerfile base images
   - Infrastructure component versions

---

## 11. Source Documentation References

### Primary Source Documents

1. **README.md** (34 lines)
   - Path: `/targets/example-quickdeliver/external-resources/README.md`
   - Content: System overview, tech stack summary, documentation index
   - Usage: Initial system understanding, component identification

2. **business-overview.md** (57 lines)
   - Path: `/targets/example-quickdeliver/external-resources/business-overview.md`
   - Content: Business model, revenue streams, market positioning, costs, launch plan
   - Usage: Business context, regulatory scope identification (payment processing, multi-party transactions)

3. **user-stories.md** (91 lines)
   - Path: `/targets/example-quickdeliver/external-resources/user-stories.md`
   - Content: User workflows for customers, drivers, merchants, and administrators
   - Usage: Functionality understanding, data flow identification, user role definitions

4. **product-roadmap.md** (59 lines)
   - Path: `/targets/example-quickdeliver/external-resources/product-roadmap.md`
   - Content: MVP features, growth phases, expansion plans, feature timeline
   - Usage: Operational scale assumptions, feature prioritization, future threat considerations

5. **architecture-overview.md** (130 lines)
   - Path: `/targets/example-quickdeliver/external-resources/architecture-overview.md`
   - Content: Tech stack, system services, data flow, authentication, deployment, performance targets
   - Usage: Component inventory, technology identification, architecture patterns, data flows

6. **api-endpoints.md** (192 lines)
   - Path: `/targets/example-quickdeliver/external-resources/api-endpoints.md`
   - Content: REST API endpoints, WebSocket events, authentication requirements, response codes
   - Usage: API surface identification, authentication boundaries, role-based endpoint separation, WebSocket security

7. **data-model.md** (116 lines)
   - Path: `/targets/example-quickdeliver/external-resources/data-model.md`
   - Content: PostgreSQL table schemas, Redis cache keys, S3 storage categories
   - Usage: Data asset identification, database structure, sensitive data location, data relationships

8. **mobile-app-features.md** (70 lines)
   - Path: `/targets/example-quickdeliver/external-resources/mobile-app-features.md`
   - Content: iOS/Android app features for customers and drivers, common mobile features
   - Usage: Mobile app functionality, GPS tracking details, client-side data handling

9. **third-party-integrations.md** (106 lines)
   - Path: `/targets/example-quickdeliver/external-resources/third-party-integrations.md`
   - Content: Stripe, Twilio, Google Maps, Firebase, Checkr, and AWS service integrations
   - Usage: External trust boundaries, data transmission to third parties, webhook identification, integration security

### Documentation Quality Summary

**Strengths:**
- Comprehensive functional documentation covering business model, user workflows, and features
- Detailed technical specifications: complete API documentation, full data model, architecture overview
- Clear third-party integration descriptions with data flows and purposes
- Consistent documentation style and level of detail across all files

**Weaknesses:**
- No explicit security documentation (controls, threat model, security requirements)
- Limited implementation details (library versions, configurations, deployment specifics)
- Operational aspects not covered (monitoring, logging, incident response, secret management)
- No compliance documentation or security policies
- Current operational status and scale not specified

**Overall Assessment:** Excellent functional and architectural documentation quality; sufficient for comprehensive architectural threat modeling; additional security-specific documentation recommended for complete security assessment

---

**END OF STAGE 1 ANALYSIS**

This Stage 1 analysis provides the foundation for subsequent threat modeling stages:
- **Stage 2** will use this component inventory and trust boundaries to create detailed data flow diagrams
- **Stage 3** will apply STRIDE methodology to identified components and trust boundaries
- **Stage 4** will assess risks using the data asset catalog and business context
- **Stage 5** will recommend mitigations aligned with identified components and security gaps
- **Stage 6** will synthesize findings into executive-ready comprehensive report

---
