# Decisions

## D-001: MVP ships one client first
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP ships the backend and one native client first, and the second client follows after validation. iOS is based on the Android version.
- **Why:** none stated
- **Rejected options:** Both clients at once – none stated
- **Updated:** `docs/01-product.md` (MVP scope), `docs/04-architecture.md` (How they fit together)
- **See also:** D-005 (which client), D-007 (backend stack)

## D-002: Connections derived from shared attributes
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Connections between passages are derived from shared themes, motifs and emotions. In the MVP they are rudimentary, and a measure of overlap between passages is planned for later.
- **Why:** none stated
- **Rejected options:** Hand-curated links (optionally typed) – none stated
- **Updated:** `docs/01-product.md` (MVP scope, Left out of the MVP), `docs/02-data-model.md` (Connections, Relationships, Open questions)

## D-003: Customisable view out of the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP has one fixed design and no customisable view.
- **Why:** none stated
- **Rejected options:** Basic options such as font size and theme – none stated
- **Updated:** `docs/01-product.md` (Left out of the MVP)

## D-004: Work is an entity in the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work is a stored entity in the MVP, and authors and works are attached to passages.
- **Why:** none stated
- **Rejected options:** Source title as plain text on Passage – none stated
- **Updated:** `docs/02-data-model.md` (Entities, Relationships; removed "Deliberately left out"), `docs/01-product.md` (Left out of the MVP)
- **Note:** This reverses the earlier "deliberately left out" decision in `docs/02-data-model.md` and `docs/01-product.md`. That decision had no log entry.

## D-005: Android client ships first
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The Android client ships first, and the iOS client follows, based on the Android version.
- **Why:** iOS is too restrained in ease of use.
- **Rejected options:** iOS first – too restrained in ease of use
- **Updated:** `docs/01-product.md` (MVP scope, Open questions), `docs/04-architecture.md` (How they fit together)

## D-006: Accounts, favourites, search, offline, social and personalisation
- **Date:** 2026-11-18
- **Status:** OPEN
- **Decision:** In or out of the MVP is undecided for each of these.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** none (the TODO stays in `docs/01-product.md`)

## D-007: Backend stack
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The backend is a .NET Core API in C#, with EF Core as the ORM and PostgreSQL as the database.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/04-architecture.md` (Components, Open questions), `docs/03-api-contract.md` (header), `docs/02-data-model.md` (Status)
