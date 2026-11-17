# 04 Architecture

## Components
| Component | Technology      | Role |
|-----------|-----------------|------|
| Android   | Kotlin (native) | Mobile client |
| iOS       | Swift (native)  | Mobile client |
| Backend   | .NET and C#     | Serves passages, authors and connections |
| Database  | Relational (engine TODO) | Source of truth, schema defined first |

## How they fit together
Both apps talk to the one backend through the contract in `03-api-contract.md`.
The backend owns all data. The apps hold no business rules the other app
would need to duplicate.

TODO: hosting, auth, caching, offline behaviour, backend project structure,
repository layout for the three codebases.

## Open questions
- Database engine?
- One repo or several?
- Where does connection logic live (database, backend)?
