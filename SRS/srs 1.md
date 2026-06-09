# 1. Introduction

## 1.1 Purpose and Scope
**Purpose:**
The purpose of this Software Requirements Specification (SRS) is to define the functional and non-functional requirements for the CivilCore system. This system is designed as a simplified construction site management application for civil engineering teams, serving as a lightweight, user-friendly alternative to complex software like Primavera P6 . The primary goal is to provide supervisors, managers, and owners with a focused tool to track daily site work, materials, and overall project progress efficiently.

**Scope:**
The CivilTrack system consists of a mobile application (built with Flutter) for on-site Supervisors, and a web application for Managers and Owners. 
The core capabilities of the system include:
*   **Daily Reporting:** Enabling Supervisors to quickly log completed tasks, materials, labour hours, weather, and geo-tagged photos in under 5 minutes.
*   **Project Setup & BOQ Integration:** Allowing Managers to set up projects, define simple Gantt-style schedules, and map Bill of Quantities (BOQ) line items directly to trackable tasks.
*   **Asset & Issue Management:** Facilitating material/equipment requests from Supervisors and logging site snags with photos for Manager resolution .
*   **Progress Dashboards:** Providing Managers with automated overall completion tracking against the BOQ, and giving Owners a read-only, high-level summary across all active projects.
*   **Offline Functionality:** Allowing Supervisors to complete reports without an internet connection, with automatic background synchronization when connectivity is restored.

**Out of Scope:**
The system explicitly will NOT include complex resource leveling (Primavera P6-style), financial accounting, invoicing, procurement, or vendor management functionalities.

## 1.2 Definitions, Acronyms, Abbreviations
*   **BOQ (Bill of Quantities):** A document containing the list of work items and their planned quantities, which the system converts into trackable tasks.
*   **Snag / Issue:** A physical problem or defect observed on the construction site that is flagged by a Supervisor using a geo-tagged photo for a Manager to resolve and close.
*   **Gantt Schedule:** A visual project timeline consisting of planned start and end dates for each activity.
*   **SRS:** Software Requirements Specification.
*   **Owner:** A stakeholder who views cross-project progress and costs in a strictly read-only capacity.

## 1.3 Overview of Document
The remainder of this SRS document is structured as follows:
*   **Section 2: Overall Description** provides a high-level overview of the system context, user personas, operating environment, and system constraints.
*   **Section 3: System Analysis** contains the fact-finding summaries, system boundary diagrams, use case descriptions, and activity diagrams detailing the system workflows.
*   **Section 4: Functional Requirements** enumerates the specific, testable functionalities the system must provide, traced back to our use cases.
*   **Section 5: Non-Functional Requirements** outlines the performance, security, reliability, scalability, and usability constraints of the system.
*   **Section 6: Alternative Solutions & Feasibility Study** evaluates different technical approaches and assesses the technical, economic, and operational feasibility of our recommended solution.
