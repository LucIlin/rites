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
- **Status:** SUPERSEDED by D-026
- **Decision:** The MVP's Work has only ID, Name and AuthorID. The creation-year columns are added in v1.0. This refines D-004.
- **Why:** none stated
- **Rejected options:** Full Work in the MVP – none stated
- **Updated:** `docs/02-data-model.md` (Work, MVP schema), `docs/01-product.md` (Left out of the MVP)

## D-009: Text.Translator NULL means the original
- **Date:** 2026-11-18
- **Status:** SUPERSEDED by D-019
- **Decision:** A Text with Translator NULL is the original. A translation by an unknown translator stores `Unknown`. A Passage has at most one original.
- **Why:** none stated
- **Rejected options:** Original identified by language – none stated; IsOriginal flag column – none stated
- **Updated:** `docs/02-data-model.md` (Text)

## D-010: Anonymous works use an `Anonymous` Author
- **Date:** 2026-11-18
- **Status:** SUPERSEDED by D-027
- **Decision:** Work.AuthorID stays NOT NULL. Anonymous works point to a seeded Author row named `Anonymous`.
- **Why:** none stated
- **Rejected options:** Nullable Work.AuthorID – none stated
- **Updated:** `docs/02-data-model.md` (Author, Work)

## D-011: PassageTag.Strength is a decimal from 0 to 1
- **Date:** 2026-11-18
- **Status:** SUPERSEDED by D-020
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
- **Status:** SUPERSEDED by D-019
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

## D-019: Schema revision 2 adopted
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** The schema follows revision 2 of the ER diagram. Person replaces Author. PassageText (PassageID, WorkID, Content) replaces Text. Translations are stored as Works, with Language, TranslationOf and TranslatorID on Work.
- **Why:** none stated
- **Rejected options:** Revision 1 (Text with Translator and Language) – none stated
- **Updated:** `docs/02-data-model.md` (rewritten in full), `docs/05-build-plan.md` (Step 1)

## D-020: PassageTag.Strength dropped
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** PassageTag is a plain link table with only PassageID and TagID.
- **Why:** none stated
- **Rejected options:** Decimal Strength in (0, 1] (D-011) – none stated
- **Updated:** `docs/02-data-model.md` (PassageTag)

## D-021: Person.Nationality removed
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** Person has only PersonID, Name and Biography.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Person)

## D-022: Creation years are required
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** CreationYearStart and CreationYearEnd are NOT NULL. A Work with an unknown date stores an estimated range.
- **Why:** none stated
- **Rejected options:** Nullable years meaning unknown – none stated
- **Updated:** `docs/02-data-model.md` (Conventions, Work)

## D-023: Relay translations allowed
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** Work.TranslationOf may point to another translation, not only to an original.
- **Why:** none stated
- **Rejected options:** Translations of originals only – none stated
- **Updated:** `docs/02-data-model.md` (Work)

## D-024: Work.Language is the Work's own language
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** Every Work, original or translation, stores its own language as an ISO 639 code. This is not the original-language column removed in D-013.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Work)

## D-025: Enumerations stored as PostgreSQL enums
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** Passage.Form and Tag.Type are PostgreSQL enum types.
- **Why:** none stated
- **Rejected options:** CHECK IN lists – none stated
- **Updated:** `docs/02-data-model.md` (Conventions, Passage, Tag)

## D-026: MVP schema to be derived from revision 2
- **Date:** 2026-11-19
- **Status:** OPEN
- **Decision:** The old MVP schema (thin Work, D-008) is removed. A new MVP schema will be derived from revision 2.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (MVP schema), `docs/01-product.md` (Left out of the MVP)

## D-027: `unknown` Person for unknown authors and translators
- **Date:** 2026-11-19
- **Status:** SUPERSEDED by D-041
- **Decision:** A sentinel Person row named `unknown` stands for an unknown author or translator. A translation always has a TranslatorID, and an original never has one.
- **Why:** none stated
- **Rejected options:** Seeded `Anonymous` author (D-010) – none stated; NULL TranslatorID for unknown translators – none stated
- **Updated:** `docs/02-data-model.md` (Person, Work)

## D-028: Passage.OriginalWorkID added
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** Passage has a required OriginalWorkID that points to the original Work the passage comes from.
- **Why:** A cheaper way to check PassageTexts, and an easier starting point for querying Passages.
- **Rejected options:** Checking PassageTexts only through the TranslationOf chain – more expensive
- **Updated:** `docs/02-data-model.md` (Passage, Backend rules)

