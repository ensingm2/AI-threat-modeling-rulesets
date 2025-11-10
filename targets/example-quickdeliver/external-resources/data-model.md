# QuickDeliver - Data Model

## PostgreSQL Tables

### users
- id, email, password_hash, phone
- role (customer, driver, merchant, admin)
- first_name, last_name
- created_at

### addresses
- id, user_id
- street_address, city, state, postal_code
- latitude, longitude
- delivery_instructions

### payment_methods
- id, user_id
- stripe_payment_method_id (Stripe handles card details)
- type (card, paypal, apple_pay)
- last_four, expiry_month, expiry_year

### merchants
- id, user_id
- business_name, business_type
- address, latitude, longitude
- commission_rate, minimum_order
- status (pending, active, paused)
- rating, total_reviews

### menu_categories
- id, merchant_id
- name, display_order

### menu_items
- id, merchant_id, category_id
- name, description, price
- image_url, is_available

### item_modifiers
- id, menu_item_id
- name (e.g., "Size", "Toppings")
- type (single, multiple)

### modifier_options
- id, modifier_id
- name, price_adjustment

### drivers
- id, user_id
- license_number, vehicle_info
- status (pending, active, suspended)
- is_online, current_latitude, current_longitude
- rating, total_deliveries

### orders
- id, order_number
- customer_id, merchant_id, driver_id
- delivery_address_id
- status (pending, confirmed, preparing, picked_up, delivered, cancelled)
- subtotal, tax, delivery_fee, tip, total
- payment_status
- stripe_payment_intent_id
- created_at, delivered_at

### order_items
- id, order_id, menu_item_id
- quantity, unit_price, subtotal

### order_item_modifiers
- id, order_item_id, modifier_option_id
- price_adjustment

### reviews
- id, order_id, reviewer_id
- reviewee_type (merchant or driver)
- reviewee_id
- rating (1-5), comment

### promotions
- id, code
- discount_type, discount_value
- valid_from, valid_until
- max_uses

### subscriptions
- id, user_id
- status (active, cancelled)
- stripe_subscription_id
- current_period_end

### payouts
- id, payee_id, payee_type (driver or merchant)
- amount, status
- stripe_transfer_id
- period_start, period_end

---

## Redis Cache

**Keys:**
- `session:{user_id}` - JWT session
- `driver:location:{driver_id}` - GPS coordinates
- `drivers:online:{city}` - Set of online driver IDs
- `menu:{merchant_id}` - Cached menu

---

## S3 Storage

- User profile photos
- Merchant logos and menu photos
- Delivery proof photos
- Driver/merchant documents (licenses, permits)
