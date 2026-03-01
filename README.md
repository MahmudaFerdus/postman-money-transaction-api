Money Transaction API – Automated Postman Collection (With Security Analysis)
This repository contains a fully automated Postman Collection and Environment file for testing the Money Transaction System API. It simulates a complete financial ecosystem with multiple user roles and performs end-to-end transaction workflows without manual intervention.

Beyond functional testing, this project also identifies critical security vulnerabilities in authorization and access control.

📄 API Documentation

+-------------+----------------------------------------------------------------------+
| Role        | Responsibilities                                                     |
+-------------+----------------------------------------------------------------------+
| Admin       | User management, virtual money creation, commissions, system deposits|
| Agent       | Deposits to customers                                                |
| Customer    | Withdrawals, transfers, payments, balance & history                  |
| Merchant    | Receives payments from customers                                     |
+-------------+----------------------------------------------------------------------+

Base Configuration
+------------------------+--------------------------------------------------+
| Parameter              | Value                                            |
+------------------------+--------------------------------------------------+
| Base URL               | https://mta.newroztech.com/api                   |
| AUTH_SECRET_KEY        | e97b4ca15fd2b3086c1e4af98b72d503                 |
| AUTH-SECRET-KEY-SYSTEM | b82439df1c92a7fe504bf23da918e6f1                 |
+------------------------+--------------------------------------------------+
"hese values are pre-configured in the Postman Environment file."
Environment Variables are Manually Configured

+--------------------+--------------------------------------------------+
| Variable           | Value                                            |
+--------------------+--------------------------------------------------+
| base_url           | https://mta.newroztech.com/api                   |
| auth_secret_key    | e97b4ca15fd2b3086c1e4af98b72d503                 |
| secret_key_system  | b82439df1c92a7fe504bf23da918e6f1                 |
+--------------------+--------------------------------------------------+

Auto-Generated via Postman Scripts
All tokens, IDs, balances, and dynamic values are captured from API responses automatically:pm.environment.set("admin_token", pm.response.json().token);

+--------------------+--------------------+--------------------+
| Variable           | Variable           | Variable           |
+--------------------+--------------------+--------------------+
| admin_token        | customer_id        | customer_balance   |
| agent_token        | agent_id           | agent_balance      |
| customer_token     | merchant_id        | withdraw_fee       |
| merchant_token     | transaction_id     | and more...        |
+--------------------+--------------------+--------------------+
+--------------------------------------+------------------+
| Feature                              | Status           |
+--------------------------------------+------------------+
| Manual token copying needed          | Not required     |
| Automated execution                 | Fully automated  |
| Dynamic data reuse across requests   | Supported        |
+--------------------------------------+------------------+

Automated Execution Flow
All requests run sequentially using postman.setNextRequest(). No manual reordering needed.

Admin Operations

+------+-----------------------------------------------+
| Step | Request                                       |
+------+-----------------------------------------------+
|  1   | Admin Login                                   |
|  2   | Create Customer                               |
|  3   | Create Agent                                  |
|  4   | Create Merchant                               |
|  5   | User List                                     |
|  6   | Search User by Email                          |
|  7   | Search User by ID                             |
|  8   | Create Virtual Money (From SYSTEM)            |
|  9   | System Virtual Balance                        |
|  10  | Commission Create                             |
|  11  | Commission Listing                            |
|  12  | Deposit System → Agent                        |
+------+-----------------------------------------------+

Agent Operations


+------+-----------------------------------------------+
| Step | Request                                       |
+------+-----------------------------------------------+
|  13  | Agent Login                                   |
|  14  | Deposit Agent → Customer                      |
+------+-----------------------------------------------+
Customer Operations


+------+-----------------------------------------------+
| Step | Request                                       |
+------+-----------------------------------------------+
|  15  | Deposit System → Customer                     |
|  16  | Customer Login                                |
|  17  | Withdraw Customer → Agent                     |
|  18  | Send Money (Customer → Customer)              |
|  19  | Payment (Customer → Merchant)                 |
|  20  | Balance Check                                 |
|  21  | Transaction History                           |
|  22  | Transaction Details                           |
+------+-----------------------------------------------+
Identified Security Issues (Authorization Bugs)
Bug Summary


