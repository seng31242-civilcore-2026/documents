# 3. System Analysis

## 3.1 Fact-Gathering Techniques Used
During the requirements elicitation phase, the following formal fact-finding techniques were employed to gather system requirements:
*   **Structured Interviews:** Conducted with key stakeholders to understand daily site operations and project management workflows. This included interviews with a Field Supervisor and a Manager.
*   **Document Analysis:** Reviewed sample Bill of Quantities (BOQ) documents (including standard Excel estimation templates and finalised physical printouts) to determine the exact data structure needed to map BOQ line items into trackable system tasks.

## 3.2 Existing System Analysis
The client's team currently relies on Primavera P6 for project management, alongside physical spreadsheets and paper-based printouts. 
**Key Pain Points Identified:**
*   **Overwhelming Complexity:** Primavera P6 is too complex and feature-heavy for daily field use, presenting a steep learning curve for on-site staff.
*   **Lack of Mobility:** Field supervisors lack a dedicated mobile-friendly tool to submit their daily progress directly from the construction site.
*   **Manual Progress Tracking:** Managers currently struggle to track daily site progress and calculate overall completion against the BOQ without making multiple phone calls to the site.
*   **Inefficient Issue Resolution:** Site problems (snags) and asset requests are often communicated informally, leading to delays and a lack of centralized tracking.

## 3.3 Use Case Diagram
*(Please refer to `diagrams/use-case-diagram.svg` in `documents` repo for the visual representation).*

The system boundary encompasses both the Mobile Application and the Web Application. The primary actors interacting with the system are:
*   **Supervisor:** Operates within the mobile app boundary (submitting reports, requesting assets, logging subcontractor work, logging issues).
*   **Manager / QS:** Operates within the web app boundary (setting up projects, manually entering BOQs, approving requests, viewing progress dashboards).
*   **Owner:** Operates within the web app boundary (utilising a read-only, cross-project dashboard).

## 3.4 Use Case Descriptions
The detailed step-by-step descriptions, including main flows, alternative flows, and business rules for all system use cases, are documented individually in the `srs/use-cases/` directory in `documents` repo. The identified system use cases are:
*   **UC-01:** Submit Daily Report
*   **UC-02:** Setup Project and Manual BOQ Entry
*   **UC-03:** Submit Asset Request
*   **UC-04:** Review Asset Request 
*   **UC-05:** View Progress Dashboard
*   **UC-06:** View Owner Dashboard
*   **UC-07:** Log Subcontractor Work
*   **UC-08:** Report Site Issue
*   **UC-09:** Record Material Delivery
*   **UC-10:** Sync Offline Data

## 3.5 Activity Diagrams
Activity diagrams illustrating the main and alternative workflows (including offline caching decision nodes and data validation loops) have been modelled using PlantUML. The exported SVGs and source files are available in the `diagrams/` directory in `documents` repo .
Key modelled workflows include:
*   `act-UC-01.svg`: Submit Daily Report
*   `act-UC-02.svg`: Setup Project and Manual BOQ Entry
*   `act-UC-03.svg`: Submit Asset Request
*   `act-UC-05.svg`: View Progress Dashboard
*   `act-UC-06.svg`: View Owner Dashboard
