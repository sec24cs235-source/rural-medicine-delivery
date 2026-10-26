# Technical Design Document – MediReach

## 1. System Objective
Build a rural-first medicine ordering platform that connects elderly users with nearby medical shops and delivery partners.

## 2. High-Level Architecture

```text
+---------------------+
| Elderly User        |
| / Caregiver         |
+----------+----------+
           |
           v
+---------------------+
| Web Frontend        |
+----------+----------+
           |
           v
+---------------------+
| REST API / Backend  |
+----+-----------+----+
     |           |
     v           v
+---------+   +----------------+
| MongoDB |   | Location/Maps  |
+---------+   +----------------+
     |
     +--------------------+
     |                    |
     v                    v
Medical Shop          Order Service
     |                    |
     +----------+---------+
                |
                v
        Delivery Partner
```

## 3. User Roles

### Elderly Customer
- Register/login
- Search medicines
- View shop availability
- Upload prescription when needed
- Place orders
- Track order status

### Caregiver
- Manage linked elderly profile
- Place orders on behalf of the elderly user
- View order status

### Medical Shop
- Manage shop profile
- Add/update medicine stock
- Accept/reject orders
- Verify prescription where required
- Mark order ready for pickup

### Delivery Partner
- View assigned deliveries
- Accept delivery
- Mark picked up
- Mark delivered

### Admin
- Manage users
- Approve/manage medical shops
- Manage delivery partners
- Monitor orders
- Handle platform-level issues

## 4. Suggested Database Collections

### users
- _id
- name
- phone/email
- passwordHash
- role
- address
- location
- caregiver information

### shops
- _id
- shopName
- ownerId
- address
- location
- phone
- operatingHours
- verificationStatus

### medicines
- _id
- shopId
- name
- category
- price
- stock
- prescriptionRequired

### orders
- _id
- userId
- shopId
- deliveryPartnerId
- items
- totalAmount
- prescriptionUrl
- deliveryAddress
- status
- createdAt

### delivery
- _id
- orderId
- partnerId
- pickupTime
- deliveryTime
- status

## 5. Order Lifecycle

```text
PLACED
  |
  v
SHOP_ACCEPTED
  |
  v
PREPARING
  |
  v
READY_FOR_PICKUP
  |
  v
OUT_FOR_DELIVERY
  |
  v
DELIVERED
```

Alternative states:
`REJECTED`, `CANCELLED`, `DELIVERY_FAILED`

## 6. API Examples

### Authentication
- POST `/api/auth/register`
- POST `/api/auth/login`

### Medicines
- GET `/api/medicines`
- GET `/api/medicines/:id`

### Shops
- GET `/api/shops/nearby`
- GET `/api/shops/:id`

### Orders
- POST `/api/orders`
- GET `/api/orders/my`
- GET `/api/orders/:id`
- PATCH `/api/orders/:id/status`

### Delivery
- GET `/api/delivery/my`
- PATCH `/api/delivery/:id/status`

Use the actual routes implemented in the prototype when the backend is finalized.

## 7. Security
- Hash passwords; never store plain-text passwords.
- Use JWT/session-based authentication.
- Protect role-specific routes.
- Validate uploaded files and restrict file types/sizes.
- Do not commit `.env` files or secrets.
- Do not publish real patient or prescription information.

## 8. Accessibility
- Large text and buttons
- High-contrast design
- Simple navigation
- Minimal steps to place an order
- Regional-language support
- Voice assistance as a future enhancement

## 9. Privacy
Only collect data required for ordering and delivery. Avoid storing unnecessary health information. Prescription documents should be access-controlled and protected.

## 10. Deployment
The frontend can be deployed using a static hosting platform or web hosting service. The backend can be deployed on a cloud server, with MongoDB hosted locally for development or through a managed database service.

## 11. Limitations of Prototype
- Delivery availability depends on participating shops.
- Location accuracy depends on the device/location service.
- Prescription verification is performed by the pharmacy/provider.
- The prototype may use sample payment and delivery data.
