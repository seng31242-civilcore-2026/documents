## 1. Introduction

### 1.1 Purpose
The primary purpose of this Software Design Specification (SDS) is to establish the complete architectural and detailed system design for the **CivilCore** application. CivilCore is a simplified construction site management application designed specifically for civil engineering teams to replace overly complex tools like Primavera P6. This document translates the business needs and user constraints defined in the Software Requirements Specification (SRS) into a concrete technical blueprint. It will serve as the core reference document for the development team during the upcoming SENG 34213 development phase, providing exact specifications for system components, database schemas, and interface boundaries. 

### 1.2 Scope
The scope of this design covers the entire CivilCore software ecosystem. The system is designed for three distinct user roles: Owners, Managers, and Supervisors. To serve these users, the design details the architecture of the following components:
*   A **cross-platform mobile application** built using **Flutter** specifically for on-site Supervisors.
*   A **web-based dashboard** built using **React** for Managers and project Owners.
*   A central **RESTful backend API** built with **Node.js** to handle system logic.
*   A **relational database (MySQL)** for strict data integrity, supplemented by **cloud object storage (S3)** to handle heavy geo-tagged site photos and project documents.

The system design encompasses core functionalities including daily reporting, Bill of Quantities (BOQ) tracking, asset requests, issue logging, and robust offline data synchronization. It explicitly excludes the design of complex resource levelling, vendor procurement, or financial accounting modules, as these are out of scope for the CivilCore product.

### 1.3 Definitions, Acronyms, and Abbreviations
*   **API:** Application Programming Interface, enabling communication between the frontend applications and the backend.
*   **BOQ:** Bill of Quantities, representing the imported list of work items and their planned quantities that supervisors will report against.
*   **JWT:** JSON Web Token, utilized for stateless user authentication and role-based access control.
*   **P6:** Primavera P6, the complex enterprise software that CivilCore is designed to replace.
*   **RBAC:** Role-Based Access Control, ensuring users can only access features permitted for their assigned role (Owner, Manager, Supervisor).
*   **SDS:** Software Design Specification.
*   **SRS:** Software Requirements Specification.

### 1.4 Overview of Document
*   **Section 2** provides a system overview and relationship to the SRS.
*   **Section 3** details the high-level Architectural Design, including the Component Diagram, Deployment Diagram, and formal Architectural Decision Records (ADRs) justifying the technology stack.
*   **Section 4** opens the "black box" of the system with Detailed Design elements, including the Class Diagram, Database Data Model, and Sequence Diagrams mapping the internal logic for all use cases.
*   **Section 5** outlines the UI Design through wireframes, navigation flow diagrams, and UX decisions.
*   **Sections 6, 7, and 8** finalize the design by specifying internal/external interfaces, security implementations (including OWASP mitigations), and how the system satisfies Non-Functional Requirements.
