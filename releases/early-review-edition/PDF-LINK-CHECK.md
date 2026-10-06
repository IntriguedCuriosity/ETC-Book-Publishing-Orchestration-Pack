# PDF Link Check

Date: 2026-10-06.

## Summary

| Class | Count |
| --- | --- |
| Total link objects scanned | 469 |
| INTERNAL_BOOK_LINK | 469 (TOC anchors and in-document navigation) |
| PUBLIC_EXTERNAL_LINK | 0 (bibliography URLs appear as plain text in this build) |
| PRIVATE | **0** |
| INVALID (with URI) | **0** |

## Required result

- PRIVATE = 0 — **PASS**
- INVALID (with URI) = 0 — **PASS**

## Patterns checked

| Pattern | Found in link URIs |
| --- | --- |
| `file://` | 0 |
| `localhost` / `127.0.0.1` | 0 |
| Windows drive paths | 0 |
| Corporate / private hosts | 0 |

## Notes

Chromium tagged-PDF export represents the generated table-of-contents entries
as internal link annotations with empty URI fields (in-document destinations).
These are classified as INTERNAL_BOOK_LINK.

Bibliography entries retain public HTTPS URLs in visible text. They were not
exported as external hyperlink annotations in this build. No private link
survived.

## Verdict

**PASS**
