# 05 Build plan

Small steps. Each has a "done when" check. Order follows the schema-first approach.

## Step 1: Data model
- Do: finish `02-data-model.md` for Person, Language, Work, Passage, PassageText, Tag and PassageTag. Connections are a planned system and not part of this step (D-015, D-016).
- Done when: every field and relationship is written down with no `TODO` left.

## Step 2: Passage text format
- Do: settle the draft in `08-passage-text-format.md` (D-034) and which marks the MVP draws (D-037). Then update `PassageText.Content` in `02-data-model.md` to match.
- Done when: D-034 and D-037 are DECIDED, `08` is no longer a draft, and `02` shows `Content` as `jsonb` with its structural CHECK.

## Step 3: Database schema
- Do: create the schema from the data model.
- Done when: schema creates cleanly from scratch and sample passages can be inserted and queried. A PassageText with the example from `08` as `Content` passes the structural and NFC CHECKs.

## Step 4: API contract
- Do: define endpoints in `03-api-contract.md` from the schema.
- Done when: each screen in the MVP has the endpoints it needs.

## Step 5: Passage text validation
- Do: write the v1 JSON Schema from `08` and the backend validator for it. The validator checks the schema, NFC, and that every `lang` exists in Language (backend rule 5).
- Done when: the example from `08` passes, and samples with an empty run text, a missing `v` or a `lang` that isn't in Language are rejected.

## Step 6: Source converters
- Do: one converter per source chosen in `07-content-sourcing.md`. Each produces documents in the `08` format.
- Done when: sample texts from each source convert to documents that pass the Step 5 validator, and converting the same input twice gives identical output.

## Step 7: Android passage text rendering
- Do: draw passage text in the Android client as decided in D-037.
- Done when: the example from `08` renders correctly, and an unknown block type or mark shows as plain text without an error.

TODO: backend implementation, Android client, iOS client, content loading.
Add each step in the same format.
