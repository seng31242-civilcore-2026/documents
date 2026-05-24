# 5. Non-Functional Requirements

This section specifies the non-functional requirements (NFRs) that define the system's quality attributes, performance constraints, and architectural characteristics.

## 5.1 Performance
*   **NFR-PER-01:** The mobile application UI/UX must be optimized to ensure that a Supervisor can complete and submit a full daily report (including tasks, materials, labour, weather, and photos) in under 5 minutes.
*   **NFR-PER-02:** The mobile application must efficiently compress geo-tagged photos before uploading to minimize bandwidth usage and speed up synchronization times from the field.
*   **NFR-PER-03:** The Manager and Owner web dashboards must quickly aggregate and calculate overall project progress (comparing daily reports against BOQ quantities) without noticeable lag, ensuring managers can view today's progress immediately without making phone calls.

## 5.2 Security
*   **NFR-SEC-01:** The system shall enforce strict Role-Based Access Control (RBAC). Specifically, the "Owner" role must be restricted to read-only permissions across all projects, preventing them from modifying tasks, schedules, or BOQ files.
*   **NFR-SEC-02:** All data transmitted between the web application, mobile application, and the central REST API must be encrypted using secure protocols (e.g., HTTPS/TLS) to protect project data and credentials.
*   **NFR-SEC-03:** The system must securely isolate project documentation and files within the cloud storage to prevent unauthorized direct access.

## 5.3 Usability
*   **NFR-USA-01:** The system must serve as a lightweight, focused alternative to Primavera P6. The interface must be highly intuitive, specifically avoiding complex resource-levelling or financial accounting screens to eliminate steep learning curves for site staff.
*   **NFR-USA-02:** The mobile application must feature large touch targets and high-contrast visuals, accommodating Field Supervisors who may be operating outdoors in bright sunlight or wearing protective gear.

## 5.4 Reliability
*   **NFR-REL-01:** The mobile application must provide robust offline capabilities. It must reliably cache data locally on the device when operating in construction zones with zero cellular connectivity.
*   **NFR-REL-02:** The system must automatically and reliably resume background synchronization of cached reports, photos, and asset requests the moment internet connectivity is restored, ensuring zero data loss.

## 5.5 Scalability
*   **NFR-SCA-01:** The system's central database (MySQL) and REST API backend must be capable of handling concurrent daily report submissions from multiple supervisors across multiple active projects at the end of the working day.
*   **NFR-SCA-02:** The system must utilize scalable cloud object storage to manage an infinitely growing library of high-resolution site photos, BOQ files, and architectural drawings without degrading database performance.

## 5.6 Maintainability
*   **NFR-MNT-01:** The mobile application must be built using Flutter to maintain a single codebase for both iOS and Android devices, reducing future maintenance overhead.
*   **NFR-MNT-02:** The backend architecture must expose a decoupled REST API (Node.js) allowing the Web (React) and Mobile (Flutter) clients to be updated and maintained independently.
