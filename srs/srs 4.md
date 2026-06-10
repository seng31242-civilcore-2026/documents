# 4. Functional Requirements

This section outlines the functional requirements for the CivilCore system. Each requirement is prioritized and traced back to its source use case to ensure complete coverage of the client's needs.

### 4.1 Field Operations (Supervisor App)

**ID:** FR-01
**Title:** Submit Daily Report
**Description:** The system shall allow a Supervisor to submit a daily report consisting of completed tasks (linked to the BOQ), materials used, labour hours logged, weather conditions, and geo-tagged site photos.
**Priority:** P1 - Critical
**Source:** Client Brief; UC-01
**Verification:** System Test (TC-FR-01)

**ID:** FR-02
**Title:** Submit Asset Request
**Description:** The system shall allow a Supervisor to submit a request for materials or equipment needed for the following working days, specifying the item, quantity, and required date.
**Priority:** P2 - High
**Source:** Client Brief; UC-03
**Verification:** Integration Test (TC-FR-02)

**ID:** FR-03
**Title:** Log Subcontractor Work
**Description:** The system shall allow a Supervisor to log specific work completed by subcontractors on a given day and link it to the subcontractor's agreed quotation.
**Priority:** P3 - Medium
**Source:** Client Brief; UC-07
**Verification:** System Test (TC-FR-03)

**ID:** FR-04
**Title:** Report Site Issue (Snag)
**Description:** The system shall allow a Supervisor to report a site issue or snag by capturing a geo-tagged photo and entering a description. The system shall set the initial status to "Open".
**Priority:** P2 - High
**Source:** Client Brief; UC-08
**Verification:** System Test (TC-FR-04)

**ID:** FR-05
**Title:** Record Material Delivery
**Description:** The system shall allow a Supervisor to record the arrival of materials on-site, capturing the item, quantity, delivery date, and supplier, which updates the inventory independently of daily usage.
**Priority:** P2 - High
**Source:** Client Brief; UC-09
**Verification:** System Test (TC-FR-05)

### 4.2 Project Management (Web App)

**ID:** FR-06
**Title:** Project Setup and Manual BOQ Entry
**Description:** The system shall allow a Manager to create a new project, assign Supervisors, define a Gantt-style schedule, and manually input Bill of Quantities (BOQ) line items to generate trackable tasks.
**Priority:** P1 - Critical
**Source:** Client Brief; UC-02
**Verification:** Integration Test (TC-FR-06)

**ID:** FR-07
**Title:** Review Asset Requests
**Description:** The system shall allow a Manager to view pending asset and material requests submitted by Supervisors and update their status to "Approved" or "Rejected".
**Priority:** P2 - High
**Source:** Client Brief; UC-04
**Verification:** System Test (TC-FR-07)

**ID:** FR-08
**Title:** Calculate Progress Dashboard
**Description:** The system shall automatically calculate and display the overall project completion percentage to the Manager by comparing the daily completed task quantities against the planned BOQ quantities.
**Priority:** P1 - Critical
**Source:** Client Brief; UC-05
**Verification:** Unit Test (TC-FR-08)

### 4.3 Executive Oversight (Web App)

**ID:** FR-09
**Title:** View Owner Dashboard
**Description:** The system shall provide Owners with a read-only dashboard summarizing progress across all active projects, cost versus budget, and active alerts for delays or budget overruns.
**Priority:** P2 - High
**Source:** Client Brief; UC-06
**Verification:** Integration Test (TC-FR-09)

### 4.4 System & Connectivity

**ID:** FR-10
**Title:** Offline Data Synchronization
**Description:** The mobile application shall cache daily reports, asset requests, and issue logs locally when operating without an internet connection, and automatically synchronize this data with the central database once a connection is restored.
**Priority:** P1 - Critical
**Source:** Client Brief; UC-10
**Verification:** Integration Test (TC-FR-10)
