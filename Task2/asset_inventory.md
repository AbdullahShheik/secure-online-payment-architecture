
# Asset Inventory Table

| Asset | Description | Location | Confidentiality | Integrity | Availability | Accountability |
|------|-------------|----------|-----------------|-----------|-------------|---------------|
| User Credentials | Customer and merchant login credentials including passwords| Authentication Service, User Database, Merchant Database | High | High | Medium | High |
| Admin Credentials | Privileged administrator authentication data | Authentication Service, Admin Portal | High | High | Medium | High |
| Session Tokens | Active user session identifiers| Web Frontend, API Backend | High | High | Medium | High |
| Personal Information | Customer personal data such as name, email, phone, and address | User Database | High | Medium | Low | Medium |
| Merchant Data | Merchant registration details | Merchant Database | High | High | Medium | Medium |
| Payment Transaction Data | Payment details including payer, payee, and amount | Transaction Database | High | High | High | High |
| Business Logic | Core payment processing workflows | API Backend | Medium | High | High | Medium |
| Administrative records | all administrative activity records | API Backend | Medium | High | Medium | High |
| Payment Processing Availability | Ability of the system to process payments in real time | API Backend, External Integrations | Low | High | High | High |

# Justification for above mapping

Assets involving authentication, financial transactions, and privileged access require the highest levels of confidentiality and integrity. Availability is marked high for payment processing components for real time service. Accountability is must for administrative actions to support non-repudiation.
