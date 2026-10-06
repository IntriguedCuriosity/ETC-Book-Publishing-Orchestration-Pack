# PDF Build Report — Private Early Review Edition

Date: 2026-10-06. Mechanical production build from the 22-file manifest
allowlist in `book/_work/09-public-candidate/PUBLIC-CANDIDATE-MANIFEST.md`.

## Output

| Item | Value |
| --- | --- |
| PDF path | `book/_work/10-private-pdf/Enterprise-Mainframe-Transformation-Early-Review-Edition.pdf` |
| File size | 3,654,767 bytes |
| Total pages | 198 |
| Page size | US Letter |
| Margins | 1 in top/bottom; 0.9 in left/right |
| Build tool | HTML assembly + Chromium print via Playwright |
| Intermediate HTML | `book/_work/10-private-pdf/_build/book.html` (not packaged) |

## Source inputs

Built exclusively from the 22 reader-facing manifest files. No recursive
directory inclusion. Excluded: `_checks/`, review records, verification records,
attestation drafts, sanitization logs, internal scripts, Git metadata.

## Content counts

| Measure | Count |
| --- | --- |
| Allowlisted source files | 22 |
| Chapters included (1–12 and 21–24) | 16 |
| Figure references rendered | 42 (27 distinct figure identifiers in source) |
| Mermaid diagrams rendered | 7 |
| Pseudocode blocks (`[PSEUDOCODE` labels) | 39 |
| Bibliography entries | 14 ([B1]–[B14]) |
| Table rows (approx., pipe-table lines) | 843 |

## Structure produced

1. Cover (title, subtitle, edition label, author)
2. Generated table of contents
3. Front matter from manifest (title/contents, notices, FM-2, attribution)
4. Chapters 1–12
5. Special Early Review Section divider (before Chapter 21)
6. Chapters 21–24
7. Forthcoming chapters (titles only)
8. Bibliography

Chapter numbering is unchanged. The TOC and the special-review divider make
the jump from Chapter 12 to Chapter 21 explicit.

## Title block used

- **Title:** Enterprise Mainframe Transformation
- **Subtitle:** Evidence, Dependency Graphs, Bounded Inference, and HLASM Comprehension
- **Edition:** EARLY REVIEW EDITION — WORK IN PROGRESS
- **Author:** ARSHADUL SHAIKH

## Mechanical notes

- Pseudocode labels preserved, including `[PSEUDOCODE — PUBLIC EDITION]`.
- Text diagrams and Mermaid blocks rendered from allowlisted source only.
- No content rewrite beyond cover, TOC, and special-review divider pages.
- No `book/release/` artifact created.

## Post-build verification summary

| Check | Result |
| --- | --- |
| PUB-033 metadata | PASS |
| Content leak scan | PASS (0 unintended hits) |
| Hyperlinks | PASS (0 private, 0 invalid with URI) |
| Embedded files / JS / forms | PASS |
| Visual QA | PASS (no replacement-character findings) |
| Production similarity spot-check | PASS |

## Source invariance

Canonical Chapters 1–12, frozen HLASM Chapters 21–24, and ETC product
source/tests were not modified (`git diff --quiet` exit 0).
