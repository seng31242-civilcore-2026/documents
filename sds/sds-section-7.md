## 7. Security Design

### 7.1 Authentication and Authorisation Strategy
The CivilCore system employs a stateless authentication mechanism utilizing JSON Web Tokens (JWT). Upon successful login, the Node.js backend issues a cryptographically signed JWT containing the user's unique identifier and their assigned system role (`OWNER`, `MANAGER`, or `SUPERVISOR`). This token is stored securely on the client device and transmitted in the `Authorization` header of all subsequent API requests.

Authorisation is governed by strict, server-side Role-Based Access Control (RBAC). The backend API utilizes dedicated middleware on every protected route to verify the JWT signature and evaluate the user's role against the endpoint's required permissions. This architecture ensures, for example, that a Supervisor is technically blocked from accessing Manager-specific endpoints—such as approving asset requests or altering a project's Bill of Quantities (BOQ)—even if they attempt to bypass the mobile interface.

### 7.2 Data Protection
The system ensures data confidentiality and integrity both at rest and in transit:
*   **Data in Transit:** All communications between the Flutter mobile application, the React web dashboards, the Node.js API, and the external AWS S3 storage buckets are strictly encrypted using HTTPS/TLS 1.2 or higher. This prevents packet sniffing and man-in-the-middle attacks, which is especially critical when supervisors transmit data over unsecured or public networks near construction sites.
*   **Data at Rest:** Sensitive user credentials, specifically passwords, are never stored in plain text. They are irreversibly hashed and salted using the robust `bcrypt` algorithm before being persisted in the MySQL database. Furthermore, the AWS S3 buckets utilized for storing sensitive project documents (like subcontractor quotations) and geo-tagged site photos are secured using restrictive IAM (Identity and Access Management) policies to prevent unauthorised public access or direct URL enumeration.

### 7.3 Input Validation Strategy
To maintain data integrity and prevent malformed data from corrupting the MySQL database, the Node.js API implements rigorous server-side input validation. 

Given that the system relies on JSON payloads exchanged between decoupled clients and the server, middleware libraries (such as `Joi` or `express-validator`) are utilized to define strict validation schemas for every incoming API request. Any request originating from the mobile or web clients that contains missing fields, incorrect data types (e.g., submitting a string instead of a numerical float for BOQ quantities), or out-of-bound values is immediately intercepted and rejected with an HTTP 400 Bad Request response before the data ever reaches the core controller logic.

### 7.4 OWASP Top 10 Considerations
The system architecture systematically mitigates critical security risks identified in the OWASP Top 10 framework:
*   **Injection Flaws:** Completely mitigated by utilizing parameterized queries and a trusted Object-Relational Mapper (ORM) or Query Builder within the Node.js backend. This approach abstracts raw SQL commands, neutralizing the risk of SQL injection attacks against the MySQL database.
*   **Broken Access Control:** Directly addressed by the stateless JWT and RBAC middleware described in Section 7.1. By enforcing access rules on the server rather than relying on the client UI to hide elements, the system prevents privilege escalation.
*   **Security Misconfiguration:** Prevented by isolating all sensitive configuration data (such as database credentials, JWT secret keys, and AWS access keys) into environment variables (`.env`). This ensures secrets are never hardcoded into the source code repository, protecting the system even if the codebase is compromised.
