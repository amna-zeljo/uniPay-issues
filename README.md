# uniPay-issues

## 1. Introduction 

The SSST Digital Wallet "UniPay" is a cashless payment solution designed specifically for the SSST University canteen. This digital platform aims to streamline the payment process, reduce wait times, and eliminate the need for physical cash transactions within the university campus.
The system allows customers; students, faculty, and staff, to create digital wallet accounts, which they can top up using different methods. When creating an account, each user receives a unique QR code that serves as their digital identity for payment purposes. When making a purchase at the canteen, users simply present their QR code, which canteen staff scan to process the transaction, automatically deducting the appropriate amount from the user's wallet balance or points if one has offered subscription points.

The SSST Digital Wallet offers multiple payment options to accommodate different user preferences:
- Standard balance system (digital currency)
- Meal plan subscriptions points 
This solution not only modernizes the payment experience but also provides users with detailed transaction histories, enabling better budget management and spending awareness.

## 2. Features 
UniPay includes the following features:
- Login feature for customers/staff members that already made an account 
- Sign Up feature for new customers/staff members
- Customer homepage from where customers can navigate to all other features
- Canteen staff homepage (for members that logged in or signed up as Staff member)
- Transaction Log history page
- Menu page of all products from the university canteen


## 3. User Interface  
The SSST Digital Wallet application follows a logical navigation structure designed to provide an intuitive user experience. The application flow begins with role selection and branches into different paths based on user type and actions.

All pages include navigation paths back to their parent pages, ensuring users can easily move throughout the application without getting lost.
The sitemap uses a color scheme that matches our application design:
- Blue: Primary pages that serve as main navigation hubs
- Light Gray: Secondary pages for specific functions
- Medium Gray (dashed outline): Pop-up elements that appear over existing pages

### Navigation Structure:
#### 3.1. Entry Points (1.0):
Users begin at the Role Selection screen where they choose their role (customer or staff)
From here, users can navigate to Sign Up, Login, or directly to the Staff Dashboard (with proper authorization)
#### 3.2. Authentication (1.1-1.2):
- New users follow the Sign Up path (1.1)
- Returning users follow the Login path (1.2)
- Both paths lead to the Customer Wallet Dashboard for regular users.
#### 3.3. Customer Journey (3.0-3.3):
The Customer Wallet Dashboard (3.0) serves as the central hub for all customer activities. 
From the dashboard, customers can navigate to:
- Customer Top Up Page (3.1) to add funds
- Customer Transactions Log (3.2) to view transaction history
- SSST Menu Page (3.3) to browse available items
- When accessing the Top Up feature, users can view detailed instructions via a pop-up (3.1.1)
#### 3.4. Staff Journey (2.0):
Staff members access their specialized dashboard directly from role selection
The Staff Wallet Dashboard provides tools for processing payments and managing the system
 
## 4. Functionalities
1. User Account Management:
2. Sign Up: New users (students, faculty, and staff) can create digital wallet accounts.
3. Login: Existing users can securely log into their accounts.
4. QR Code Generation: Upon account creation, each user receives a unique QR code serving as their digital payment identity.
5. Wallet Top-Up Options: Users can add funds to their digital wallet.
6. Payment Processing:
   - Users make payments by presenting their QR code at the canteen, which staff scan to complete the transaction.
   - Automatic deduction of the appropriate amount from the user's wallet balance or meal plan subscription points.
7. Meal Plan Subscription Points: Users can subscribe to meal plans using points as an alternative payment method.
8. Canteen Staff Interface: Staff members have a dedicated homepage for processing transactions and managing sales.
9. Customer Homepage: Users can access all features from a centralized customer dashboard.
10. Transaction History: Users can view detailed logs of all their past transactions for better budget management.
11. Canteen Menu Display: A menu page showcasing all available canteen products for easy selection and payment.
12. Real-Time Transaction Processing: Quick and efficient payment processing to reduce wait times at the canteen.
13. Budget Management Tools: Users can track spending and manage their finances with transaction history insights.
14. Subscription Management: Users can manage and modify their meal plan subscriptions easily.
15. Cashless Payment Experience: Complete elimination of physical cash transactions within the university canteen.

