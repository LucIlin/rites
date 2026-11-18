# Decisions

## D-001: Work excluded from the MVP
- **Date:** 2026-11-18
- **Status:** SUPERSEDED by D-002
- **Decision:** Work is not a stored entity in the MVP.
- **Why:** The model should not centre on the whole work.
- **Rejected options:** none stated
- **Updated:** none (this records the stance that 01-product.md and 02-data-model.md already held)

## D-002: Thin Work in the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP keeps Work with only ID, Name and AuthorID. The rest of Work's columns are added in v1.0.
- **Why:** none stated
- **Rejected options:** Drop Work from the MVP – none stated; full Work in the MVP – none stated
- **Updated:** 01-product.md (Left out of the MVP); 02-data-model.md (MVP schema, Deliberately left out)

## D-003: Text.Translator NULL means the original
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** A Text with Translator NULL is the original. A translation by an unknown translator stores `Unknown`. A Passage has at most one original.
- **Why:** none stated
- **Rejected options:** Original identified by language – none stated; IsOriginal flag column – none stated
- **Updated:** 02-data-model.md (Text)

## D-004: Anonymous works use an `Anonymous` Author
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work.AuthorID stays NOT NULL. Anonymous works point to a seeded Author row named `Anonymous`.
- **Why:** none stated
- **Rejected options:** Nullable Work.AuthorID – none stated
- **Updated:** 02-data-model.md (Author, Work)

## D-005: PassageTag.Strength is a decimal from 0 to 1
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Strength is DECIMAL(3,2), with 0 < Strength <= 1.
- **Why:** none stated
- **Rejected options:** Integer 1–5 – none stated; integer 1–10 – none stated
- **Updated:** 02-data-model.md (PassageTag)

## D-006: Work creation date stored as a year range
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work.DateOfOrigin is replaced by CreationYearStart and CreationYearEnd.
- **Why:** To support a range of possible years in which a work may have been created.
- **Rejected options:** Single DateOfOrigin column – cannot hold a range
- **Updated:** 02-data-model.md (Work)

## D-007: Work.OriginalLanguage removed
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** Work has no OriginalLanguage column.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** 02-data-model.md (Work, Deliberately left out)

## D-008: Passage to Text is zero-or-many
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** A Passage has zero or many Texts.
- **Why:** none stated
- **Rejected options:** One-or-many – none stated
- **Updated:** 02-data-model.md (Text, Relationships)

## D-009: No passage-connection system in the MVP
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The MVP has no system for connecting passages. A simple tag browser is built instead.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** 01-product.md (MVP scope, Left out of the MVP); 02-data-model.md (Connections)

## D-010: How passage connections work
- **Date:** 2026-11-18
- **Status:** OPEN
- **Decision:** Connections between passages are a planned system. It is still undecided whether they are typed or plain links, and whether they are derived from tags or stored.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** none

## D-011: Final list of Passage.Form values
- **Date:** 2026-11-18
- **Status:** OPEN
- **Decision:** The starting set is `verse`, `prose` and `drama`. The final list is not decided.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** none

## D-012: Database design source of truth
- **Date:** 2026-11-18
- **Status:** DECIDED
- **Decision:** The v1.0 and MVP schemas in 02-data-model.md are the source of truth for database design. They supersede all earlier data-model text.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** 02-data-model.md (rewritten in full)
