# 💰 Money Transaction API  
### Fully Automated Postman Collection + Critical Security Audit

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=flat-square&logo=postman&logoColor=white)
![Automated](https://img.shields.io/badge/Automation-100%25_Sequential-brightgreen?style=flat-square)
![Security](https://img.shields.io/badge/Security-Critical_Vulnerabilities-red?style=flat-square)

**One-click end-to-end testing** of a complete digital wallet system with real privilege escalation exploits discovered live.

---

### 📄 Live API Documentation  
🔗 [View Full Interactive Docs](https://documenter.getpostman.com/view/22815578/2sBXcAH2jZ)

---

### 👥 Roles & Capabilities (Fully Simulated)

| Role       | Icon | Key Capabilities                                                                 |
|------------|------|-----------------------------------------------------------------------------------|
| Admin      | 🛡️   | Create users, generate virtual money, set commissions, system deposits           |
| Agent      | 💼   | Deposit money from system/agent → customer                                        |
| Customer   | 👤   | Withdraw, P2P transfer, pay merchants, check balance & history                    |
| Merchant   | 🏪   | Receive payments from customers                                                   |

---

### ⚙️ Base Configuration (Pre-filled in Environment)

| Variable                  | Value                                      |
|---------------------------|--------------------------------------------|
| `base_url`                | `https://mta.newroztech.com/api`           |
| `auth_secret_key`         | `e97b4ca15fd2b3086c1e4af98b72d503`          |
| `secret_key_system`       | `b82439df1c92a7fe504bf23da918e6f1`          |

---

### 🌍 Environment Variables (Smart & Automatic)

| Type                  | Variables Automatically Captured                                                                 |
|-----------------------|--------------------------------------------------------------------------------------------------|
| Manually Set          | `base_url`, `auth_secret_key`, `secret_key_system`                                              |
| Auto-Generated (Scripts) | `admin_token` · `agent_token` · `customer_token` · `merchant_token` <br> `customer_id` · `agent_id` · `merchant_id` <br> `balances` · `transaction_id` · `withdraw_fee` |

**Zero manual token copying** – Everything flows automatically via `pm.environment.set()` & `postman.setNextRequest()`

---

### 🔄 Full Automated Flow (Runs Sequentially)

| Step | Workflow                                                                                  |
|------|-------------------------------------------------------------------------------------------|
| 1    | Admin Login → Create Customer/Agent/Merchant → Create Virtual Money → Set Commission     |
| 2    | System Deposit → Agent → Agent Deposit → Customer                                        |
| 3    | Customer Login → Withdraw → Send Money (P2P) → Pay Merchant → Balance & History Checks   |

All executed in perfect order using Collection Runner.

---

### 🔐 Critical Security Vulnerabilities Discovered

| # | Vulnerability                        | Severity       | Status     | Details                                                                 |
|---|--------------------------------------|----------------|------------|-------------------------------------------------------------------------|
| 1 | Improper RBAC                        | 🔴 Critical    | Exploitable | Customer token can create virtual money & set commissions               |
| 2 | Cross-Role Token Misuse              | 🔴 Critical    | Exploitable | `customer_token` works on Admin/System endpoints                        |
| 3 | Weak Secret Key Validation           | 🟠 High        | Exploitable | Combining user token + global secrets = full privilege escalation      |

**Real Impact:** Unlimited money creation, commission manipulation, total system takeover.

---

🔐 Critical Security Vulnerabilities Discovered


#	Vulnerability	Severity	Status	What It Means (Plain English)
1	Improper Role-Based Access Control (RBAC)	🔴 Critical	Exploitable	The system is supposed to say: "Only Admin can create money!"<br>But in reality, a normal Customer can use their own token and create unlimited virtual money. This is like giving a regular shopper the bank manager's key.
2	Cross-Role Token Misuse	🔴 Critical	Exploitable	Some endpoints are meant to work only with admin_token or system token.<br>But they also accept customer_token!<br>Example: The "Deposit System → Agent" endpoint should reject customer token → it accepts it and works perfectly.<br>Result: A customer can act like an Admin without anyone noticing.
3	Weak Secret Key Validation	🟠 High	Exploitable	The API has two secret keys that are supposed to be super secret (AUTH_SECRET_KEY & AUTH-SECRET-KEY-SYSTEM).<br>If a customer simply copies their own token + these two secrets into the request, they instantly get full Admin + System privileges.<br>No password, no verification — just paste and gain god mode.
Real-World Impact (What an attacker can actually do)
Attack Scenario	Possible?	Result
Create unlimited virtual money	Yes	Can make themselves billionaire in seconds
Change commission rates to 0% or 99%	Yes	Steal all transaction fees or make everything free for themselves
Deposit money into any account	Yes	Can fund any customer/agent/merchant without permission
Bypass all payment limits	Yes	Transfer millions without any restriction
Take over the entire financial system	Yes	Full control — the bank basically belongs to the attacker now
Bottom line:
This is not a small bug.
This is a complete authorization breakdown.
Any registered customer can become the owner of the entire system in less than 2 minutes using just this Postman collection.

That’s why all three issues are rated Critical/High — they allow total compromise of the money transaction platform.

---

### 🎯 What This Project Proves

| Skill Demonstrated                              |
|-------------------------------------------------|
| End-to-end API automation                       |
| Advanced Postman scripting & dynamic variables  |
| Multi-role financial workflow simulation        |
| Real-world authorization bypass testing         |
| Automated security vulnerability discovery      |

---

### 🚀 How to Run (Takes 30 seconds)

| Step | Action                                               |
|------|------------------------------------------------------|
| 1    | Clone this repo                                      |
| 2    | Import **Collection** + **Environment** into Postman |
| 3    | Select the environment (top-right)                   |
| 4    | Click **Run** in Collection Runner → Watch magic     |

Everything runs automatically. No manual steps.

---

### 👩‍💻 Author

**Mahmuda Ferdus**  
Security-Minded QA Automation Engineer  
[![GitHub](https://img.shields.io/badge/GitHub-MahmudaFerdus-black?style=flat-square&logo=github)](https://github.com/MahmudaFerdus)

> **Purpose:** Advanced automation practice + real security research  
