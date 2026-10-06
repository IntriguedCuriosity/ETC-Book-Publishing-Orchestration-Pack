# PDF Content Leak Check

Date: 2026-10-06. Text extracted from the generated PDF and scanned. No secret
values are printed.

## Scan results

| Category | Hits |
| --- | --- |
| Private paths (Windows) | 0 |
| Private paths (POSIX home) | 0 |
| Emails | 0 |
| API keys / PATs | 0 |
| Private repository names | 0 |
| Corporate hostnames | 0 |
| Internal ID families (GAP-, CL-, AB-, PUB-, etc.) | 0 |
| Model-routing / model names | 0 |
| `mainframe-jcl` | 0 |
| `became(` | 0 |
| `file://` | 0 |
| `localhost` | 0 |
| Private commit hashes (non-public-pin) | 0 |

**Total unintended hits: 0**

Public corpus pins and public vendor document URL fragments (for example hex
tokens inside `ibm.com` PDF URLs) were scoped out as public provenance.

## Source-symbol residue

No unintended product-source symbol collisions were introduced by layout.
Approved retained vocabulary (relationship kinds, enum output values, teaching
terms) appears as in the public candidate.

## Attribution strings verified in extracted text

| Corpus | Check | Result |
| --- | --- | --- |
| CBSA | © IBM Corporation; no source reproduced | Present |
| CardDemo | © Amazon Web Services, Inc.; Apache License 2.0 | Present |
| GenApp | © IBM Corporation; EPL-2.0 | Present |
| FIG-12-1 | `reader: the JCL reader` | Present |
| FIG-12-1 | `mainframe-jcl` absent | Confirmed |

## Verdict

**PASS**
