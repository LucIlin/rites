# 07 Content sourcing

## Where passages come from
TODO

## What may be used
TODO: public domain, licensed, user-submitted. Record the licence for each source.

## Attribution
TODO: how author and source are credited in the app.

## Loading
Seed files carry the UUID of every catalog row (Person, Work, Passage, Tag) (D-031).
- A script may fill in missing UUIDs in the seed files once. After that they are permanent and never change.
- Rebuilding the database from the seed files gives every row the same ID as before.
- Seed files for different works can be prepared separately, with no shared ID ranges.
- Languages are seed data too, keyed by their tag instead of a UUID (D-040).
- The seeding process handles possible duplicate Works (D-042).
- Validation queries run after seeding and catch a translation with no translator rows (D-041).

TODO: how passages and their attributes enter the database.
