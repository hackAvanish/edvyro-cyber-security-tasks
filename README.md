# EdVyro Cyber Security Internship - Task 02

## 1. Threat-Model Diagram (Architecture & Data Flow)
- **External Entities (Users):** End-users accessing the web application via a standard web browser over HTTPS.
- **Trust Boundary 1 (Internet to Web Server):** Encrypted traffic hits a Reverse Proxy / WAF, routing requests to the Application Server.
- **Application Server:** Handles business logic, authentication (JWT/Session tokens), and input validation.
- **Trust Boundary 2 (App Server to Database):** Internal secure network segment communicating with a PostgreSQL/MySQL database and a Redis cache.

## 2. Risk Register using STRIDE

| Threat Category | Threat Description | Potential Impact | Target Asset |
| :--- | :--- | :--- | :--- |
| **Spoofing** | An attacker steals or forges session tokens / cookies to impersonate a legitimate user. | High | Authentication Module |
| **Tampering** | An attacker injects malicious SQL payloads into input fields to modify database records. | Critical | Database / User Records |
| **Repudiation** | A user performs a sensitive transaction, but insufficient audit logs make it impossible to trace. | Medium | Audit Logging System |
| **Information Disclosure** | API error messages expose stack traces, database schema details, or server paths. | High | API Endpoints |
| **Denial of Service (DoS)** | An attacker floods the login endpoint with automated requests, exhausting server resources. | High | Authentication Service |
| **Elevation of Privilege** | A standard user manipulates role parameters in an API request to gain administrator privileges. | Critical | User Access Control |

## 3. Prioritized Hardening Checklist
- [ ] **1. Input Validation & Sanitization (Prevents Tampering):** Implement strict server-side validation and use parameterized queries / ORM to completely block SQL Injection and XSS.
- [ ] **2. Secure Authentication & Session Management (Prevents Spoofing & Privilege Escalation):** Enforce multi-factor authentication (MFA), secure HTTP-only cookies, and proper RBAC checks on every API endpoint.
- [ ] **3. Rate Limiting & Bot Protection (Prevents DoS):** Apply rate limiting on high-risk endpoints like `/login` and `/password-reset`.
- [ ] **4. Error Handling & Logging (Prevents Information Disclosure & Repudiation):** Disable verbose debug error messages in production and ensure critical actions write to secure audit logs.
- [ ] **5. Transport Layer Security (TLS 1.3):** Ensure all data in transit is fully encrypted using strong SSL/TLS certificates.
