# 04 Architecture

## Components
| Component | Technology      | Role |
|-----------|-----------------|------|
| Android   | Kotlin (native) | Mobile client |
| iOS       | Swift (native)  | Mobile client |
| Backend   | .NET Core API in C#, EF Core as ORM | Serves passages, authors, works and connections |
| Database  | PostgreSQL      | Source of truth, schema defined first |

## How they fit together
Both apps talk to the one backend through the contract in `03-api-contract.md`.
The MVP ships the backend and the Android client first. The iOS client follows after validation and is based on the Android version.
The backend owns all data. The apps hold no business rules the other app
would need to duplicate.

## Databases
- One database is the source of truth. After launch, that is production (D-045).
- New rows are created only in the source-of-truth database. Other databases only receive copies.
- Other databases are created from dumps of the source-of-truth database. Rows with sensitive data are mocked instead of copied.
- UUIDs stay the same across databases unless exceptions apply.

TODO: hosting, auth, caching, offline behaviour, backend project structure,
repository layout for the three codebases.

## Open questions
- One repo or several?
- Where does connection logic live (database, backend)?
