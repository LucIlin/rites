# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository details

This repository contains Rites, a mobile app for reading and discovering literature and poetry
through excerpts referred to as passages. Rites has a planned backend and separate Android and iOS apps.

## Project status

This repository is still at the design stage. It has no source code, build system, tests, or tooling yet, so there are no build, lint, or test commands. Update this file once a stack is chosen and code exists.

- Database: planned
- API: planned
- Android app: planned
- iOS app: planned
- 
## Documentation layout

The project is planned in `docs/`. The files are numbered in reading order. Most are empty placeholders for now.

- `01-product.md`: product definition
- `02-data-model.md`: data model
- `03-api-contract.md`: API contract
- `04-architecture.md`: system architecture
- `05-build-plan.md`: build plan and sequencing
- `06-design-notes.md`: design notes
- `07-content-sourcing.md`: content sourcing
- `decisions.md`: decision log

When these docs have content, treat them as the source of truth for design intent. Read the relevant ones before implementing anything. When a design decision gets made or changed, record it in `docs/decisions.md`.

## Instructions 

- If a doc says something exists but you can’t find it in the code, say so and ask instead of assuming

## License

All rights reserved (see `README.md`). The code is provided for viewing only, so don't add third-party license headers or relicense anything.

## Glossary

A list of domain or business terms used in Rites.

| Word    | Explanation            |
|---------|------------------------|
| Passage | The excerpts and works |

