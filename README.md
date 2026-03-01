Money Transaction API – Automated Postman Collection (With Security Analysis)
This repository contains a fully automated Postman Collection and Environment file for testing the Money Transaction System API.

The collection simulates a complete financial ecosystem involving multiple user roles and performs end-to-end transaction workflows automatically.

Roles Covered
Admin
Agent
Customer
Merchant
All requests are executed sequentially using:

JavaScript

postman.setNextRequest()
This ensures a proper business flow from user creation to transaction history without manual intervention.

Base Configuration
Base URL
text

https://mta.newroztech.com/api
Authentication Keys
text

AUTH_SECRET_KEY: e97b4ca15fd2b3086c1e4af98b72d503
AUTH-SECRET-KEY-SYSTEM: b82439df1c92a7fe504bf23da918e6f1
These values are configured inside the Postman Environment.

Environment Variables
Manually Configured Variables
Variable Name	Value
base_url	https://mta.newroztech.com/api
auth_secret_key	e97b4ca15fd2b3086c1e4af98b72d503
secret_key_system	b82439df1c92a7fe504bf23da918e6f1
Automatically Set via Postman Test Scripts
All tokens, IDs, balances, and other dynamic values are captured from API responses and stored automatically using Postman scripts.

Example:

JavaScript

pm.environment.set("admin_token", pm.response.json().token);
Auto-generated Variables Include:
admin_token
agent_token
customer_token
merchant_token
customer_id
agent_id
merchant_id
customer_balance
agent_balance
withdraw_fee
transaction_id
and other transaction-related values
✔ No manual token copying
✔ Fully automated execution
✔ Dynamic data reuse across requests

Automated Execution Flow
The collection runs in the following strict sequence:

Admin Operations
Admin Login
Create Customer
Create Agent
Create Merchant
User List
Search User by Email
Search User by ID
Create Virtual Money (From SYSTEM)
System Virtual Balance
Commission Create
Commission Listing
Deposit System → Agent
Agent Operations
Agent Login
Deposit Agent → Customer
Customer Operations
Deposit System → Customer
Customer Login
Withdraw Customer → Agent
Send Money (Customer → Customer)
Payment (Customer → Merchant)
Balance Check
Transaction History
Transaction Details
The request order is controlled programmatically. Manual reordering is not required.

Identified Security Issues (Authorization Bugs)
During testing, several authorization weaknesses were identified.

1. Improper Role-Based Access Control (RBAC)
The API does not strictly validate user roles against endpoint permissions.

Observation:
If logged in as a Customer, and the customer_token is used in the Authorization header:

The customer can create Virtual Money
The customer can create Commission
The customer can perform Admin-level operations
These operations should be restricted to the Admin role only.

2. Token Misuse Across Roles
Endpoints that require admin_token still work when customer_token is used.

Example:

Deposit System → Agent

Expected: Admin token required
Actual: Works with customer_token
This suggests that the backend validates only token existence, not role permissions.

3. Secret Key Validation Weakness
When combining:

customer_token
AUTH_SECRET_KEY
AUTH-SECRET-KEY-SYSTEM
Privileged operations can still be performed.

This indicates missing server-side authorization enforcement and weak privilege separation.

Security Impact
These issues may result in:

Privilege escalation
Unauthorized fund creation
Commission manipulation
Financial system abuse
Compromise of system integrity
Recommendations
Based on testing observations, the following improvements are recommended:

Implement strict Role-Based Access Control (RBAC)
Enforce role validation at middleware level
Validate token-role mapping on every protected endpoint
Separate Admin and System privileges clearly
Prevent cross-role token misuse
What This Project Demonstrates
End-to-End API Automation
Advanced Postman scripting
Multi-role workflow testing
Dynamic environment variable handling
Financial transaction lifecycle validation
Security and authorization testing
This project demonstrates both functional automation and security-focused API testing.

API Documentation
https://documenter.getpostman.com/view/22815578/2sBXcAH2jZ

Author
Mahmuda Ferdus
GitHub: https://github.com/MahmudaFerdus

Project Purpose
This project was built for:

API automation practice