+-----+----------------------------------------------+-------------+
| #   | Issue                                        | Severity    |
+-----+----------------------------------------------+-------------+
|  1  | Improper Role-Based Access Control (RBAC)    | Critical    |
|  2  | Token Misuse Across Roles                    | Critical    |
|  3  | Secret Key Validation Weakness               | High        |
+-----+----------------------------------------------+-------------+
Bug 1: Improper Role-Based Access Control (RBAC)
The API does not strictly validate user roles against endpoint permissions.



+------------------------------------------+----------+----------+
| Action Performed with Customer Token     | Expected | Actual   |
+------------------------------------------+----------+----------+
| Create Virtual Money                     | Denied   | Allowed  |
| Create Commission                        | Denied   | Allowed  |
| Perform Admin-level operations           | Denied   | Allowed  |
+------------------------------------------+----------+----------+
These operations should be restricted to the Admin role only.

Bug 2: Token Misuse Across Roles
Endpoints requiring admin_token still work when customer_token is used.



+-------------------------+----------------+----------------+---------+
| Endpoint                | Required Token | Token Used     | Result  |
+-------------------------+----------------+----------------+---------+
| Deposit System → Agent  | admin_token    | customer_token | Works   |
+-------------------------+----------------+----------------+---------+
The backend validates only token existence, not role permissions.

Bug 3: Secret Key Validation Weakness

+---------------------------------------------------------------+----------+----------+
| Combined Credentials                                          | Expected | Actual   |
+---------------------------------------------------------------+----------+----------+
| customer_token + AUTH_SECRET_KEY + AUTH-SECRET-KEY-SYSTEM      | Denied   | Allowed  |
+---------------------------------------------------------------+----------+----------+
This indicates missing server-side authorization enforcement and weak privilege separation.

Security Impact


+--------------------------------------+-------------+
| Risk                                 | Severity    |
+--------------------------------------+-------------+
| Privilege Escalation                 | Critical    |
| Unauthorized Fund Creation           | Critical    |
| Commission Manipulation              | High        |
| Financial System Abuse               | Critical    |
| Compromise of System Integrity       | Critical    |
+--------------------------------------+-------------+
Recommendations


+-----+--------------------------------------------------------------+
| #   | Recommendation                                               |
+-----+--------------------------------------------------------------+
|  1  | Implement strict Role-Based Access Control (RBAC)            |
|  2  | Enforce role validation at middleware level                   |
|  3  | Validate token-role mapping on every protected endpoint      |
|  4  | Separate Admin and System privileges clearly                 |
|  5  | Prevent cross-role token misuse                              |
+-----+--------------------------------------------------------------+
What This Project Demonstrates


+---------------------------+---------------------------------------------------+
| Area                      | Details                                           |
+---------------------------+---------------------------------------------------+
| API Automation            | End-to-end workflow with advanced Postman scripting|
| Multi-Role Testing        | Admin, Agent, Customer, Merchant workflows        |
| Dynamic Variables         | Auto-generated tokens, IDs, balances              |
| Transaction Lifecycle     | Deposits, withdrawals, transfers, payments        |
| Security Testing          | RBAC vulnerabilities, privilege escalation analysis|
+---------------------------+---------------------------------------------------+
How to Run


+------+--------------------------------------------------------------+
| Step | Action                                                       |
+------+--------------------------------------------------------------+
|  1   | Clone this repository                                        |
|  2   | Import the Collection and Environment files into Postman     |
|  3   | Select the imported environment                              |
|  4   | Run the collection using Collection Runner                   |
|  5   | All requests execute automatically in sequence               |
+------+--------------------------------------------------------------+
Author


+-----------+---------------------------------------------------+
| Name      | Mahmuda Ferdus                                    |
| GitHub    | https://github.com/MahmudaFerdus                 |
| Purpose   | API automation practice and security testing      |
+-----------+---------------------------------------------------+
