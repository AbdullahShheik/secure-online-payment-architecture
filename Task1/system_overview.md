# 1. System Overview
The Online Payment Processing Application facilitates the customers to perform secure online payments to registered merchants.

# 2. Application Components

## Web Frontend
A browser based user interface that allows customers and merchants to initiate payments, view transaction history, and manage their accounts.

## API Backend
The API backend contains the core business logic of the application. It processes client requests, applies authorization rules, checks payment workflows, and communicates with external services such as the payment gateway and banking system.

## Authentication Service
The authentication service is responsible for verifying user identities, and applying login security policies.

## Admin Portal
A restricted interface used by system administrators to manage users, merchants, and system configurations. Access to this component will be strictly controlled.

## User Database
The user database stores customer profile information and authentication data. 

## Merchant Database
The merchant database maintains merchant registration details and account status.

## Transaction Database
The transaction database stores payment records, transaction states and administrative actions record.

## Payment Gateway
The payment gateway is an external third-party service that performs payment authorization and processing.

## Core Banking System
The core banking system is an external financial infrastructure responsible for interbank fund transfers.

# 3. Users and Roles

## Customers
Customers are external users who initiate and track payments through the web frontend.

## Merchants
Merchants are external businesses who receive and track payments through the web frontend. 

## System Administrators
System administrators are privileged internal users responsible for user administration.

## External Systems
The payment gateway and core banking system act as external system actors.

## Threat Actors
This system assumes the presence of both external attackers attempting unauthorized access and insider threats from malicious internal users.

# 4. Data Types Handled
- Personal Information
- Authentication Credentials
- Session Tokens
- Payment Transaction Data
- Merchant Data
- Records for administrative activities

# 5. External Dependencies
- The payment gateway
- core banking system

# 6. Trust Boundaries
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


