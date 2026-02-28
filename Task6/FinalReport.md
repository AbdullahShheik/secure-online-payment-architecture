# 1. System Overview
The Online Payment Processing Application facilitates the customers to perform secure online payments to registered merchants.

## 1. Application Components

### Web Frontend
A browser based user interface that allows customers and merchants to initiate payments, view transaction history, and manage their accounts.

### API Backend
The API backend contains the core business logic of the application. It processes client requests, applies authorization rules, checks payment workflows, and communicates with external services such as the payment gateway and banking system.

### Authentication Service
The authentication service is responsible for verifying user identities, and applying login security policies.

### Admin Portal
A restricted interface used by system administrators to manage users, merchants, and system configurations. Access to this component will be strictly controlled.

### User Database
The user database stores customer profile information and authentication data. 

### Merchant Database
The merchant database maintains merchant registration details and account status.

### Transaction Database
The transaction database stores payment records, transaction states and administrative actions record.

### Payment Gateway
The payment gateway is an external third-party service that performs payment authorization and processing.

### Core Banking System
The core banking system is an external financial infrastructure responsible for interbank fund transfers.

## 2. Users and Roles

### Customers
Customers are external users who initiate and track payments through the web frontend.

### Merchants
Merchants are external businesses who receive and track payments through the web frontend. 

### System Administrators
System administrators are privileged internal users responsible for user administration.

### External Systems
The payment gateway and core banking system act as external system actors.

### Threat Actors
This system assumes the presence of both external attackers attempting unauthorized access and insider threats from malicious internal users.

## 3. Data Types Handled
- Personal Information
- Authentication Credentials
- Session Tokens
- Payment Transaction Data
- Merchant Data
- Records for administrative activities

## 4. External Dependencies
- The payment gateway
- core banking system

## 5. Trust Boundaries
The architecture defines multiple trust boundaries where the level of trust changes between components.

**Internet to Front end:**  
This boundary separates untrusted public users from the web frontend and admin portal. It prevents direct exposure of internal services to the internet.

**Front end to API Backend:**  
This boundary ensures that only validated and well-formed requests from the frontend are processed by backend services.

**API Backend to Database:**  
This boundary restricts direct database access and ensures that sensitive data is accessed only through authorized backend components.

**API Backend to Payment Gateway:**  
This boundary protects communication between the internal system and the external payment processor.

**API Backend to Core Banking System:**  
This boundary secures financial communications with external banking infrastructure.

**Administrative Access:**  
This boundary separates privileged administrative operations from normal user activities.

![High-Level Architecture Diagram](Task1\OnlinePaymentSystemDesign.drawio.png)

# 2. Asset Inventory

| Asset | Description | Location | Security Objective |
|------|-------------|----------|-----------------|
| User Credentials | Customer and merchant login credentials including passwords| Authentication Service, User Database, Merchant Database | Confidentiality |
| Admin Credentials | Privileged administrator authentication data | Authentication Service, Admin Portal | Confidentiality |
| Session Tokens | Active user session identifiers| Web Frontend, API Backend | Confidentiality |
| Personal Information | Customer personal data such as name, email, phone, and address | User Database | Confidentiality |
| Merchant Data | Merchant registration details | Merchant Database | Integrity |
| Payment Transaction Data | Payment details including payer, payee, and amount | Transaction Database | Integrity |
| Business Logic | Core payment processing workflows | API Backend | Availability |
| Administrative records | all administrative activity records | API Backend | Accountability |
| Payment Processing Availability | Ability of the system to process payments in real time | API Backend, External Integrations | Availability |

# Justification for above mapping

Assets involving authentication, financial transactions, and privileged access require the highest levels of confidentiality and integrity. Availability is marked high for payment processing components for real time service. Accountability is must for administrative actions to support non-repudiation.

# 3. Threat Model

