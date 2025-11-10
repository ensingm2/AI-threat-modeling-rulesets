# QuickDeliver - Third-Party Services

## Stripe (Payments)

**What it does:**
- Customer payments (credit cards, Apple Pay, Google Pay)
- Driver and merchant payouts
- Subscription billing (QuickDeliver Plus)

**Key features:**
- Payment intents for orders
- Connected accounts for drivers/merchants
- Automatic payouts
- Webhook notifications for payment events

---

## Twilio (SMS/Phone)

**What it does:**
- SMS verification codes
- Order status notifications
- Driver dispatch alerts
- Customer support calls (masked numbers for privacy)

**Key features:**
- Programmable SMS
- Phone number masking between customers and drivers

---

## Google Maps Platform

**What it does:**
- Address autocomplete
- Geocoding (convert addresses to coordinates)
- Distance/duration calculations
- Turn-by-turn navigation for drivers
- Real-time route optimization

**APIs used:**
- Places API (autocomplete)
- Geocoding API
- Directions API
- Distance Matrix API

---

## Firebase Cloud Messaging (Push Notifications)

**What it does:**
- Push notifications to mobile apps
- Real-time alerts (order updates, driver arrival, etc.)

**Notification types:**
- Order status changes
- New order alerts for drivers/merchants
- Promotional messages
- Chat messages

---

## Checkr (Background Checks)

**What it does:**
- Driver background checks
- Driving record verification

**Process:**
- Driver submits info during onboarding
- Checkr runs checks (usually 3-5 days)
- Webhook notifies us of results
- Auto-approve or manual review

---

## AWS Services

**S3:**
- Profile photos
- Menu images
- Merchant documents
- Delivery proof photos

**CloudFront:**
- CDN for fast image delivery

**RDS:**
- Managed PostgreSQL database

**ElastiCache:**
- Managed Redis for caching

**ECS:**
- Container hosting for backend services

---

## Merchant POS Integrations (Future)

- Square
- Toast
- Clover

Direct menu/order sync to reduce manual entry.
