# ADR-01: Adoption of Flutter for Mobile Application Development

Date: 2026-06-12
Status: Accepted

## Context
The CivilCore system requires a mobile application for field supervisors to submit daily reports, asset requests, and log site issues [3, 4]. The supervisors operate in harsh construction environments, often with poor network connectivity, requiring robust offline capabilities to cache reports and photos until a connection is restored [5]. Additionally, the application must be accessible on both iOS and Android devices [6]. 

## Decision
We will use *Flutter* (with Dart) as the primary cross-platform framework for developing the supervisor mobile application [6].

## Rationale
Flutter provides a single codebase for both iOS and Android, which satisfies our maintainability requirements (NFR-MNT-01). It allows for rapid UI development with high-contrast, large touch targets suitable for outdoor construction environments (NFR-USA-02). Furthermore, Flutter possesses robust local storage ecosystem support (e.g., SQLite or Hive), which is critical for reliably caching daily reports and heavy geo-tagged photos when the device operates in an offline mode (NFR-REL-01) [5].

## Alternatives Considered
| Alternative | Pros | Cons | Reason Rejected |
|-------------|------|------|-----------------|
| Native iOS/Android (Kotlin & Swift) | Maximum performance, native UI feel. | Requires two separate development teams and two codebases. | Not technically or economically feasible given the strict 4-month development phase timeline. |
| React Native | Uses JavaScript (familiar to the React web team), cross-platform. | Relies on native bridges which can impact performance; UI consistency can vary across OS versions. | Flutter's custom UI rendering engine guarantees pixel-perfect consistency across all devices, which reduces training overhead for non-technical site staff. |

## Consequences
*   *Positive:* Greatly reduced development and maintenance time; highly consistent UI across all devices.
*   *Negative:* The development team must familiarize themselves with the Dart programming language.
*   *Risk:* Managing heavy geo-tagged photo caching will require careful memory management to prevent app crashes on lower-end devices.