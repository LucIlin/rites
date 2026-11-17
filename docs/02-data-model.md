# 02 Data model

Status: MVP in progress. Relational database, designed schema-first.

## Entities (MVP)
### Passage
TODO: fields (text, attributes such as theme, motif, emotion, author reference).

### Author
TODO: fields.

### Connections
TODO: how passages relate to each other and to attributes (theme, motif, emotion).

## Relationships
TODO: Passage ↔ Author, Passage ↔ Passage, Passage ↔ attributes.

## Deliberately left out
- **Work**: not an entity in the MVP, because the model should not centre on the whole work.
  Revisit only if a concrete need appears. Note it in decisions.md if so.

## Open questions
- Is a connection typed (similar theme, same motif, contrast) or a plain link?
- Are themes, motifs and emotions separate tables or one tag table with a kind?