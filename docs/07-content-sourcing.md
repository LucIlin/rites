# 07 Content sourcing

## Where passages come from
TODO

## What may be used
TODO: public domain, licensed, user-submitted. Record the licence for each source.

## Attribution
TODO: how author and source are credited in the app.

## Loading
The source-of-truth database (production, after launch) holds the catalog (D-045). A seeding process loads content into it, and only into it; other databases receive copies through dumps. It does not read from seed files, and no seed files are kept, because they would go stale (D-043).
- The backend creates every UUID (version 7) when it inserts a row. A row's UUID never changes once it has been created.
- Languages are added by the seeding process like the rest of the catalog (D-040).
- The seeding process handles the checks, including possible duplicate Works (D-042).
- Validation queries run after seeding and catch a translation with no translator rows (D-041).

TODO: how passages and their attributes enter the database.

## Editorial review
After launch, the catalog is reviewed and developed in a continuous editorial process (D-050). Fine-grained decisions about
the data, such as nuanced categorization, can be left to manual attention there. This works because the catalog is finite
and its categorization is unlikely to change once finalized.
