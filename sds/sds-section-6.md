## 6. Interface Design

### 6.1 External Interfaces
The CivilCore system integrates with external cloud infrastructure to manage operations that fall outside the scope of the primary relational database. 

*   **AWS S3 REST API:** The Node.js backend interfaces directly with AWS S3 (or an equivalent cloud storage provider) via the official AWS SDK to securely handle heavy binary files. This external API is invoked via HTTPS to upload, store, and retrieve geo-tagged site photos captured by supervisors during daily reporting and snag logging. Additionally, this interface supports the project's document library, allowing managers to upload and access large project files such as architectural drawings, subcontractor quotations, and Bill of Quantities (BOQ) files.

### 6.2 Internal Module Interfaces
The system's Client-Server architecture relies on strictly defined internal boundaries to ensure data integrity and platform decoupling.

*   **RESTful Backend API:** The central Node.js backend exposes a stateless, structured REST API that serves as the exclusive communication hub for the system. All data exchange between the Flutter mobile application, the React web dashboards, and the MySQL database occurs through these JSON-over-HTTPS endpoints. 
*   **Data Exchange Format:** The internal modules communicate strictly using lightweight JSON payloads. This ensures that the complex relational data—such as nested arrays of BOQ tasks, labour hours, and utilized materials—is transmitted efficiently over low-bandwidth mobile networks.
*   **Endpoint Routing:** Internal communication is logically organized around core domain entities utilizing standard HTTP methods (GET, POST, PUT). For example, the mobile application transmits end-of-day progress via the `/api/v1/reports` endpoint, while the web application fetches real-time portfolio metrics for the Owner dashboard via the `/api/v1/projects/dashboard` endpoint.
