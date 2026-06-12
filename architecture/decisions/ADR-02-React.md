# ADR-02: Adoption of React for Web Dashboard Development

Date: 2026-06-12
Status: Accepted

## Context
The CivilCore system requires a web-based portal for Managers to set up projects, import/manage the Bill of Quantities (BOQ), and review asset requests, as well as a high-level progress dashboard for Project Owners. The interfaces require complex, dynamic data rendering, such as tracking project completion percentages and materials used versus budgets, which need to update responsively without full page reloads.

## Decision
We will use **React** as the primary frontend framework for developing the Manager and Owner web applications.

## Rationale
React's component-based architecture allows us to build reusable UI elements (e.g., data tables, BOQ forms, and progress charts) which speeds up development. Its virtual DOM ensures fast rendering of large data sets, directly satisfying our performance requirement for dashboards to calculate and display overall project progress without noticeable lag (NFR-PER-03).

## Alternatives Considered
| Alternative | Pros | Cons | Reason Rejected |
|-------------|------|------|-----------------|
| Angular | Comprehensive enterprise-level framework; strict TypeScript enforcement. | Steep learning curve and heavier boilerplate. | The 4-month development timeline is too short to accommodate the learning curve compared to the team's familiarity with React. |
| Vue.js | Very lightweight; highly intuitive. | Smaller ecosystem for complex data visualization libraries compared to React. | React offers better out-of-the-box charting libraries required for the Owner's cost vs. budget overview. |

## Consequences
*   **Positive:** Fast, responsive UI; extensive ecosystem for dashboard components and charts.
*   **Negative:** Requires managing application state externally (e.g., via Redux or Context API) which adds architectural complexity.

## References
*   CivilCore Project Brief - Platforms & User Roles
*   SRS Section 5 (NFR-PER-03)