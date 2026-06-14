## 4. Detailed Design

### 4.1 Database and Data Model Design

The CivilCore system utilizes a highly relational data model implemented in MySQL to ensure strict ACID compliance across all field reporting and management activities. The core entity of the system is the `Project`.

The primary entities and their relationships are structured as follows:

- **Project:** Stores overarching details including the project name, location, start and end dates, and the assigned team of supervisors. It acts as the root node for all other relational data.
- **Task:** Represents individual line items imported from the Bill of Quantities (BOQ). Each task is strictly linked to a single `Project` and contains the planned quantity, unit of measurement, and assigned rate.
- **Daily Report:** Represents a single end-of-day submission by a field supervisor. Each report is relationally mapped to the submitting `Supervisor` and the target `Project`. It contains the report date, weather conditions, logged labour hours (categorized by skilled and unskilled workers), and an array of geo-tagged site photo URLs.
- **TaskProgress (Join Table):** Maps the many-to-many relationship between a `Daily Report` and a `Task`. It records the exact quantity of work completed for a specific task on a specific day.
- **Asset Request:** Tracks requests for equipment or materials needed for upcoming work. It includes the requested item, quantity, needed date, and current approval status, linked to a specific `Project` and requesting `Supervisor`.
- **Issue:** Represents a snag or problem logged on-site. It contains a description, a photo URL (stored in S3), the reporting supervisor, and the resolution status.
- **Material Delivery:** An independent log tracking materials arriving on site, which is distinct from the materials actively used in daily reports. It records the item, quantity, delivery date, and supplier.

### 4.2 Class Diagram

The system class diagram formally defines the object-oriented structure of the backend application, outlining the attributes, methods, and visibility of all system entities. It models the core inheritance strategy where `Supervisor`, `Manager`, and `Owner` inherit from a base `User` class to handle authentication, while encapsulating the distinct methods available to each role.

![System Class Diagram](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/class-diagram/exported/Class%20Diagram/Class%20Diagram.svg)

_(Note: The source PlantUML file for this diagram is located at `documents/diagrams/class-diagram.puml`)_

### 4.3 Sequence Diagrams

The dynamic behaviour of the system is mapped through detailed sequence diagrams. These diagrams model the internal chronological interactions between the frontend UI components (React/Flutter), the Node.js API controllers, the MySQL database, and the S3 storage bucket for all 10 core use cases.

- **UC-01 Submit Daily Report:** Maps the flow of a supervisor selecting tasks, entering labour/materials, and capturing photos, terminating in a concurrent database insertion. ![ssd-uc-01](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-01.svg)
- **UC-02 Setup Project:** Details the manager's process of initializing a project and iterating through a BOQ import to generate individual `Task` records. ![ssd-uc-02](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-02.svg)
- **UC-03 Asset Request:** Illustrates the two-part asynchronous workflow: the supervisor's initial submission and the manager's subsequent approval or rejection. ![ssd-uc-03](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-03.svg)
- **UC-04 Progress Monitoring:** Models the manager dashboard querying the API to calculate overall project completion percentages and budget variances dynamically. ![ssd-uc-04](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-04.svg)
- **UC-05 Subcontractor Tracking:** Shows the assignment of a specific subcontractor to a BOQ task and linking the agreed quotation. ![ssd-uc-05](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-05.svg)
- **UC-06 Owner Dashboard:** Demonstrates the heavy, concurrent global read queries required to aggregate progress and calculate budget alerts across all active projects. ![ssd-uc-06](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-06.svg)
- **UC-07 Issue / Snag Logging:** Maps the flow of a supervisor uploading an issue photo to S3, saving the URL to MySQL, and the manager later resolving the snag. ![ssd-uc-07](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-07.svg)
- **UC-08 Material Delivery Log:** Details the independent process of logging arriving materials and supplier information to the database. ![ssd-uc-08](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-08.svg)
- **UC-09 Document Library:** Illustrates a manager uploading PDFs/DWGs to the S3 bucket and storing the metadata references in the database. ![ssd-uc-09](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-09.svg)
- **UC-10 Offline Data Sync:** Maps the background process where the mobile app detects network restoration and systematically flushes the local SQLite cache to the Node.js API. ![ssd-uc-10](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/detailed-sequence-diagrams/exported/ssd-uc-10.svg)

### 4.4 State Machine Diagrams

To manage the lifecycle of mutable data, the system strictly enforces state transitions on two critical entities within the Node.js controllers:

1.  **Asset Requests Lifecycle:**
    - `Draft` (Optional: Saved locally on the mobile device during offline mode).
    - `Pending` (Persisted to the MySQL database and visible to the Manager).
    - `Approved` or `Rejected` (Terminal states triggered by Manager intervention).
2.  **Issue (Snag Log) Lifecycle:**
    - `Open` (Triggered upon supervisor submission; alerts the manager).
    - `Resolved` (Terminal state triggered once the manager confirms the physical issue is fixed).
