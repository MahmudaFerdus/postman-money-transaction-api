Money Transaction API – Automated Postman Collection (With Security Analysis)
This repository contains a fully automated Postman Collection and Environment file for testing the Money Transaction System API.

The collection simulates a complete financial ecosystem including:

1.Admin
2.Agent
3.Customer
4.Merchant

All requests execute sequentially using:

JavaScript

postman.setNextRequest()
ensuring a complete end‑to‑end financial workflow.

🌐 Base Configuration
🔗 Base URL : https://mta.newroztech.com/api
🔐 Authentication Keys

AUTH_SECRET_KEY: e97b4ca15fd2b3086c1e4af98b72d503
AUTH-SECRET-KEY-SYSTEM: b82439df1c92a7fe504bf23da918e6f1
These are configured inside the Postman Environment.

⚙️ Environment Variables
✅ Manually Configured
Variable	Value
base_url	https://mta.newroztech.com/api
auth_secret_key	e97b4ca15fd2b3086c1e4af98b72d503
secret_key_system	b82439df1c92a7fe504bf23da918e6f1
✅ Automatically Set via Postman Scripts
All tokens, IDs, and dynamic data are automatically stored from API responses using Postman test scripts:

Example:

JavaScript
pm.environment.set("admin_token", pm.response.json().token);

🔄 Auto-generated Variables
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
and many more...
✅ No manual token copying
✅ Fully automated execution
✅ Dynamic data chaining across requests

🔄 Automated Execution Flow
The collection runs in the following strict order:

🛠 Admin Operations
Admin Login
Create Customer
Create Agent
Create Merchant
User List
Search User by Email
Search User by ID
Create Virtual Money (SYSTEM)
System Virtual Balance
Commission Create
Commission Listing
Deposit System → Agent
🏦 Agent Operations
Agent Login
Deposit Agent → Customer
👤 Customer Operations
Deposit System → Customer
Customer Login
Withdraw Customer → Agent
Send Money (Customer → Customer)
Payment (Customer → Merchant)
Balance Check
Transaction History
Transaction Details
🐞 Identified Security Issues (Authorization Bugs)
During testing, several critical authorization vulnerabilities were discovered.

❗ 1. Improper Role-Based Access Control (RBAC)
The API does not properly validate user roles against their permissions.

🔎 Example Findings:
✅ If logged in as a Customer,
and the customer_token is used in the Authorization header:

Customer can create Virtual Money
Customer can create Commission
Customer can perform Admin-level operations
⚠️ These actions should only be allowed for Admin role.

❗ 2. Token Misuse Across Roles
Even when using:

text

Authorization: Bearer {{customer_token}}
for endpoints that require:

text

Authorization: Bearer {{admin_token}}
the API still allows execution.

🔎 Example:
Deposit System → Agent
Expected: Admin Token Required
Actual: Works with Customer Token
This indicates:

No strict role validation
Missing permission checks
Backend only validating token existence, not role authority
❗ 3. Secret Key Validation Weakness
When combining:

customer_token
AUTH_SECRET_KEY
AUTH-SECRET-KEY-SYSTEM
The system still allows privileged operations.

This suggests:

Improper privilege separation
Missing server-side authorization enforcement
🚨 Security Impact
These issues may lead to:

Privilege Escalation
Unauthorized Fund Creation
Unauthorized Commission Manipulation
Financial Fraud Risk
System Integrity Compromise
✅ Recommendation (As QA Observation)
To fix these issues, the API should implement:

Strict Role-Based Access Control (RBAC)
Server-side role verification per endpoint
Proper token-role mapping validation
Middleware-level permission enforcement
Separation of Admin/System privileges
🧪 What This Project Demonstrates
✅ End-to-End API Automation
✅ Advanced Postman Scripting
✅ Multi-Role Workflow Testing
✅ Dynamic Environment Handling
✅ Financial Transaction Simulation
✅ Security Vulnerability Identification
✅ Authorization & Access Control Testing
This project not only demonstrates automation skills but also security-focused API testing capability.

📖 API Documentation
👉 https://documenter.getpostman.com/view/22815578/2sBXcAH2jZ

👩‍💻 Author
Mahmuda Ferdus
GitHub: https://github.com/MahmudaFerdus

📌 Project Purpose
This project was built for:

API Automation Practice
