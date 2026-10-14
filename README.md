# RailGroup: Group Seat Booking Extension

> Book train seats **together with your group**, and optionally pay extra to choose your exact seats.

**Status:** Planning / early prototype in progress. This is a student project using simulated train data. It is **not affiliated with Indian Railways or IRCTC** and does not connect to their systems(yet).

---

## Problem

When a group books train tickets, the seats it gets are often scattered across a coach or even different coaches. Passengers who want to sit with their group have no way to ask for it, and those who care about specific seats have no option to choose them.

## Concept

1. **Register a group request:** pick train, date, class and group size, then add the passengers.
2. **Queue and allocate:** requests are queued and processed after a short **processing window**. An allocation algorithm seats the group together (same coach, adjacent seats where possible).
3. **Confirmation:** after allocation, the group sees the confirmed seats.
4. **Premium seat selection (optional):** passengers with preferences can pay an extra fee to pick exact seats from a seat map. Seats are locked briefly during selection to prevent double booking.

## Planned features

* [ ] User accounts and login
* [ ] Simulated trains, coaches and seat layouts
* [ ] Group request registration and queue
* [ ] Batch allocation with a contiguous-seat algorithm and fallback
* [ ] Confirmation view and notifications
* [ ] Premium seat selection with seat locking and a mock payment
* [ ] Admin: manage trains and coaches, run or schedule allocation
* [ ] Booking history and cancellation before allocation

## Open design questions

* **Fairness:** should premium seat selection be limited to a share of each coach, so group allocation isn't starved? (Proposed: configurable quota.)
* **Group size limit:** configurable maximum (default to be decided).
* **Partial allocation:** when no contiguous block exists, split across the fewest possible adjacent blocks, or waitlist?

## Tech stack

| Layer         | Choice                                                                        |
| ------------- | ----------------------------------------------------------------------------- |
| Frontend      | React                                                                         |
| Backend       | Node.js + Express REST API                                                    |
| Relational DB | **MySQL**: users, trains, coaches, seats, requests, bookings, locks, payments |
| Document DB   | **MongoDB**: train schedules and booking event logs                           |
| Auth          | JWT, bcrypt                                                                   |
| Testing       | Jest, Supertest                                                               |
| Tooling       | Git, GitHub, Jira (project management), draw.io (UML diagrams)                |

MySQL is planned to manage transactional booking data, seat availability and allocation. MongoDB will store train schedule documents and booking event logs. Seat allocation is designed to use MySQL transactions, row-level locking (`SELECT ... FOR UPDATE`) and appropriate database constraints to prevent conflicting seat assignments. Payment is **mocked** in this prototype.

## Documentation (software engineering artefacts)

| Document                                     | Contents                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| [docs/SRS.md](docs/SRS.md)                   | Requirements analysis: FR/NFR, user stories, use cases                   |
| [docs/DESIGN.md](docs/DESIGN.md)             | Class design (CRC), allocation algorithm, sequence and activity diagrams |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | Architecture style, component and deployment diagrams, data model        |
| [docs/TESTING.md](docs/TESTING.md)           | Test plan including concurrency tests                                    |
| [ROADMAP.md](ROADMAP.md)                     | Agile roadmap, sprint plan, Kanban board, definition of done             |

## Progress

* [ ] Sprint 0: Setup and SRS
* [ ] Sprint 1: Design and scaffolding
* [ ] Sprint 2: Core backend (allocation and locking)
* [ ] Sprint 3: Frontend and integration
* [ ] Sprint 4: Testing, quality, deployment
* [ ] Sprint 5: Final documentation and demo

## Getting started

Setup instructions will be added after the initial project structure, environment configuration, database migrations and development scripts are in place.

## Credits

Idea suggested by Dr. Pooja Shah, PDEU. Built by Krishna Patel.
