## 3. Architectural Design

### 3.1 Architecture Pattern
The CivilCore system implements a decoupled **Client-Server Architecture** operating via a stateless RESTful backend. This pattern was selected over a monolithic architecture to enforce a strict separation of concerns between the user interfaces and the core business logic. 

**Justification referencing Quality Attributes:**
*   **Scalability:** By decoupling the client applications from the server, the central Node.js REST API can be scaled horizontally and independently to handle high volumes of concurrent requests, such as the "end-of-day rush" when multiple supervisors submit heavy daily reports simultaneously.
*   **Maintainability:** The frontend applications (Flutter for mobile, React for web) and the backend API exist in separate repositories and deployment pipelines. This allows the web and mobile development teams to work in parallel without causing merge conflicts or deployment bottlenecks, directly supporting the tight 4-month development timeline.
*   **Reliability:** A stateless REST API architecture simplifies the implementation of the strict offline-mode requirements. Since the backend does not hold active session states for the mobile client, the Flutter app can seamlessly cache data locally in SQLite when the network drops, and safely push these complete JSON payloads to the API once connectivity is restored.

### 3.2 Technology Stack & Justifications
Every major component selected below has been formally evaluated against alternatives. The detailed rationales, alternatives considered, and accepted trade-offs for these decisions are fully documented in the project's **Architectural Decision Records (ADRs)** located in the `documents/architecture/decisions/` repository.

*   **Mobile Application: Flutter (Dart)**
    *   *Decision:* Adopted to build the field supervisor mobile application for both iOS and Android.
    *   *Justification:* Flutter allows for a single, unified cross-platform codebase, drastically reducing the maintenance overhead. Its custom rendering engine guarantees pixel-perfect UI consistency across various mobile devices, ensuring the large touch targets required for site supervisors function reliably.
    *   *Reference:* [ADR-01-Flutter.md](https://github.com/seng31242-civilcore-2026/documents/blob/main/architecture/decisions/ADR-01-Flutter.md)
*   **Web Application: React (JavaScript)**
    *   *Decision:* Adopted to build the web-based dashboards for Managers and Owners.
    *   *Justification:* The Manager and Owner dashboards require complex, data-heavy visualizations (such as Gantt-style schedules and dynamic budget tracking). React’s Virtual DOM provides highly efficient rendering of these large datasets without noticeable UI lag, directly addressing our performance requirements.
    *   *Reference:* [ADR-02-React.md](https://github.com/seng31242-civilcore-2026/documents/blob/main/architecture/decisions/ADR-02-React.md)
*   **Backend API: Node.js (Express)**
    *   *Decision:* Adopted to build the central RESTful API.
    *   *Justification:* Node.js utilizes an asynchronous, non-blocking I/O model. This is exceptionally efficient for handling multiple concurrent network requests, making it the ideal framework to process the heavy, simultaneous data payloads submitted by field supervisors at the end of their shifts.
    *   *Reference:* [ADR-03-NodeJS.md](https://github.com/seng31242-civilcore-2026/documents/blob/main/architecture/decisions/ADR-03-NodeJS.md)
*   **Primary Database: MySQL**
    *   *Decision:* Adopted as the primary relational database management system. 
    *   *Justification:* While PostgreSQL was suggested in the initial client brief, the team explicitly pivoted to MySQL. The system requires strict ACID compliance to securely manage the highly relational data (Projects containing Tasks, which belong to Daily Reports). MySQL provides this necessary data integrity, and the development team possesses deep, existing expertise in the MySQL engine, significantly reducing technical risk during the development phase.
    *   *Reference:* [ADR-04-MySQL.md](https://github.com/seng31242-civilcore-2026/documents/blob/main/architecture/decisions/ADR-04-MySQL.md)
*   **File Storage: AWS S3 (Cloud Object Storage)**
    *   *Decision:* Adopted for handling heavy binary files.
    *   *Justification:* To keep the relational database performant and lightweight, MySQL will only store metadata and file URLs. The actual binary blobs for geo-tagged site photos, issue logs, and project documents (DWG/PDF files) will be pushed directly to AWS S3 via the backend API.

### 3.3 Component Diagram
The following Component Diagram illustrates the high-level logical architecture of the CivilCore system. It maps the distinct software packages (Mobile App, Web App, REST API, Database, and S3 Storage) and traces the JSON-over-HTTPS interfaces connecting them.

![Component Diagram](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/component-diagram/exported/Component%20Diagram.svg)

*(Note: The source PlantUML file for this diagram is located at `diagrams/component-diagram/`)*

### 3.4 Deployment Diagram
The Deployment Diagram models the physical infrastructure topology of the CivilCore system. It demonstrates where each software artefact executes in the production environment, tracking the flow from the Supervisor's physical iOS/Android device in the field to the cloud-hosted Application and Database servers.

 ![Deployment Architecture](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/deployment-diagram/exported/Deployment%20Diagram.svg)

*(Note: The source PlantUML file for this diagram is located at `diagrams/deployment-diagram/`)*