These functionalities aim to enhance the payment experience, improve efficiency, and provide users with greater control over their spending within the SSST University campus.

## 5. API Documentation
This section outlines all endpoints needed for the application's core functionality. Organized into five sections covering authentication, wallet management, transactions, menu browsing, and staff operations, it provides a clear structure for development. Each endpoint includes its URL path, request/response formats, and purpose, with comprehensive DTOs defining all data structures. This documentation serves as the blueprint for implementing both customer and staff interfaces while ensuring security and consistency.
- API Authentication & User Management: handles user registration, login, and profile management with secure role-based access control.
<img width="495" alt="API authentication" src="https://github.com/user-attachments/assets/aae4006a-23ad-4ed7-bcea-6466e12161fe" />

- API Wallet: enables customers to view their balance, add funds, and access top-up instructions through intuitive endpoints.
<img width="493" alt="API wallet" src="https://github.com/user-attachments/assets/47d6e340-0bd8-4056-a212-238f91f15500" />

- API Transactions: provides comprehensive history tracking and detailed transaction information for complete financial transparency.
<img width="492" alt="API transactions" src="https://github.com/user-attachments/assets/752259a1-243b-4de3-a0f5-f1fc139341b5" />

- API Menu Management: allows users to browse available food items, view details, and access nutritional information through simple query parameters.
<img width="510" alt="API menu" src="https://github.com/user-attachments/assets/d15b6079-144d-4d50-a054-50a6e7bf5ca5" />

- API Staff Operations: equips canteen workers with dashboard analytics and QR code scanning functionality for efficient payment processing.
<img width="506" alt="API staff" src="https://github.com/user-attachments/assets/295eb191-1beb-48f8-8fa0-2a558ddc367f" />

