# Threat Model Table

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