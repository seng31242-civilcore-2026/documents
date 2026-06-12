# ADR-04: Adoption of MySQL for Primary Relational Database

Date: 2026-06-12
Status: Accepted

## Context
CivilCore relies heavily on structured, interconnected data. A Daily Report is linked to specific Tasks, which are derived from BOQ line items, which in turn belong to specific Projects. This highly relational data must be stored securely and retrieved efficiently to calculate aggregate project progress.

## Decision
We will use **MySQL** as our primary relational database management system.

## Rationale
Although the client brief suggested PostgreSQL, MySQL is fully capable of handling the highly relational data structures (Projects, Tasks, Reports, Assets) defined in the system scope. MySQL provides robust ACID compliance ensuring data integrity when supervisors submit multi-part daily reports. The decision to select MySQL over PostgreSQL is driven by the development team's deep existing expertise, which drastically reduces database setup and maintenance risks during the tight SENG 34213 development phase.

## Alternatives Considered
| Alternative | Pros | Cons | Reason Rejected |
|-------------|------|------|-----------------|
| PostgreSQL | Advanced features; explicitly suggested in the client brief. | Slightly higher operational complexity. | Team expertise in MySQL is higher, and MySQL fully satisfies all CivilTrack relational data requirements without the overhead of learning a new engine. |
| MongoDB | Highly flexible schema; easy to scale horizontally. | NoSQL format is poorly suited for strict relational mappings (e.g., BOQ to Tasks to Subcontractors). | The project’s core logic requires strict relational integrity (ACID), making a document store inappropriate. |

## Consequences
*   **Positive:** Highly reliable relational data storage; rapid development due to team familiarity.
*   **Negative:** Deviates slightly from the initial client suggestion, requiring this formal justification to the review panel.

## References
*   CivilCore Project Brief - Key Data Entities
*   SRS Section 5 (NFR-SCA-01)