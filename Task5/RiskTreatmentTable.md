# Task 5. Risk Treatment and Residual Risk

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