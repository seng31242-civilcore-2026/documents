# ADR-03: Adoption of Node.js for Backend REST API

Date: 2026-06-12
Status: Accepted

## Context
The CivilCore system requires a decoupled backend API to serve both the Flutter mobile application and the React web dashboards. This API must handle synchronized data payloads (Daily Reports containing multiple tasks, labour hours, and materials) being submitted simultaneously by multiple field supervisors at the end of the working day.

## Decision
We will use **Node.js** (with a framework like Express) to build the central REST API.

## Rationale
Node.js uses an event-driven, non-blocking I/O model, making it exceptionally lightweight and efficient for handling high volumes of concurrent requests. This directly addresses our scalability requirement (NFR-SCA-01) for processing multiple end-of-day report submissions. Additionally, it allows the team to use a unified JavaScript/TypeScript ecosystem across both the web frontend (React) and the backend, reducing context-switching.

## Alternatives Considered
| Alternative | Pros | Cons | Reason Rejected |
|-------------|------|------|-----------------|
| Django (Python) | Excellent built-in admin panel and ORM; fast to scaffold. | Heavier footprint; synchronous by default. | The team prefers the asynchronous nature and full-stack JavaScript alignment of Node.js. |
| Laravel (PHP) | Highly mature ecosystem; great out-of-the-box features. | PHP is less aligned with the team's current skill set. | Training overhead for PHP is too high for the given timeline. |

## Consequences
*   **Positive:** High concurrency handling; unified language (JavaScript/TypeScript) across web and backend.
*   **Negative:** Asynchronous callback/promise handling can lead to complex code if not strictly managed.

## References
*   CivilCore Project Brief - Tech Stack
*   SRS Section 5 (NFR-SCA-01)