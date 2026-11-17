# 05 Build plan

Small steps. Each has a "done when" check. Order follows the schema-first approach.

## Step 1: Data model
- Do: finish `02-data-model.md` for Passage, Author and connections.
- Done when: every field and relationship is written down with no `TODO` left.

## Step 2: Database schema
- Do: create the schema from the data model.
- Done when: schema creates cleanly from scratch and sample passages can be inserted and queried.

## Step 3: API contract
- Do: define endpoints in `03-api-contract.md` from the schema.
- Done when: each screen in the MVP has the endpoints it needs.

TODO: backend implementation, Android client, iOS client, content loading.
Add each step in the same format.
