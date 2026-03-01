# 💰 Money Transaction API  
### Automated Postman Collection with Security Analysis

This repository contains a fully automated **Postman Collection & Environment** for testing a **Money Transaction System API**.

It simulates a complete financial ecosystem with multiple roles and executes end‑to‑end workflows automatically.

In addition to functional testing, this project identifies **critical authorization vulnerabilities**.

---

## 📄 API Documentation

| Resource | Link |
|----------|------|
| Postman Documentation | https://documenter.getpostman.com/view/22815578/2sBXcAH2jZ |

---

# 👥 Roles Covered

| Role      | Key Capabilities |
|-----------|-----------------|
| 👑 **Admin**    | Manage users, Create virtual money, Manage commissions, System deposits |
| 🏪 **Agent**    | Deposit money to customers |
| 👤 **Customer** | Withdraw, Transfer, Pay merchants, Check balance |
| 🛍️ **Merchant** | Receive customer payments |

---

# ⚙️ Base Configuration

| Configuration | Value |
|--------------|-------|
| Base URL | https://mta.newroztech.com/api |
| AUTH_SECRET_KEY | e97b4ca15fd2b3086c1e4af98b72d503 |
| AUTH-SECRET-KEY-SYSTEM | b82439df1c92a7fe504bf23da918e6f1 |

✅ Configured inside Postman Environment

---

# 🌍 Environment Variables

## ✅ Manually Configured

| Variable Name |
|--------------|
| base_url |
| auth_secret_key |
| secret_key_system |

---

## ✅ Automatically Generated (via Test Scripts)

### Example Script

```javascript
pm.environment.set("admin_token", pm.response.json().token);

### 🔄 Auto-Captured Values (Generated Automatically)

| Tokens                | IDs                | Others               |
|-----------------------|--------------------|----------------------|
| `admin_token`         | `customer_id`      | `balances`           |
| `agent_token`         | `agent_id`         | `transaction_id`     |
| `customer_token`      | `merchant_id`      | `withdraw_fee`       |
| `merchant_token`      |                    |                      |

### 🤖 Automation Features

| Feature                              | Status |
|--------------------------------------|--------|
| No manual token copying              | ✅     |
| Fully sequential execution           | ✅     |
| Dynamic data reuse across requests   | ✅     |

### 🔄 Automated Execution Flow  
All requests run in perfect order using `postman.setNextRequest()`

#### 👑 Admin Workflow
| Step                          |
|-------------------------------|
| Admin Login                   |
| Create Customer               |
| Create Agent                  |
| Create Merchant               |
| User Search & Listing         |
| Create Virtual Money          |
| Commission Setup              |
| Deposit System → Agent        |

#### 💼 Agent Workflow
| Step                          |
|-------------------------------|
| Agent Login                   |
| Deposit Agent → Customer      |

#### 👤 Customer Workflow
| Step                                      |
|-------------------------------------------|
| Deposit System → Customer                 |
| Customer Login                            |
| Withdraw Customer → Agent                 |
| Send Money (Customer → Customer)          |
| Payment (Customer → Merchant)             |
| Balance Check                             |
| Transaction History                       |
| Transaction Details                       |

### 🔐 Identified Security Issues

#### 🚨 Vulnerability Summary
| Issue                            | Severity       |
|----------------------------------|----------------|
| Improper RBAC                    | 🔴 Critical    |
| Token Misuse Across Roles        | 🔴 Critical    |
| Secret Key Validation Weakness   | 🟠 High        |

#### 1️⃣ Improper Role-Based Access Control
| Test Scenario                          | Expected       | Actual          |
|----------------------------------------|----------------|-----------------|
| Customer creates Virtual Money         | ❌ Access Denied | ✅ Access Allowed |
| Customer creates Commission            | ❌ Access Denied | ✅ Access Allowed |
| Customer performs Admin operations     | ❌ Access Denied | ✅ Access Allowed |

#### 2️⃣ Token Misuse Across Roles
| Endpoint                  | Expected Token | Actual Working Token |
|---------------------------|----------------|----------------------|
| Deposit System → Agent    | `admin_token`  | `customer_token`     |

> **Backend only checks if token exists — not who it belongs to.**

#### 3️⃣ Secret Key Validation Weakness
| Components Used                          | Result                     |
|------------------------------------------|----------------------------|
| `customer_token` + `AUTH_SECRET_KEY` + `AUTH-SECRET-KEY-SYSTEM` | Full privileged access |

**Server-side role/permission enforcement completely missing.**

### ⚠️ Security Impact
| Impact Area                     |
|---------------------------------|
| Privilege Escalation            |
| Unauthorized Fund Creation      |
| Commission Manipulation         |
| Financial System Abuse          |
| Compromised System Integrity    |

### ✅ Recommendations
| Recommendation                                      |
|----------------------------------------------------|
| Implement strict Role-Based Access Control (RBAC)  |
| Validate role in middleware for every endpoint    |
| Enforce token-role mapping validation              |
| Separate Admin and System privileges completely    |
| Prevent cross-role token usage                     |

### 🎯 What This Project Demonstrates
| Capability                                    |
|-----------------------------------------------|
| End-to-End API Automation                     |
| Advanced Postman Scripting                    |
| Multi-Role Financial Workflow Testing         |
| Dynamic Environment Variable Handling         |
| Real-World Security & Authorization Testing   |

### 🚀 How to Run
| Step | Action                                      |
|------|---------------------------------------------|
| 1    | Clone repository                            |
| 2    | Import Collection & Environment into Postman|
| 3    | Select the Environment (top-right)          |
| 4    | Run via **Collection Runner**               |
| ✅   | Everything executes automatically           |

### 👩‍💻 Author
| Name             | Profile                                          |
|------------------|--------------------------------------------------|
| Mahmuda Ferdus   | [github.com/MahmudaFerdus](https://github.com/MahmudaFerdus) |