## D-029: Creation years of a translation
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** A translation's CreationYearStart and CreationYearEnd are the years the translation was made.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Work)

## D-030: Passages without text allowed
- **Date:** 2026-11-19
- **Status:** DECIDED
- **Decision:** A Passage may have zero PassageText rows.
- **Why:** Cheap, and a passage without text fails the mandatory checks anyway.
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Passage, Relationships)

## D-031: GUID primary keys, fixed in seed files
- **Date:** 2026-11-20
- **Status:** DECIDED
- **Decision:** Every table uses a UUID primary key, version 7 (`Guid.CreateVersion7()`). Catalog rows (Work, Passage, Person, Tag) get their GUIDs written into the seed files, and the database never creates them. The composite keys of PassageText and PassageTag are made of those GUIDs. A catalog row's GUID never changes once it has been seeded. A script may fill in missing GUIDs in the seed files once, and after that they are permanent.
- **Why:** The database is a read-mostly, seeded catalog, so the usual cost of GUIDs (index page splits on insert) doesn't apply; indexes can be rebuilt after a large seed if needed. Key size (16 bytes vs 4 or 8) is irrelevant at the expected scale. Seeded databases are rebuilt often, and GUIDs in the seed files keep each row's identity the same on every database. Seed files for different works can be prepared separately without coordinating ID ranges.
- **Rejected options:** Auto-increment IDs – they change when the seed order changes, which would break bookmarks, cached app data and shared links.
- **Trade-offs:** IDs are hard to read while debugging.
- **Updated:** `docs/02-data-model.md` (Conventions, Entities diagram, entity tables, Person seed), `docs/07-content-sourcing.md` (Loading)

## D-032: Language as a natural-key table
- **Date:** 2026-11-20
- **Status:** DECIDED (2026-11-23)
- **Decision:** Add a `Language` table keyed by a BCP 47 tag, with `Name` and `Direction` ('ltr'/'rtl'). `Work.Language` becomes a foreign key to `Language.Tag`. Every `lang` value in text JSON must exist in `Language` (checked by the backend). The tag format is defined in D-033.
- **Why:** Direction belongs to the script, not the language, so storing `Direction` once keeps backend, Android and iOS from deriving different answers. A table also stops well-formed but non-existent codes and gives the apps display names.
- **Rejected options:** Text column with a format check only (accepts non-existent codes; each platform derives direction on its own). Deriving direction from the language alone (fails for languages written in scripts with different directions).
- **Updated:** `docs/02-data-model.md` (Language table, Work.Language FK; remove from Open questions)

