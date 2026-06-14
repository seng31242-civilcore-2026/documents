## 5. UI Design

### 5.1 Navigation Flow Diagram
The user interface navigation is strictly segregated by the system's Role-Based Access Control (RBAC). Upon authentication, the system automatically routes the user to the appropriate application interface based on their assigned role: Supervisors are directed to the mobile application's home screen, while Managers and Owners are directed to their respective web-based dashboards. 

The navigation flow diagram below maps the complete screen-to-screen routing and available user actions within each discrete interface.

*   ![Navigation Flow](https://github.com/seng31242-civilcore-2026/documents/raw/main/diagrams/navigation-flow/exported/navigation-flow.svg)
*(Note: The source PlantUML file for this diagram is located at `diagrams/navigation-flow/navigation-flow.puml`)*

### 5.2 Wireframes
The system features three primary user interfaces tailored to the workflows of the distinct user roles. The low-fidelity wireframes representing these core screens have been developed and exported to the prototypes repository.

*   **Supervisor Mobile Interface (Daily Report View):** Designed for the Flutter mobile app. This interface focuses on capturing the core daily metrics: completed BOQ tasks, labour hours (skilled and unskilled), utilized materials, weather conditions, and geo-tagged site photos. It explicitly includes UI controls for offline caching.

    ![Daily Report View](https://github.com/seng31242-civilcore-2026/prototypes/raw/main/wireframes/exported/wireframe-mobile-daily-report.svg)
*   **Manager Web Interface (Progress & Approvals View):** Designed for the React web application. This interface provides a comprehensive project overview, including a Gantt-style schedule. It highlights overall completion percentages against the BOQ, materials used versus the budget, and provides a consolidated view of pending daily reports, asset requests, and logged issues awaiting review.

    ![Progress & Approvals View](https://github.com/seng31242-civilcore-2026/prototypes/raw/main/wireframes/exported/wireframe-web-manager.svg)
*   **Owner Web Interface (Global Portfolio View):** A read-only dashboard designed to provide high-level visibility across all active projects. It aggregates cost-versus-budget data and highlights system-generated alerts for critical schedule delays or budget overruns.

![Global Portfolio View](https://github.com/seng31242-civilcore-2026/prototypes/raw/main/wireframes/exported/wireframe-web-owner.svg)

### 5.3 UX Decisions and Rationale
The user experience (UX) strategy for CivilCore was driven entirely by the need to provide a lightweight, mobile-friendly alternative to complex enterprise tools like Primavera P6, which the target users find too cumbersome for daily field use.

*   **Mobile App (Supervisors):** 
    *   **Speed & Efficiency:** To satisfy the strict success criterion that a daily report must be completed in under 5 minutes, the mobile UI heavily utilizes simple checkbox interactions for BOQ tasks rather than manual text entry.
    *   **Environmental Considerations:** The interface incorporates high-contrast typography to reduce glare in bright, outdoor site environments. Large touch targets are implemented to accommodate supervisors who may be wearing protective equipment or operating the device while walking the site.
    *   **Offline Transparency:** Given the requirement for offline capabilities, the UX explicitly informs the user of their network state. When offline, primary submission buttons dynamically shift to "Save to Cache," preventing user frustration from unexpected network timeouts.
*   **Web App (Managers and Owners):**
    *   **Data Density & Visualization:** The desktop interfaces leverage the available screen real estate to present dense project data clearly. Complex timelines are visualized using Gantt-style schedules.
    *   **Alert Hierarchy:** The Owner dashboard employs strict visual hierarchies (e.g., colour-coded warning banners) to immediately draw attention to critical project anomalies, such as material costs exceeding the baseline budget or weather-related schedule delays.
