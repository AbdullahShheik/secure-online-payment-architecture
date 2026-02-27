
# Asset Inventory Table

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
