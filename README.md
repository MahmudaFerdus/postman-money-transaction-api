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
