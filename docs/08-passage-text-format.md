# 08 Passage text format

Status: Draft, not decided (D-034). Describes the planned format of `PassageText.Content` (`02-data-model.md`).

## Requirements
1. Other text formats can be converted to it in a straightforward way, so the database does not depend on any one data source.
2. It supports details. Anything the author could reasonably have used to convey meaning in the text is supported by the format.
3. Each line is a separate unit.
4. It is supported in PostgreSQL and passes from the database through the backend to the apps without loss and without janky workarounds.
5. It supports as many languages as reasonably possible.

## Overview
The content is a JSON document in Rites' own schema, stored in a `jsonb` column. It borrows ideas from TEI, the scholarly standard used by Perseus, but is much smaller.

- `v` is the format version, so old rows can be told apart from new ones when the format is extended.
- `blocks` is the ordered list of blocks in the passage. Array order is the reading order.
- `notes` is the list of notes the text points to (D-035).

The author's choices are what count, not the typesetter's.
- In verse, line breaks are the author's, so each line is a separate unit (requirement 3).
- In prose, line breaks come from the page width. The author's unit is the paragraph, so prose is stored as paragraphs, not printed lines.

## Blocks
Every block has a `type`. Any block may also have `role`: `epigraph` or `dedication`.

| Type | Holds | Used for |
|---|---|---|
| `lineGroup` | `lines` | A stanza, or any run of verse lines. |
| `paragraph` | `runs` | Prose. The text wraps freely. |
| `speech` | `speaker` (runs), `blocks` (`lineGroup` or `paragraph`) | Drama: one speaker's speech. |
| `stage` | `runs` | A stage direction that stands on its own. |
| `heading` | `runs` | A section heading inside the passage. |
| `break` | nothing | A section break in prose, such as `* * *`. |

## Lines
A line is an object in a `lineGroup`'s `lines` array.

| Field | Required | Meaning |
|---|---|---|
| `runs` | yes | The text of the line. |
| `n` | no | The source line number as a string, for example `"37"` or `"2.14"`. |
| `part` | no | `initial`, `medial` or `final`, for a line split across speakers or across the page. |
| `indent` | no | Indentation level, a whole number from 1. |
| `align` | no | `center` or `right`. Left is the default. |

- A line's position comes from the array. `n` is a separate field and is never the array position, because real numbering skips, restarts per book and starts mid-poem in an excerpt.
- The parts of a split line share the same `n` and are told apart by `part`, as in TEI's `part="I|M|F"`. Numbers such as `1.1` stay free for book.line citations.
- Lines have no ids of their own, and lines are not aligned between the original and its translations (D-036).

## Inline runs
Inline formatting is stored as runs, not as character positions. A line or paragraph is a list of pieces, each with its own text and marks.

Character positions would break across the platforms. C# and Kotlin count UTF-16 units, Swift counts visible characters, and PostgreSQL counts code points. An accented Greek letter or an emoji would give a different position on each platform. With runs nothing is counted, so nothing can disagree.

| Field | Required | Meaning |
|---|---|---|
| `text` | yes | The text. Must not be empty, except in a marker run. |
| `marks` | no | A list of flags: `italic`, `bold`, `smallCaps`, `sup`, `stage` (a stage direction inside a line). |
| `lang` | no | The language of this run, when it differs from the default. |
| `ruby` | no | Small text shown above the run, such as furigana in Japanese or pinyin above Chinese. |
| `note` | no | The id of a note this run is part of. |
| `caesura` | no | `true` in a marker run with no text: a gap within a line, as in Old English verse. |

- Spaces at the edges of runs are part of the text and are kept, as in `"In the "`.
- A phrase that crosses a line break is split into one run per line.

## Notes
Notes are kept in a separate list at the end of the document, and runs point to them (D-035).

```json
"notes": [
  { "id": "n1", "by": "author", "runs": [{ "text": "The note text." }] }
]
```

- `by` is `author`, `translator` or `editor`. Requirement 2 covers the author's choices. Editorial notes from sources such as Perseus or Gutenberg aren't the author's and may carry their own rights, so they are imported only once those rights are settled in `07-content-sourcing.md`.
- A note attached to a phrase that spans several runs or lines is marked by giving every run of the phrase the same `note` id. The note marker is placed after the last run that carries the id.

## Languages and scripts
- The database is UTF-8. All text is normalised to NFC on the way in, so "é" stored as one character and "é" stored as a letter plus an accent become identical.
- The default language of a PassageText is its Work's `Work.Language`. A run carries its own `lang` only where it differs, for example one Greek word kept in an English translation.
- Every `lang` value is a BCP 47 tag that exists in the `Language` table (D-032, D-033). The backend checks this on every write.
- Writing direction comes from `Language.Direction` (`ltr` or `rtl`). The format has no direction field, and no platform works out direction on its own. Each run with its own `lang` is bidi-isolated when drawn, so a right-to-left word does not reorder the text around it.
- `lang` has to reach the app's text renderer, not only its font choice. Chinese, Japanese and Korean share code points that are drawn differently in each language.

### Known limits of NFC
NFC treats some characters as equivalent that a specialist might want kept apart:
- Greek: oxia becomes tonos (U+1F71 becomes U+03AC). The ano teleia U+0387 becomes the middle dot U+00B7, and the Greek question mark U+037E becomes `;`. Fonts draw these the same, so this is accepted.
- CJK compatibility ideographs (U+F900–U+FAFF) are folded into the unified ideographs, which loses variant glyphs in some Japanese and Korean texts. Converters map them to standardised variation sequences before normalising, which keeps the glyph.