### Data Transfer Objects
1) UserRegistrationDto 
```
{
  "username": "string",
  "email": "string",
  "password": "string",
  "role": "customer" | "staff",
  "fullName": "string",
  "studentId": "string (optional)"
}
```
2) LoginDto
```
{
  "email": "string",
  "password": "string"
}
```
3) UserDto
```
{
  "userId": "string",
  "username": "string",
  "email": "string",
  "fullName": "string",
  "role": "customer" | "staff",
  "studentId": "string (optional)",
  "qrCode": "string (base64 encoded)",
  "token": "string (only included after login/registration)"
}
```
4) UserUpdateDto
```
{
  "username": "string (optional)",
  "email": "string (optional)",
  "fullName": "string (optional)",
  "password": "string (optional)"
}
```
5) RolesDto
```
{
  "roles": [
	{
  	"id": "string",
  	"name": "string",
  	"description": "string"
	}
  ]
}
```
6) WalletDto
```
{
  "balance": "number",
  "points": "number",
  "mealPlanStatus": "active" | "inactive",
  "qrCode": "string (base64 encoded)",
  "lastUpdated": "string (ISO format)",
  "recentTransactions": [
	{
  	"id": "string",
  	"date": "string (ISO format)",
  	"amount": "number",
  	"type": "topup" | "purchase",
  	"description": "string"
	}
  ]
}
```
7) TopUpDto
```
{
  "amount": "number",
  "paymentMethod": "cash" | "points" | "mealPlan",
  "notes": "string (optional)"
}
```
8) TransactionDto
```
{
  "transactionId": "string",
  "amount": "number",
  "newBalance": "number",
  "timestamp": "string (ISO format)",
  "status": "success" | "pending" | "failed"
}
```
9) InstructionsDto
```
{
  "methods": [
	{
  	"id": "string",
  	"name": "string",
  	"instructions": "string",
  	"locations": ["string"],
  	"conversionRate": "number (if applicable)"
	}
  ]
}
```
10) TransactionsFilterDto
```
{
  "startDate": "string (ISO format, optional)",
  "endDate": "string (ISO format, optional)",
  "type": "topup" | "purchase (optional)",
  "limit": "number (optional, default: 20)",
  "offset": "number (optional, default: 0)"
}
```
11) TransactionsListDto
```
{
  "transactions": [
	{
  	"id": "string",
  	"date": "string (ISO format)",
  	"amount": "number",
  	"type": "topup" | "purchase",
  	"description": "string",
  	"paymentMethod": "cash" | "points" | "mealPlan",
  	"balance": "number (balance after transaction)"
	}
  ],
  "pagination": {
	"total": "number",
	"limit": "number",
	"offset": "number",
	"hasMore": "boolean"
  }
}
```
12) TransactionDetailDto
```
{
  "id": "string",
  "date": "string (ISO format)",
  "amount": "number",
  "type": "topup" | "purchase",
  "description": "string",
  "paymentMethod": "cash" | "points" | "mealPlan",
  "items": [
	{
  	"name": "string",
  	"quantity": "number",
  	"price": "number",
  	"subtotal": "number"
	}
  ],
  "balanceBefore": "number",
  "balanceAfter": "number",
  "receiptUrl": "string (optional)"
}
```
13) MenuFilterDto
```
{
  "category": "string (optional)",
  "available": "boolean (optional)",
  "search": "string (optional)"
}
```
14) MenuListDto
```
{
  "categories": ["string"],
  "items": [
	{
  	"id": "string",
  	"name": "string",
  	"description": "string",
  	"price": "number",
  	"pointsPrice": "number (optional)",
  	"category": "string",
  	"imageUrl": "string (optional)",
  	"available": "boolean"
	}
  ]
}
```
15) MenuItemDetailDto
```
{
  "id": "string",
  "name": "string",
  "description": "string",
  "price": "number",
  "pointsPrice": "number (optional)",
  "category": "string",
  "imageUrl": "string (optional)",
  "nutritionalInfo": {
	"calories": "number",
	"protein": "number",
	"carbs": "number",
	"fat": "number",
	"allergens": ["string"]
  },
  "available": "boolean",
  "popularityRank": "number"
}
```
16) StaffDashboardDto
```
{
  "dailyTransactions": "number",
  "dailyRevenue": "number",
  "pendingOrders": "number",
  "popularItems": [
	{
  	"id": "string",
  	"name": "string",
  	"count": "number"
	}
  ]
}
```
17) ScanDto
```
{
  "transactionId": "string",
  "customerName": "string",
  "amount": "number",
  "newBalance": "number",
  "status": "success" | "failed",
  "timestamp": "string (ISO format)"
}
```
18) PaymentResponseDto
```
{
  "transactionId": "string",
  "customerName": "string",
  "amount": "number",
  "newBalance": "number",
  "status": "success" | "failed",
  "timestamp": "string (ISO format)"
}
```

## 6. Technical Requirements 
UniPay is built using the following technical requirements:
- Backend: Java, Spring, PostgreSQL, etc.
- Frontend: Angular, HTML, CSS, etc.

## 7. Mockups
The following screenshots showcase the user interface design ideas roughly drafted as the general approach which is subject to alter over the course of creating , illustrating the visual implementation of key features. These designs demonstrate the intuitive navigation flow from role selection through authentication to the main wallet dashboard. The mockups highlight the clean, modern interface with a consistent color scheme of blue, dark grey, and white that enhances usability. Each screen has been carefully designed to provide a seamless user experience, with special attention to the QR code display, transaction history visualization, and menu browsing functionality. The designs reflect both customer and staff perspectives, ensuring that all user roles have appropriate interfaces for their specific needs.
<img width="904" alt="Login" src="https://github.com/user-attachments/assets/baac0b46-9464-4115-9ddd-d53d745ec7a4" />
<img width="838" alt="account" src="https://github.com/user-attachments/assets/eb612af0-065c-4f57-903b-904b0b270953" />
<img width="359" alt="staff" src="https://github.com/user-attachments/assets/58de1e7e-1830-41fc-a5e9-7d4d3c05e201" />


https://www.figma.com/design/wUWI3d5djnR9VUA7nhk1I0/UniPay?node-id=0-1&t=CHrAkjUCtfhDgBJ7-1



