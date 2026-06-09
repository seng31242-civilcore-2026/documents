# 6. Alternative Solutions & Feasibility Study

## 6.1 Alternative Solutions Analysed

Before proposing the custom CivilCore system, the following alternative solutions were evaluated:

**Alternative 1: Continued Use and Customization of Primavera P6**
*   **Description:** Attempting to build custom mobile dashboards or simplify views within the client's existing Primavera P6 enterprise software.
*   **Pros:** The software is already licensed, and historical project data is retained within a single enterprise ecosystem. It contains highly advanced resource leveling capabilities.
*   **Cons:** The underlying system remains fundamentally too complex for field supervisors. It is not inherently mobile-friendly, lacks streamlined offline capabilities for harsh construction environments, and presents a steep learning curve that discourages daily use.

**Alternative 2: Generic Task Management Software (e.g., Asana, Monday.com)**
*   **Description:** Migrating site operations to off-the-shelf, cloud-based project management tools.
*   **Pros:** These tools have excellent, modern mobile applications, require minimal setup time, and are highly user-friendly.
*   **Cons:** They are completely domain-agnostic and lack construction-specific data structures. They cannot natively add  Bill of Quantities (BOQ) to calculate physical progress percentages, do not separate daily material usage from inventory delivery, and lack specialized workflows for subcontractor tracking and geo-tagged snag reporting.

## 6.2 Feasibility Study

**6.2.1 Technical Feasibility**
The proposed system is technically highly feasible. The selected technology stack (Flutter for cross-platform mobile, React for the web dashboard, Node.js for the REST API, and MySQL for the database) consists of mature, industry-standard frameworks. Managing geo-tagged photos and documents can be reliably handled by integrating standard cloud object storage. The team possesses the required skills to implement the background offline-sync architecture required by the mobile application.

**6.2.2 Economic Feasibility**
The project is economically feasible. By developing a custom, focused solution, the client can eliminate expensive, per-user enterprise licensing fees associated with software like Primavera P6 for their field staff. Operating costs will be restricted to predictable, scalable cloud hosting fees, which provide a high return on investment by significantly reducing manual data entry and manager phone calls.

**6.2.3 Operational Feasibility**
Operational feasibility is exceptionally high. Field supervisors actively desire a simplified, mobile-first alternative that allows them to submit reports in under 5 minutes without dealing with complex Gantt charting or resource leveling. Because the system maps directly to their current physical workflows (BOQ task tracking, asset requests, and issue logging), user adoption will be rapid and require minimal training.

**6.2.4 Schedule Feasibility**
The system scope has been strictly defined to exclude financial accounting, invoicing, procurement, and complex resource leveling. Because of these strict boundaries, designing the system within the 8-week SENG 31242 timeline and developing it within the subsequent 4-month SENG 34213 timeline is highly realistic and feasible.

## 6.3 Justified Recommendation

Based on the analysis above, we strongly recommend proceeding with the custom development of the **CivilCore system**. 

Neither continuing with Primavera P6 nor adopting generic task managers fulfills the dual need for operational simplicity in the field and construction-specific BOQ tracking in the office. CivilCore strikes the exact required balance: providing supervisors with a fast, offline-capable mobile tool for daily reporting, while giving managers and owners automated, BOQ-driven progress dashboards without the overhead of enterprise accounting software.