## D-033: Language tag format
- **Date:** 2026-11-23
- **Status:** DECIDED
- **Decision:** Language tags follow BCP 47: language (2–3 lowercase letters), optional script (4 letters, capitalised), optional region (2 uppercase letters or 3 digits), e.g. `en`, `grc`, `pt-BR`, `zh-Hant`. Tags use the shortest correct form; a script or region is added only when it changes something. Enforced by a format check on `Language.Tag`: `^[a-z]{2,3}(-[A-Z][a-z]{3})?(-([A-Z]{2}|[0-9]{3}))?$`
- **Why:** The previous check rejected region and script tags the data needs (`pt-BR`, `zh-Hant`). BCP 47 is what .NET, Android and iOS use, so tags pass through every layer unchanged. One canonical letter case stops `pt-BR` and `PT-br` from becoming two values.
- **Rejected options:** Bare ISO 639 codes only (can't express script or region).
- **Updated:** `docs/02-data-model.md` (Language.Tag constraint)

## D-034: Passage text format
- **Date:** 2026-11-22
- **Status:** OPEN
- **Decision:** Draft: `PassageText.Content` becomes a JSON document of blocks, lines and inline runs in Rites' own schema, based on TEI and stored in a `jsonb` column. It is versioned with `v`, verse is stored as lines and prose as paragraphs, and text is normalised to NFC. The draft is in `docs/08-passage-text-format.md`.
- **Why:** Other formats convert to it, so the database is source-agnostic. It keeps every detail the author used to convey meaning. Each verse line is a separate unit. It passes losslessly from PostgreSQL through the backend to both apps, because all three parse JSON natively. It supports as many languages as reasonable.
- **Rejected options:** XML or HTML – need extra parsers on mobile, and HTML also needs cleaning. Inline formatting as character positions – C#, Kotlin, Swift and PostgreSQL count characters differently, so positions disagree between platforms.
- **Updated:** `docs/08-passage-text-format.md` (new), `docs/02-data-model.md` (PassageText, Open questions), `CLAUDE.md` (Documentation layout), `.claude/skills/decision-log/SKILL.md` (Where decisions go)

## D-035: Notes in a separate list
- **Date:** 2026-11-22
- **Status:** DECIDED
- **Decision:** Notes in the passage text format are stored in a separate `notes` list at the end of the document, each with an `id` and a `by` (author, translator or editor). Runs point to a note with `note`, and a phrase spanning several runs or lines gives each of its runs the same id.
- **Why:** none stated
- **Rejected options:** Notes inline in the runs – none stated
- **Updated:** `docs/08-passage-text-format.md` (Notes)

## D-036: Stable line ids and line alignment
- **Date:** 2026-11-22
- **Status:** REJECTED
- **Decision:** Lines have no ids of their own, and lines are not aligned between an original and its translations. `n` stays only as the source line number.
- **Why:** Irrelevant to Rites.
- **Rejected options:** none stated
- **Updated:** `docs/08-passage-text-format.md` (Lines)

## D-037: Which marks the MVP draws
- **Date:** 2026-11-22
- **Status:** OPEN
- **Decision:** Undecided. The format can hold everything from day one, and anything an app does not draw shows as plain text. The proposal is to draw what the MVP content needs: stanzas, paragraphs, line breaks, indentation, italic, `lang`, split lines, and speakers and stage directions if drama passages are seeded.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/08-passage-text-format.md` (Open questions)

## D-038: No unknown language
- **Date:** 2026-11-22
- **Status:** DECIDED
- **Decision:** Rites has no unknown-language value. There is no `und` row in Language, and every Work's language is a real tag in Language.
- **Why:** The concept is far outside the scope of the app.
- **Rejected options:** `und` sentinel Language row – far outside the scope of the app
- **Updated:** `docs/02-data-model.md` (Conventions, Language seed data)
- **Note:** The `und` convention was added to `docs/02-data-model.md` in commit 174ae8f without a log entry.

## D-039: Multiple authors and translators per Work
- **Date:** 2026-11-23
- **Status:** DECIDED (2026-11-23)
- **Decision:** A Work can have several authors and several translators, stored as WorkContributor rows (D-040).
- **Why:** none stated
- **Rejected options:** One `AuthorID` and at most one `TranslatorID` on Work (revision 2) – none stated
- **Updated:** `docs/02-data-model.md` (Open questions, WorkContributor)

## D-040: Schema revision 3 adopted
- **Date:** 2026-11-23
- **Status:** DECIDED
- **Decision:** The schema follows revision 3 of the ER diagram. WorkContributor (WorkID, PersonID, Role `author`/`translator`) replaces `Work.AuthorID` and `Work.TranslatorID`. Every Work has at least one author row, translator rows exist only on Works with `TranslationOf` set, and a translation's author rows are copied from the Work it was translated from (backend). Contributors are shown sorted by name. Languages are seed data, added through seed files like the rest of the catalog.
- **Why:** none stated
- **Rejected options:** Revision 2 (single `AuthorID` and `TranslatorID` on Work) – none stated
- **Updated:** `docs/02-data-model.md` (Status, Conventions, Entities diagram, Person, Language, Work, WorkContributor, Relationships, Backend rules), `docs/05-build-plan.md` (Step 1), `docs/07-content-sourcing.md` (Loading)

## D-041: Translators and the `unknown` Person
- **Date:** 2026-11-23
- **Status:** DECIDED
- **Decision:** The sentinel Person row `unknown` stands for an unknown author or translator. Every translation has at least one translator row, and if the translator isn't known, the row points to `unknown`. A translation with no translator rows is an error, caught when the backend creates it and by the validation queries after seeding. This supersedes D-027.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Conventions, Person, Backend rules), `docs/07-content-sourcing.md` (Loading)

## D-042: Duplicate Works handled by seeding
- **Date:** 2026-11-23
- **Status:** DECIDED
- **Decision:** Work has no uniqueness rule. The seeding process handles possible duplicate Works.
- **Why:** none stated
- **Rejected options:** none stated
- **Updated:** `docs/02-data-model.md` (Work), `docs/07-content-sourcing.md` (Loading)
- **Note:** The line `UNIQUE NULLS NOT DISTINCT (AuthorID, Name, Language, TranslatorID)` was added to `docs/02-data-model.md` in commit 9e00352 without a log entry. It was never a decision and is removed.
