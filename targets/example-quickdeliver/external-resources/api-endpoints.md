# QuickDeliver - API Endpoints

**Base URL**: `https://api.quickdeliver.com/v1`

**Auth**: All endpoints need `Authorization: Bearer <token>` header except login/signup

---

## Auth

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/auth/register` | Sign up |
| POST | `/auth/login` | Log in |
| POST | `/auth/login/social` | OAuth (Google/Apple/Facebook) |
| POST | `/auth/forgot-password` | Reset password |
| POST | `/auth/refresh-token` | Get new token |

## User Profile

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/users/me` | Get my profile |
| PUT | `/users/me` | Update profile |
| GET | `/users/me/addresses` | Get saved addresses |
| POST | `/users/me/addresses` | Add address |
| DELETE | `/users/me/addresses/{id}` | Delete address |
| GET | `/users/me/payment-methods` | Get saved cards |
| POST | `/users/me/payment-methods` | Add card |
| DELETE | `/users/me/payment-methods/{id}` | Delete card |

---

## Customer Endpoints

### Merchants

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/merchants` | Browse restaurants |
| GET | `/merchants/{id}` | Get restaurant details |
| GET | `/merchants/{id}/menu` | Get menu |

### Orders

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/orders` | Place order |
| GET | `/orders/{id}` | Get order details |
| GET | `/orders` | Order history |
| PUT | `/orders/{id}/cancel` | Cancel order |
| POST | `/orders/{id}/tip` | Add/update tip |
| POST | `/orders/{id}/review` | Rate order |
| POST | `/orders/{id}/issue` | Report problem |

### Subscription

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/subscription/subscribe` | Subscribe to Plus |
| DELETE | `/subscription/cancel` | Cancel subscription |

### Promos

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/promos/validate` | Check promo code |
| GET | `/promos/available` | Get deals |

---

## Driver Endpoints

### Profile

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/drivers/apply` | Apply to be driver |
| GET | `/drivers/me` | Get my profile |
| POST | `/drivers/documents` | Upload docs |

### Deliveries

| Method | Endpoint | What it does |
|--------|----------|--------------|
| PUT | `/drivers/me/status` | Go online/offline |
| GET | `/drivers/orders/available` | Get delivery requests |
| POST | `/drivers/orders/{id}/accept` | Accept delivery |
| POST | `/drivers/orders/{id}/decline` | Decline delivery |
| PUT | `/drivers/orders/{id}/pickup` | Mark picked up |
| PUT | `/drivers/orders/{id}/deliver` | Mark delivered |

### Money

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/drivers/earnings` | See earnings |
| POST | `/drivers/payout/instant` | Cash out now |
| GET | `/drivers/me/stats` | Performance stats |

---

## Merchant Endpoints

### Profile

| Method | Endpoint | What it does |
|--------|----------|--------------|
| POST | `/merchants/apply` | Apply as merchant |
| GET | `/merchants/me` | Get my profile |
| PUT | `/merchants/me/availability` | Pause/resume orders |

### Menu

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/merchants/me/menu` | Get menu |
| POST | `/merchants/me/menu/items` | Add menu item |
| PUT | `/merchants/me/menu/items/{id}` | Update item |
| DELETE | `/merchants/me/menu/items/{id}` | Delete item |
| POST | `/merchants/me/menu/import` | Import menu CSV |

### Orders

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/merchants/me/orders/pending` | Get new orders |
| POST | `/merchants/me/orders/{id}/accept` | Accept order |
| POST | `/merchants/me/orders/{id}/reject` | Reject order |
| PUT | `/merchants/me/orders/{id}/ready` | Mark ready for pickup |

### Stats

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/merchants/me/analytics/sales` | Sales reports |
| GET | `/merchants/me/payouts` | Payout history |

---

## Admin Endpoints

| Method | Endpoint | What it does |
|--------|----------|--------------|
| GET | `/admin/users` | Search users |
| PUT | `/admin/users/{id}/suspend` | Ban user |
| GET | `/admin/drivers/applications` | Driver applications |
| POST | `/admin/drivers/{id}/approve` | Approve driver |
| GET | `/admin/merchants/applications` | Merchant applications |
| POST | `/admin/merchants/{id}/approve` | Approve merchant |
| GET | `/admin/orders` | All orders |
| POST | `/admin/orders/{id}/refund` | Issue refund |
| POST | `/admin/promos` | Create promo code |

---

## WebSocket Events

**Connect**: `wss://ws.quickdeliver.com` with auth token

### Customer receives:
- `order:confirmed` - Merchant accepted
- `driver:assigned` - Driver on the way
- `driver:location` - Driver GPS update
- `order:picked_up` - Driver has food
- `order:delivered` - Order complete
- `eta:updated` - ETA changed

### Driver receives:
- `delivery:request` - New delivery available
- `order:ready` - Food ready for pickup
- `order:cancelled` - Customer cancelled

### Merchant receives:
- `order:new` - New order incoming
- `driver:arrived` - Driver at restaurant

---

## Response Codes

| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 400 | Bad request |
| 401 | Not logged in |
| 403 | Not allowed |
| 404 | Not found |
| 429 | Too many requests |
| 500 | Server error |
