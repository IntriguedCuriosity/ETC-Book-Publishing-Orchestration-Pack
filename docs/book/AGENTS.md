# ETC Book Authoring Rules

These rules apply to all work under `docs/book/`.

## Source of truth

The source of truth is the frozen ETC product baseline identified in:

`docs/book/_work/00-baseline/BOOK-SOURCE-BASELINE.md`

Repository implementation, tests, measured corpus evidence, and verified public documentation outrank model assumptions.

## Baseline discipline

- Do not modify ETC product source/tests/generated Java to make documentation easier.
- If product behavior appears wrong or incomplete, record an authoring or engineering gap.
- Do not silently change the product baseline commit.
- If unexpected product-code changes are detected, stop with `PRODUCT_BASELINE_DRIFT`.

## Evidence discipline

Always distinguish:

- OBSERVED FACT
- DETERMINISTIC DERIVATION
- INTERPRETATION

Never treat UNKNOWN as NONE.
Never treat missing evidence as proof of absence.
Never treat duplicate evidence from one source as independent corroboration.

## Architecture vocabulary

- ExecutionSlice is not automatically an Application.
- ExecutionSlice is not automatically a Deployment Unit.
- ExecutionSlice is not automatically a Migration Wave.
- Java compilation is not behavioral equivalence.
- GnuCOBOL reference equivalence is not production z/OS equivalence.
- AWS target generation is not production deployment.
- LLM interpretation cannot be presented as graph truth, deterministic confidence, transformation eligibility, or equivalence proof unless the audited implementation explicitly establishes such authority.

## Publication security

Never reproduce denylisted publication content, credentials, private endpoints, internal URLs, personal data, corporate-only source, or private screenshots.

Use sanitized markers instead.

## Authorship workflow

- Sonnet owns prose.
- Grok reviews and does not rewrite chapters.
- Opus adjudicates.
- Sonnet applies approved revisions.
- Composer performs mechanical production only.

Only adjudicated content may move into `docs/book/chapters/`.
`docs/book/release/` remains empty until public-release gates pass.
