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
- **Status:** SUPERSEDED by D-015
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

## D-008: Thin Work in the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP's Work has only ID, Name and AuthorID. The creation-year columns are added in v1.0. This refines D-004.
- **Why:** none stated
- **Rejected options:** Full Work in the MVP – none stated
- **Updated:** `docs/02-data-model.md` (Work, MVP schema), `docs/01-product.md` (Left out of the MVP)

## D-009: Text.Translator NULL means the original
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** A Text with Translator NULL is the original. A translation by an unknown translator stores `Unknown`. A Passage has at most one original.
- **Why:** none stated
- **Rejected options:** Original identified by language – none stated; IsOriginal flag column – none stated
- **Updated:** `docs/02-data-model.md` (Text)

## D-010: Anonymous works use an `Anonymous` Author
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work.AuthorID stays NOT NULL. Anonymous works point to a seeded Author row named `Anonymous`.
- **Why:** none stated
- **Rejected options:** Nullable Work.AuthorID – none stated
- **Updated:** `docs/02-data-model.md` (Author, Work)

## D-011: PassageTag.Strength is a decimal from 0 to 1
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Strength is DECIMAL(3,2), with 0 < Strength <= 1.
- **Why:** none stated
- **Rejected options:** Integer 1–5 – none stated; integer 1–10 – none stated
- **Updated:** `docs/02-data-model.md` (PassageTag)

## D-012: Work creation date stored as a year range
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work.DateOfOrigin is replaced by CreationYearStart and CreationYearEnd.
- **Why:** To support a range of possible years in which a work may have been created.
- **Rejected options:** Single DateOfOrigin column – cannot hold a range
- **Updated:** `docs/02-data-model.md` (Work)

## D-013: Work.OriginalLanguage removed
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work has no OriginalLanguage column.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Work, Deliberately left out)

## D-014: Passage to Text is zero-or-many
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** A Passage has zero or many Texts.
- **Why:** none stated
- **Rejected options:** One-or-many – none stated
- **Updated:** `docs/02-data-model.md` (Text, Relationships)

## D-015: No passage-connection system in the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP has no system for connecting passages. A simple tag browser is built instead. This supersedes D-002.
- **Why:** none stated
- **Rejected options:** Rudimentary derived connections in the MVP (D-002) – none stated
- **Updated:** `docs/01-product.md` (MVP scope, Left out of the MVP, Open questions), `docs/02-data-model.md` (Connections)

## D-016: How passage connections work
- **Date:** 2026-11-18
- **Status:** OPEN
- **Decision:** Connections between passages are a planned system. It is still undecided whether they are typed or plain links, and whether they are derived from tags or stored.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** none

## D-017: Final list of Passage.Form values
- **Date:** 2026-11-18
- **Status:** OPEN
- **Decision:** The starting set is `verse`, `prose` and `drama`. The final list is not decided.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** none

## D-018: Database design source of truth
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The v1.0 and MVP schemas in `docs/02-data-model.md` are the source of truth for database design. They supersede all earlier data-model text.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (rewritten in full)
