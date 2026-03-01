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


#	Vulnerability	Severity	Status	What Actually Happens 
1	Zero RBAC Enforcement	:  A normal Customer can print unlimited money<br>Yes, you read that right. They just send one request with their customer_token → the server happily creates billions for them.<br>Same as giving every customer the central bank's printing machine — on steroids.
2	Cross-Role Token Misuse	: Customer token = Admin token<br>Endpoints that scream "Admin only!" in the docs actually accept customer_token without complaining.<br>Real example: "Deposit System → Agent" works perfectly with customer token → Customer can silently fund any account like a god — forever.
3	Secret Key Validation Completely Broken	: Just paste 3 lines and become God<br>Take your customer_token + the two "super secret" keys from the environment → send → Instant full Admin + System access.<br>No 2FA. No questions. No logs. Just god mode unlocked in 1 click.
🔥 Real-World Attack Scenarios (What an attacker can do in < 2 minutes)

Attack Scenario	Possible?	Outcome
Become a billionaire	YES	Create unlimited virtual money → withdraw or transfer anywhere
Set commission to 0% or 100%	YES	Steal every single transaction fee in the system
Fund any user without permission	YES	Deposit billions into friends/hackers accounts silently
Bypass all limits & KYC	YES	Transfer $1B+ in one click → no alerts
Complete system takeover	YES	The entire bank now belongs to any registered customer
Bottom Line (in big bold letters):

This is not a bug.
This is a bank with the vault door wide open and the keys taped to the front desk.

Any customer who runs this Postman collection instantly becomes the owner of the entire financial platform.



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