## Storage and transport
- **PostgreSQL:** `PassageText.Content` would become a `jsonb` column. `jsonb` reorders object keys, drops whitespace between fields and keeps only the last of any duplicate keys. It never changes the text inside string values, and arrays keep their order. Nothing that matters is lost.
- **Database checks:** the non-blank CHECK is replaced by a structural CHECK: `Content ? 'v'`, `jsonb_typeof(Content->'blocks') = 'array'` and `jsonb_array_length(Content->'blocks') > 0`. NFC is checked with `Content::text IS NFC NORMALIZED`.
- **Backend checks:** on every write the backend validates the whole document against a JSON Schema. It also checks the `lang` values (backend rule 5 in `02-data-model.md`).
- **.NET:** `Content` is mapped as a plain `jsonb` column (`JsonDocument` or string), not with EF Core's `ToJson()`, because EF Core doesn't support inheritance for complex types and so can't hold "a block is a lineGroup or a paragraph". On reads, the backend passes the document to the API unchanged. Typed deserialization with System.Text.Json happens only on write, in the loader and validator.
- **Key order:** because `jsonb` reorders keys, `type` is not always the first property. A paragraph comes back as `{"runs": …, "type": …}`. System.Text.Json requires the type discriminator first by default, so the backend sets `AllowOutOfOrderMetadataProperties = true` (.NET 9 and later).
- **Kotlin:** `kotlinx.serialization`, polymorphic on `type`. **Swift:** `Codable`, with a custom `init(from:)` for the block types.

## Forward compatibility
- Apps ignore fields and marks they don't know, and show a block type they don't know as plain text. This lets the format grow without breaking app versions already installed. On Kotlin this means `ignoreUnknownKeys` and a default polymorphic deserializer. On Swift it means an `unknown` case.
- An additive change (a new optional field, mark or block type) keeps `v`. A change that alters the meaning of existing data bumps `v`.

## Search copy
A plain-text copy of the content for full-text search is deferred until search is decided for the MVP (D-006). When it is added, the backend builds it from the runs and stores it next to the content. It can't be a generated column, because the search language comes from `Work.Language` in another table.

## Conversion from sources
One converter per source, each producing the same JSON. This keeps the database independent of where the text came from (requirement 1). The sources below are examples. Which sources are used is decided in `07-content-sourcing.md`.

- **TEI (Perseus):** close to one-to-one. `<lg>` becomes a `lineGroup`, `<l n="…">` a line with `n`, `<l part="…">` a line with `part`, `<hi>` a mark, `<note>` a note, `<sp>`/`<speaker>` a `speech`, `<stage>` a stage direction, `<foreign xml:lang="…">` a run with `lang`.
- **Standard Ebooks:** in verse, `<p>` becomes a `lineGroup`, each `<span>` a line, and the class `i1` becomes `indent: 1`.
- **Wikisource and Gutenberg plain text:** a blank line becomes a stanza break, and leading spaces or `:` become indentation. These sources hold less information, so the converter guesses the structure. That limit comes from the source, not from the format.

Converters collapse the source's layout whitespace before splitting text into runs, and normalise to NFC.

## Out of scope
- **Shaped poetry**, where the picture is the poem (Apollinaire's calligrams, for example). No line-based format can capture it. If one is ever needed, store the text plus an image.
- **Vertical text** (classical Chinese and Japanese). It is not supported, rather than half-supported.

## Example
```json
{
  "v": 1,
  "blocks": [
    {
      "type": "lineGroup",
      "lines": [
        { "n": "1", "runs": [{ "text": "Tyger Tyger, burning bright," }] },
        { "n": "2", "indent": 1, "runs": [
            { "text": "In the " },
            { "text": "forests", "marks": ["italic"], "note": "n1" },
            { "text": " of the night;" }
        ]}
      ]
    },
    {
      "type": "speech",
      "speaker": [{ "text": "BERNARDO" }],
      "blocks": [
        { "type": "lineGroup", "lines": [
            { "n": "1", "part": "initial", "runs": [{ "text": "Who's there?" }] }
        ]}
      ]
    },
    {
      "type": "speech",
      "speaker": [{ "text": "FRANCISCO" }],
      "blocks": [
        { "type": "lineGroup", "lines": [
            { "n": "1", "part": "final", "runs": [{ "text": "Nay, answer me." }] }
        ]}
      ]
    },
    { "type": "break" },
    {
      "type": "paragraph",
      "runs": [
        { "text": "A prose block flows and wraps freely, and keeps one word in Greek: " },
        { "text": "λόγος", "lang": "grc", "marks": ["italic"] },
        { "text": "." }
      ]
    }
  ],
  "notes": [
    { "id": "n1", "by": "author", "runs": [{ "text": "An example note." }] }
  ]
}
```

## Open questions
- Which marks and blocks do the MVP apps draw? Everything not drawn shows as plain text. The proposal is to draw what the MVP content needs: stanzas, paragraphs, line breaks, indentation, italic, `lang`, the staggered layout of split lines, and speakers and stage directions if drama passages are seeded. (D-037)
