# Test Cases – MediReach

| ID | Test Case | Expected Result |
|---|---|---|
| TC01 | Register a new customer | Account is created successfully |
| TC02 | Login with valid credentials | User reaches the dashboard |
| TC03 | Login with invalid password | Login is rejected |
| TC04 | Search for an available medicine | Matching medicines are displayed |
| TC05 | Search for unavailable medicine | User is informed that it is unavailable |
| TC06 | View nearby medical shops | Participating nearby shops are displayed |
| TC07 | Add medicine to cart | Medicine appears in cart |
| TC08 | Place order with valid details | Order is created successfully |
| TC09 | Upload an allowed prescription file | File is accepted and linked to the order |
| TC10 | Upload unsupported file type | Upload is rejected |
| TC11 | Shop accepts an order | Order status changes to accepted/preparing |
| TC12 | Shop marks order ready | Status changes to ready for pickup |
| TC13 | Delivery partner accepts assignment | Delivery is assigned |
| TC14 | Delivery partner marks pickup | Status changes to out for delivery |
| TC15 | Delivery partner marks delivered | Order status becomes delivered |
| TC16 | Customer views order history | Previous orders are displayed |
| TC17 | Unauthenticated user accesses protected order route | Access is denied |
| TC18 | Caregiver places order for linked elderly user | Order is created for the selected elderly profile |
| TC19 | User enters invalid quantity | Validation message is shown |
| TC20 | User submits an empty required field | Form validation prevents submission |

## Test Data
Use only dummy data such as:
- Demo customer: Elderly User
- Demo shop: Village Care Medicals
- Demo medicine: Paracetamol 500mg
- Demo delivery partner: Demo Delivery Partner

Never use real patient information.
