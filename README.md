Money Transaction API – Automated Postman Collection (With Security Analysis)
This repository contains a fully automated Postman Collection and Environment file for testing the Money Transaction System API. It simulates a complete financial ecosystem with multiple user roles and performs end-to-end transaction workflows without manual intervention.

Beyond functional testing, this project also identifies critical security vulnerabilities in authorization and access control.

Roles Covered
Role	Responsibilities
Admin	User management, virtual money creation, commissions, system deposits
Agent	Deposits to customers
Customer	Withdrawals, transfers, payments
Merchant	Receives payments from customers
Base Configuration
Parameter	Value
Base URL	https://mta.newroztech.com/api
AUTH_SECRET_KEY	e97b4ca15fd2b3086c1e4af98b72d503
AUTH-SECRET-KEY-SYSTEM	b82439df1c92a7fe504bf23da918e6f1
These values are pre-configured in the Postman Environment file.

Environment Variables
Manually Configured:

Variable	Value
base_url	https://mta.newroztech.com/api
auth_secret_key	e97b4ca15fd2b3086c1e4af98b72d503
secret_key_system	b82439df1c92a7fe504bf23da918e6f1
Auto-Generated via Postman Scripts:

All tokens, IDs, balances, and dynamic values are captured from API responses automatically:

JavaScript

pm.environment.set("admin_token", pm.response.json().token);
Includes: admin_token, agent_token, customer_token, merchant_token, customer_id, agent_id, merchant_id, customer_balance, agent_balance, withdraw_fee, transaction_id, and more.

✅ No manual token copying · ✅ Fully automated · ✅ Dynamic data reuse across requests

Automated Execution Flow
All requests run sequentially using postman.setNextRequest(). No manual reordering needed.

text

ADMIN OPERATIONS                 AGENT OPERATIONS         CUSTOMER OPERATIONS
─────────────────                ────────────────         ────────────────────
1.  Admin Login                  13. Agent Login          15. Deposit Sys → Customer
2.  Create Customer              14. Deposit Agent        16. Customer Login
3.  Create Agent                     → Customer           17. Withdraw Cust → Agent
4.  Create Merchant                                       18. Send Money (C → C)
5.  User List                            │                19. Payment (C → Merchant)
6.  Search by Email                      │                20. Balance Check
7.  Search by ID                         │                21. Transaction History
8.  Create Virtual Money                 │                22. Transaction Details
9.  System Virtual Balance               │
10. Commission Create                    │
11. Commission Listing                   ▼
12. Deposit Sys → Agent ──────────►  FLOW END



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

API practice/API automation practice
    
