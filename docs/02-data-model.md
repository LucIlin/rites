# 02 Data model

Status: MVP in progress. Relational database, designed schema-first.

## Entities (MVP)
### Passage
TODO: fields (text, attributes such as theme, motif, emotion, author reference).

### Author
TODO: fields.

### Work
TODO: fields. Work is an entity in the MVP (see D-004 in decisions.md).

### Connections
Connections between passages are derived from shared attributes (theme, motif, emotion).
They are not stored as hand-curated, typed links.
TODO: how the derivation is computed and whether it is stored.

## Relationships
TODO: Passage ↔ Author, Passage ↔ Work, Work ↔ Author, Passage ↔ attributes.
Passage ↔ Passage is derived through shared attributes.

## Open questions
- Are themes, motifs and emotions separate tables or one tag table with a kind?