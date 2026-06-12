## 8. Non-Functional Design Decisions

### 8.1 Reliability and Offline Capabilities
The system architecture explicitly addresses the requirement for supervisors to operate and fill out reports without an active internet connection. The Flutter mobile application integrates local storage to securely cache daily report data, including completed BOQ tasks, labour hours, and geo-tagged photos. A background synchronization manager monitors the device's network state, automatically pushing the cached data to the backend API once connectivity is restored.

### 8.2 Performance
Performance is optimized across both the data entry and data visualization workflows:
*   **Field Reporting:** To satisfy the strict success criterion that a supervisor can submit a complete daily report in under 5 minutes on their mobile device, the application logic and UI are designed to minimize text entry, utilizing rapid selections for BOQ tasks and materials.
*   **Dashboard Rendering:** The Owner dashboard must aggregate progress and cost-versus-budget data across all active projects. The Node.js backend processes these heavy read operations using concurrent queries, while the React web application efficiently renders the resulting metrics and alerts without interface lag.

### 8.3 Scalability
The system is designed to handle concentrated spikes in traffic, particularly when multiple supervisors submit heavy daily reports (containing arrays of tasks, materials, and geo-tagged photos) at the end of the working day. The backend REST API leverages the non-blocking I/O model of Node.js to efficiently process these simultaneous payload submissions without performance degradation.

### 8.4 Usability
As a lightweight alternative to complex enterprise tools like Primavera P6, the system prioritizes ease of use. The mobile application is tailored for the physical constraints of a construction site, focusing on a streamlined reporting flow that requires a minimal learning curve for field teams.

### 8.5 Maintainability
By utilizing Flutter for the mobile application, the system achieves true cross-platform capability for both iOS and Android devices from a single unified codebase. This architectural decision significantly reduces the ongoing maintenance burden and ensures feature parity across all supervisor devices.
