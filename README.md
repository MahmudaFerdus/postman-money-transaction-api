💰 Money Transaction API
Automated Postman Collection (With Security Analysis)
This repository contains a fully automated Postman Collection & Environment for testing a Money Transaction System API.

It simulates a complete financial ecosystem with multiple roles and executes end‑to‑end workflows automatically.

In addition to functional testing, this project identifies critical authorization vulnerabilities.

📄 API Documentation
https://documenter.getpostman.com/view/22815578/2sBXcAH2jZ

👥 Roles Covered
Role	Key Capabilities
Admin	Manage users, create virtual money, manage commissions, system deposits
Agent	Deposit money to customers
Customer	Withdraw, transfer, pay merchants, check balance
Merchant	Receive customer payments
⚙️ Base Configuration
Base URL: https://mta.newroztech.com/api
AUTH_SECRET_KEY: e97b4ca15fd2b3086c1e4af98b72d503
AUTH-SECRET-KEY-SYSTEM: b82439df1c92a7fe504bf23da918e6f1
Configured inside the Postman Environment.

🌍 Environment Variables
✅ Manually Configured
base_url
auth_secret_key
secret_key_system
✅ Automatically Generated (via Test Scripts)
Example:

JavaScript

pm.environment.set("admin_token", pm.response.json().token);
Auto-Captured Values
admin_token
agent_token
customer_token
merchant_token
customer_id
agent_id
merchant_id
balances
transaction_id
withdraw_fee
Automation Features
✅ No manual token copying
✅ Fully sequential execution
✅ Dynamic data reuse across requests
🔄 Automated Execution Flow
All requests run sequentially using:

text

postman.setNextRequest()
Admin Workflow
Admin Login
Create Customer
Create Agent
Create Merchant
User Search & Listing
Create Virtual Money
Commission Setup
Deposit System → Agent
Agent Workflow
Agent Login
Deposit Agent → Customer
Customer Workflow
Deposit System → Customer
Customer Login
Withdraw Customer → Agent
Send Money (Customer → Customer)
Payment (Customer → Merchant)
Balance Check
Transaction History
Transaction Details
🔐 Identified Security Issues
🚨 Vulnerability Summary
Issue	Severity
Improper RBAC	🔴 Critical
Token Misuse Across Roles	🔴 Critical
Secret Key Validation Weakness	🟠 High
1️⃣ Improper Role-Based Access Control
Customer token can:

Create Virtual Money ❌ (Should be Admin only)
Create Commission ❌
Perform Admin-level operations ❌
✅ Expected: Access Denied
❌ Actual: Access Allowed

2️⃣ Token Misuse Across Roles
Endpoint	Expected Token	Actual Working Token
Deposit System → Agent	admin_token	customer_token
Backend validates token existence — not role permission.

3️⃣ Secret Key Validation Weakness
Combining:

customer_token
AUTH_SECRET_KEY
AUTH-SECRET-KEY-SYSTEM
Allows privileged operations.

This indicates missing server-side authorization enforcement.

⚠️ Security Impact
Privilege Escalation
Unauthorized Fund Creation
Commission Manipulation
Financial System Abuse
Compromised System Integrity
✅ Recommendations
Implement strict Role-Based Access Control (RBAC)
Validate role in middleware for every protected endpoint
Enforce token-role mapping validation
Separate Admin and System privileges
Prevent cross-role token usage
🎯 What This Project Demonstrates
End-to-End API Automation
Advanced Postman Scripting
Multi-Role Financial Workflow Testing
Dynamic Environment Variable Handling
Security & Authorization Testing
🚀 How to Run
Clone repository
Import Collection & Environment into Postman
Select Environment
Run via Collection Runner
All requests execute automatically
👩‍💻 Author
Mahmuda Ferdus
GitHub: https://github.com/MahmudaFerdus

Purpose: API automation practice and security-focused testing.