| ID | Threat Scenario | STRIDE | Affected Part | Impact | Risk | Risk Reasoning |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| **T1** | Attackers trying thousands of leaked passwords to get in. | Spoofing | Web Frontend | Unauthorized access to user accounts. | **High** | Very easy to automate the process. |
| **T2** | Stealing a merchant's account | Spoofing | Merchant Portal | Loss of merchant funds. | **High** | Leads to direct theft of business profits. |
| **T3** | Staff gaining "Admin" power | Elevation | Admin Portal | Attacker can change system settings or view all restricted customer data. | **Med** | Harder to do from outside, but dangerous if threat is from inside. |
| **T4** | Changing the prices of items | Tampering | API Backend | Significant financial loss due to users buying products below cost. | **High** | Simple to do and it can causes instant money loss. |
| **T5** | Skipping the login screen | Spoofing | Authorization Service | Complete system takeover by bypassing all security checks. | **Crit** | It will cause total failure as attacker will get complete access. |
| **T6** | Stealing the user database | Information Disclosure | User DB | Massive loss of user data. | **High** | There will Huge legal fines for leaking private info. |
| **T7** | Sneaking into the Database | Tampering | Databases | Massive loss of data. | **High** | Hackers will steal or delete data. |
| **T8** | Someone looking at private merchant business plans. | Information Disclosure | Merchant DB | Massive loss of merchant's market and future plans. | **Med** | Bad for privacy, but there will not be instant cash loss. |
| **T9** | Changing payment history | Tampering | Transaction DB | Corrupted records. | **High** | It will destroy our records of who owns what. |
| **T10** | Spying on card numbers in transactions | Information Disclosure | Payment Gateway | Financial fraud. | **High** | It can cause instant cash loss. |
| **T11** | Changing where the bank sends the final money | Tampering | Core Bank | Direct theft of large scale funds. | **Crit** | This is the worst case scenerio, massive theft. |
| **T12** | Deleting security logs from administrative actions | Repudiation | System Logs | Complete loss of system logs, no way to prove a crime happened. | **Med** | Makes it impossible to catch the attacker. |

![High-Level Architecture Diagram](Task3\SecureOnlinePaymentThreatModel.jpeg)

# 4. Security Controls

| Control Category | Security Control | Justification |
|------------------|------------------------|--------------------------|
| Identity & Access Management | Multi-Factor Authentication | Reduces risk of password guessing. |
| Identity & Access Management | Account Lockout After Failed Attempts | Stops brute-force login attacks. |
| Network Security | Firewall with Basic Rules | Blocks unauthorized external access to internal systems. |
| Network Security | IP Whitelisting for Admin Access | Ensures only approved locations can access admin accounts. |
| Network Security | Separate Internal and Guest Networks | Prevents outsiders from accessing core business systems. |
| Data Protection | Regular Offline Backups | Protects against data loss. |
| Data Protection | Data Masking | Limits exposure of sensitive information like card numbers. |
| Secrets Management | Regular Password & Key Rotation | Reduces impact if credentials are leaked. |
| Monitoring & Logging | Login Alerts for Suspicious Activity | Detects unusual login attempts quickly. |
| Monitoring & Logging | Daily Log Review | Helps identify suspicious behavior early. |

![High-Level Architecture Diagram](Task4\SecurityControlsThreatModel.jpeg)

# 5. Risk Treatment

| ID | High-Risk Threat | Strategy | Action Taken |
| ---- | ---- | ---- | ---- |
| **T1** | Attackers trying thousands of leaked passwords | **Mitigate** | Implementing Multi Factor Authentication (MFA) on the login page. |
| **T2** | Stealing a merchant's account | **Mitigate** | Enforcing strong password policies and MFA for all merchant portals. |
| **T4** | Changing the prices of items | **Mitigate** | Performing server side validation to ensure the checkout price matches the product database. |
| **T5** | Skipping the login screen | **Mitigate** | Rotating the "Tokens" and keys used between the Authentication Service and API Backend, we make it much harder for an attacker to use an old or forged token to skip the login. |
| **T6** | Stealing the user database | **Mitigate** | Use AES-256 encryption for the database and store keys in a secure Vault. |
| **T7** | Sneaking into the Database | **Mitigate** | Use firewalls. |
| **T9** | Changing payment history | **Mitigate** | Use the Transaction Database daily logs review and Offline Backup Storage to ensure any changes can be detected and reverted. |
| **T10** | Spying on card numbers in transactions | **Transfer** | Send requests directly to the Payment Gateway which uses Data Masking to ensure the API Backend never sees raw card numbers. |
| **T11** | Changing where the bank sends the final money | **Mitigate** | Use IP Whitelisting on the Admin Portal within the Core Banking System to approve all fund transfers. |

# Residual Risk Explanation

Residual risk is the risk that remains after we have applied our security controls. For example in our payment system, the following risk still persists:

1. **Third-Party dependency:** Since we **Transfer** the risk of card data (T10) to an external payment gateway, we become dependent on their security.















