# QuickDeliver - Architecture Overview

## System Overview

Simple 3-tier web app: mobile apps + backend APIs + databases. All hosted on AWS.

```
[Mobile Apps] → [Load Balancer] → [Node.js Services] → [Databases]
```

---

## Tech Stack

### Frontend
- **Customer & Driver Apps**: React Native (iOS + Android)
- **Merchant & Admin Portal**: React web app
- **Maps**: Google Maps SDK
- **Notifications**: Firebase Cloud Messaging

### Backend
- **Language**: Node.js + Express
- **API**: REST + WebSocket for real-time tracking
- **Auth**: JWT tokens

### Databases
- **PostgreSQL**: Main database (users, orders, merchants, menus)
- **Redis**: Cache and session storage
- **S3**: Images and files

### AWS Services
- **ECS**: Run Docker containers
- **RDS**: PostgreSQL database
- **ElastiCache**: Redis
- **S3**: File storage
- **CloudFront**: CDN for images/static files
- **Load Balancer**: Route traffic

### Third-Party
- **Stripe**: Payments
- **Twilio**: SMS
- **Google Maps**: Geocoding, routing, navigation
- **Firebase**: Push notifications

---

## Services

### User Service
- Login/signup
- User profiles
- Passwords

### Order Service
- Create orders
- Track order status
- Order history

### Driver Service  
- Driver signup
- Assignment algorithm (who gets which delivery)
- Track driver location

### Merchant Service
- Restaurant profiles
- Menus
- Hours and availability

### Payment Service
- Stripe integration
- Process payments
- Split money (merchant + driver + platform)
- Refunds

### Notification Service
- Push notifications
- SMS alerts
- Emails

### Tracking Service
- WebSocket server for real-time location
- Calculate ETA
- Route optimization

---

## Data Flow

### Ordering Flow
1. Customer browses merchants
2. Adds items to cart
3. Submits order + payment
4. Stripe authorizes payment
5. System finds available driver
6. Driver accepts
7. Driver picks up order
8. Customer sees live tracking
9. Driver delivers
10. Payment captured, money split

### Real-Time Tracking
- Driver app sends GPS every 5 seconds
- Tracking service broadcasts to customer via WebSocket
- Calculate updated ETA based on location

---

## Authentication

- Users log in with email/password or OAuth (Google/Apple/Facebook)
- Server returns JWT token
- Token required for all API calls
- Token expires after 15 min, refresh token for 7 days

---

## Deployment

- Everything runs in Docker containers
- AWS ECS manages containers
- Auto-scaling based on load
- Deploy via GitHub Actions CI/CD

---

## Performance Targets

- API response < 200ms
- Real-time updates < 2 second delay
- 99.9% uptime
