# 2. Overall Description

## 2.1 Product Perspective
The CivilCore system is an independent, cloud-based software solution designed to replace complex legacy tools like Primavera P6 for daily construction site management. The system operates across two primary interfaces: a mobile application for on-site field use and a web-based dashboard for office administration. Both platforms communicate with a central REST API backend and a MySQL database. The system is entirely self-contained for daily operational tracking but relies on cloud storage for managing project documents and geo-tagged site photos.

## 2.2 User Classes and Characteristics
The system caters to three distinct user personas:
*   **Supervisor (Mobile App User):** Construction field workers who operate on-site. They require a highly intuitive, simplified interface as they operate in harsh environments, often with protective gear and under time constraints. Their primary technical need is a fast daily reporting workflow (under 5 minutes) and the ability to operate offline when deep inside construction zones.
*   **Manager / QS (Web App User):** Office-based project managers or Quantity Surveyors who use desktop browsers. They possess moderate technical proficiency and require detailed dashboards to set up projects, import Bill of Quantities (BOQ) data, manage schedules, and monitor daily progress and budgets without making phone calls.
*   **Owner (Web App User):** Executive stakeholders who require high-level visibility. Their technical interaction is minimal; they need a strictly read-only, cross-project dashboard to monitor overall progress, cost versus budget, and critical delay alerts.

## 2.3 Operating Environment
*   **Mobile Application:** Developed in Flutter, required to run on modern iOS and Android smartphone devices.
*   **Web Application:** Developed using React, accessible via standard desktop web browsers (Chrome, Edge, Firefox, Safari).
*   **Backend Subsystem:** A REST API (Node.js) hosted on a cloud environment.
*   **Database & Storage:** MySQL for relational data mapping (Projects, Tasks, Reports) and Cloud Object Storage for media and document libraries.
*   **Network Environment:** The web application assumes a stable broadband connection. However, the mobile application explicitly assumes an unstable or non-existent cellular data connection on-site, requiring local caching and background auto-sync capabilities.

## 2.4 Design and Implementation Constraints
*   **Time constraint:** The UI/UX must be optimized so that a Supervisor can submit a complete daily report in under 5 minutes.
*   **Technology stack:** The system must utilise Flutter for the mobile application and MySQL for the database.
*   **Scope limitations:** The system design must strictly avoid incorporating complex resource levelling, financial accounting, invoicing, or vendor procurement modules, keeping the focus entirely on daily site tracking.
*   **Hardware limitations:** The mobile application must efficiently compress geo-tagged photos to accommodate bandwidth constraints during background synchronization.

## 2.5 Assumptions and Dependencies
*   **Device Access:** It is assumed that all field Supervisors have access to a smartphone equipped with a functional camera and GPS module for geo-tagging.
*   **Local Storage:** It is assumed that Supervisors' mobile devices have sufficient available local storage to securely cache daily reports, asset requests, and photos during offline mode.
*   **Data Availability:** Subcontractor details and agreed-upon quotations are assumed to be pre-existing and entered into the system prior to supervisors logging subcontractor work.

