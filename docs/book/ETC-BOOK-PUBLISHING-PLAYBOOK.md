# ETC Book Multi-Model Publishing & Orchestration Playbook

**Version:** 1.0  
**Purpose:** Produce a public-quality modernization handbook from a frozen ETC implementation while preserving evidence discipline, security, reproducibility, and clear model ownership.  
**Status:** Book-generation workflow only. ETC engineering is paused while this edition is prepared.

---

## 1. Operating model

Use **Claude Opus 5.5 Medium** as the parent/coordinator in Cursor.

The repository, tests, measured corpus evidence, and verified public sources are the source of truth. Opus is the principal auditor/adjudicator, not the source of truth.

Recommended roles:

| Role | Model |
|---|---|
| Parent / architecture auditor / adjudicator / release gate | Claude Opus 5.5 Medium |
| External public-source researcher | Gemini 3.8 Flash High |
| Primary technical author / approved reviser | Claude Sonnet 5.5 High |
| Adversarial technical reviewer | Grok 4.7 High |
| Mechanical publication engineer | Composer 2.5 Fast |

Preferred flow:

```text
FROZEN ETC PRODUCT BASELINE
          |
          v
CLAUDE OPUS 5.5 MEDIUM
          |
          +--> Gemini 3.8 Flash High
          +--> Sonnet 5.5 High
          +--> Grok 4.7 High
          +--> Composer 2.5 Fast
          |
          v
OPUS adjudication + release gate
          |
          v
BOOK CANDIDATE
          |
          v
FINAL HUMAN / CHATGPT REVIEW
```

---

## 2. How model switching works

A Markdown file cannot change the active parent model by itself.

Use one Opus parent chat. The supplied custom agents in `.cursor/agents/` declare their own model. Opus should delegate research, authoring, review, and production to those subagents.

If Cursor does not honor the configured model, stop the phase and record:

`MODEL_ROUTING_DEVIATION`

Manual fallback:

1. Select the required model in Cursor.
2. Submit that phase prompt.
3. Save all outputs to disk.
4. Switch models only after the phase gate passes.

The on-disk artifacts are the handoff contract. Chat memory is not.

---

## 3. Security and publication boundary

The eventual handbook may be public. The working repository is not automatically public.

Mandatory rules:

- Keep this workflow local to the ETC repository.
- Do not use Cloud Agents, Projects, or `/in-cloud` for private repository work.
- Never copy credentials, API keys, tokens, passwords, `.env` contents, authentication headers, private endpoints, internal URLs, customer data, employee data, personal data, private screenshots, or private corpora into publication-bound artifacts.
- Do not publish repository code merely because it exists locally.
- Public code excerpts require ownership/release clearance.
- Third-party/public-corpus material must retain attribution/license evidence.
- Public release remains ON HOLD until security, claim, license, and ownership gates pass.

Before book automation begins, rotate/revoke any still-live credential that should no longer be valid.

Use `docs/book/PUBLICATION-DENYLIST.md` for project-specific exclusions.

---

## 4. Freeze the ETC product baseline

Before any audit:

```bash
git status
git rev-parse HEAD
```

Record the product baseline in:

`docs/book/_work/00-baseline/BOOK-SOURCE-BASELINE.md`

Then create a dedicated book branch, for example:

```bash
git switch -c book/v0.1
```

While the product is frozen, expected book-cycle changes are normally limited to:

```text
docs/book/**
.cursor/agents/**
```

If an agent wants to modify ETC source, tests, generated Java, parser behavior, graph logic, confidence logic, transformation behavior, or product metrics merely to make documentation easier:

`STOP: PRODUCT_BASELINE_DRIFT`

Record an engineering gap instead.

---

## 5. Required directory structure

```text
.cursor/
  agents/
    book-researcher.md
    book-author.md
    book-reviewer.md
    book-production.md

docs/book/
  AGENTS.md
  ETC-BOOK-PUBLISHING-PLAYBOOK.md
  PUBLICATION-DENYLIST.md

  _work/
    00-baseline/
      BOOK-SOURCE-BASELINE.md
    01-audit/
    02-research/
    03-contract/
    04-drafts/
    05-review/
    06-adjudication/
    07-revision/
    08-production/
    09-release-review/

  chapters/
  figures/
  appendices/
  candidate/
  release/

  CLAIM-LEDGER.md
  CAPABILITY-MATRIX.md
  CODE-REFERENCE-INDEX.md
  REFERENCES.md
  QUIZ-ANSWER-KEY.md
  FIGURE-INDEX.md
  TABLE-INDEX.md
  QUIZ-INDEX.md
  CHANGELOG.md
  VERSION.md
  README.md
```

Directory rule:

- `_work/` may contain drafts, rejected ideas, disagreements, and unresolved issues.
- `chapters/` may contain only adjudicated text.
- `candidate/` is the assembled manuscript for final review.
- `release/` remains empty until release gates pass.

---

## 6. Evidence discipline

All authoring must preserve:

- OBSERVED FACT
- DETERMINISTIC DERIVATION
- INTERPRETATION

Never:

- treat UNKNOWN as NONE;
- treat missing evidence as proof of absence;
- treat duplicate readings of one source as independent corroboration;
- collapse Java compile into behavioral equivalence;
- collapse GnuCOBOL reference equivalence into production z/OS equivalence;
- collapse ExecutionSlice into Application, Deployment Unit, or Migration Wave;
- let LLM interpretation become deterministic graph truth, deterministic confidence, transformation eligibility, or equivalence proof unless audited code explicitly grants that authority.

---

## 7. Phase 0 — Bootstrap

Run with **Opus 5.5 Medium**.

Verify:

- product baseline commit recorded;
- book branch created;
- product-code boundary frozen;
- `PUBLICATION-DENYLIST.md` created from the template;
- required book folders exist;
- custom agents exist under `.cursor/agents/`;
- no secret/private-source publication;
- no product source/test changes are planned.

If unexpected product changes exist, stop with `PRODUCT_BASELINE_DRIFT`.

---

## 8. Phase 1 — Repository architecture audit

Run with **Opus 5.5 Medium**.

Do not write chapters.

Create only:

```text
docs/book/_work/01-audit/
  REPOSITORY-ARCHITECTURE-AUDIT.md
  CAPABILITY-MATRIX.md
  CLAIM-LEDGER.md
  CODE-REFERENCE-INDEX.md
  TEST-EVIDENCE-INDEX.md
  CORPUS-EVIDENCE-MATRIX.md
  LLM-BOUNDARY-AUDIT.md
  PUBLICATION-EXCLUSION-REPORT.md
  OPEN-ENGINEERING-GAPS.md
  MASTER-CODEBASE-MAP.md
  BOOK-OUTLINE-DRAFT.md
```

Audit rules:

- Code + tests + measured evidence + verified docs outrank model assumptions.
- Do not infer implementation from filenames, TODOs, comments, or roadmap diagrams.
- Distinguish implemented, partial, documented-only, planned, and unknown.
- Every material capability claim must point to actual code/tests/evidence or explicitly say evidence was not established.
- Do not reproduce denylisted content.

The Code Reference Index should assign stable IDs such as:

```text
JCL-001
PROC-001
STORE-001
GRAPH-001
SLICE-001
CONF-001
COBOL-001
HLASM-001
EQUIV-001
LLM-001
```

For each reference record path, symbol, responsibility, input/output, relevant tests, evidence strength, and capability status.

Special audit questions:

1. Where are graph nodes/edges created?
2. How is typed node identity implemented?
3. Which node-edge-node triples are allowed?
4. Where does PROC expansion happen?
5. Which execution view do graph consumers use?
6. How is store identity/role/lifecycle/access mode resolved?
7. How are scheduler edges created?
8. How are execution slices built?
9. Which relationships influence grouping?
10. How is technical-boundary confidence calculated?
11. Where do penalties/caps apply?
12. Where is the LLM called?
13. Can LLM output alter graph truth, slice membership, deterministic confidence, eligibility, or equivalence?
14. Where is COBOL transformation eligibility decided?
15. Where do Java generation/refusal, compile evidence, and equivalence evidence live?
16. Which HLASM capabilities are real vs planned?

Create a Mermaid master architecture using real modules/symbols where reasonable and mark components CURRENT / PARTIAL / PLANNED.

STOP after Phase 1.

### Gate A

Bring the Phase-1 summary to human/ChatGPT review before authoring or research continues.

---

## 9. Claim Ledger format

Use multiple evidence dimensions rather than one mutually exclusive status.

Recommended fields:

```text
claim_id
claim_text
implementation_status
code_refs
test_status
test_refs
corpus_status
corpus_refs
external_refs
source_baseline_commit
public_wording
prohibited_wording
review_status
notes
```

Example:

```text
Claim: Four HLASM return patterns are proven.
Implementation: CODE_SUPPORTED
Tests: TEST_SUPPORTED
Corpus: VALIDATION_CORPUS_MEASURED
Estate evidence: NOT_OBSERVED
Allowed wording:
  "The HLASM analyser proves four return patterns in the independent
   validation corpus at this product baseline."
Prohibited wording:
  "ETC resolves production assembler returns."
```

No downstream model may make a stronger public product claim than the ledger allows.

---

## 10. Phase 2 — External evidence research

Invoke **book-researcher / Gemini 3.8 Flash High** only after Gate A.

Inputs should be approved audit artifacts and explicit public-source questions.

Gemini does not determine what ETC implements.

Prefer:

1. IBM official documentation;
2. AWS official documentation;
3. official vendor/scheduler documentation;
4. language specifications;
5. pinned permissively licensed source used by ETC;
6. public validation-corpus documentation.

Create:

```text
docs/book/_work/02-research/
  REFERENCES.md
  SOURCE-CLAIM-MATRIX.md
  CORPUS-LICENSE-MATRIX.md
  AWS-TARGET-REFERENCE-MATRIX.md
  MAINFRAME-REFERENCE-MATRIX.md
  SOURCE-GAPS.md
```

For each source record organization, title, version/revision, URL, retrieval date, license, claims supported, and claims explicitly not supported.

Do not write chapters. Do not modify the Claim Ledger.

---

## 11. Phase 3 — Book Contract

Return to **Opus 5.5 Medium**.

Reconcile Phase 1 and Phase 2.

Create:

```text
docs/book/_work/03-contract/
  BOOK-CONTRACT.md
  FINAL-BOOK-OUTLINE.md
  CHAPTER-DEPENDENCY-MAP.md
  FIGURE-PLAN.md
  CODE-TRACE-PLAN.md
  CASE-STUDY-SPEC.md
  TERMINOLOGY-GLOSSARY.md
  CLAIM-WORDING-GUIDE.md
```

The Book Contract must define:

- claims authors may make;
- claims authors must not make;
- terminology;
- implemented/partial/planned boundaries;
- evidence hierarchy;
- figure provenance rules;
- code-excerpt rules;
- LLM boundary;
- equivalence vocabulary;
- ExecutionSlice vocabulary.

Create one fictional but production-realistic case study that evolves through the book. It may include nested PROC, symbols, temporary/persistent stores, scheduler relationships, producer/consumer handoffs, one unresolved dependency, one conflicting evidence example, COBOL/copybook use, DB2 or VSAM, later HLASM dependency, and eventual AWS decisions.

If evidence is insufficient, downstream authors must insert:

`[AUTHORING BLOCKER: <exact missing evidence>]`

### Gate B

Review the Book Contract, terminology, case study, outline, and claim limits before drafting.

---

## 12. Phase 4 — Chapter drafting

Invoke **book-author / Sonnet 5.5 High**.

Generate small chapter batches only.

Binding inputs:

- Book Contract
- final outline
- Claim Ledger
- Code Reference Index
- References
- Case Study Spec

Sonnet is the single prose owner.

Do not let the author modify ETC product source/tests to make the chapter easier.

Each chapter should include where appropriate:

- why the problem exists;
- simple mental model;
- production-like example;
- how it appears in mainframe execution;
- why modernization cares;
- Observed vs Derived vs Interpreted;
- ETC approach;
- implementation flow;
- relevant code;
- Mermaid visualization;
- ambiguity/failure case;
- Architect's Warning;
- ETC Lesson Learned;
- Current Support;
- Current Limitations;
- transformation/AWS implication;
- challenges;
- claim check;
- quick recall;
- architecture reasoning;
- code-trace challenge;
- hands-on exercise;
- key takeaways.

Code blocks must use exactly one label:

```text
[ACTUAL ETC EXCERPT]
[SIMPLIFIED ETC EXCERPT]
[PSEUDOCODE]
[FUTURE DESIGN]
```

Actual/simplified ETC code should cite Code Reference ID, path, and symbol.

Figures need Figure ID, title, and provenance:

```text
CODE-DERIVED
SOURCE-DERIVED
AUTHOR-CONCEPTUAL
```

Questions belong in chapters; answers belong in `QUIZ-ANSWER-KEY.md`.

Do not author the entire book in one run.

---

## 13. Phase 5 — Adversarial review

Invoke **book-reviewer / Grok 4.7 High**.

Read-only review. Do not edit chapters, product code, tests, Claim Ledger, or Book Contract.

Review for:

- technical inaccuracies;
- unjustified assumptions;
- stronger-than-evidence claims;
- mainframe terminology misuse;
- code/document mismatch;
- unjustified graph edges;
- declared/effective execution confusion;
- DISP-as-I/O mistakes;
- NONE/UNKNOWN confusion;
- duplicate evidence treated as corroboration;
- ExecutionSlice/Application confusion;
- LLM leakage into deterministic truth;
- compile/equivalence confusion;
- reference-equivalence/zOS confusion;
- simplistic AWS mappings;
- misleading diagrams;
- missing failure modes;
- beginner explanations that become technically false;
- incorrect code references;
- missing public-source citations.

Create:

`docs/book/_work/05-review/CHAPTER-REVIEW-<range>.md`

Each issue must have:

- Severity: BLOCKER / MAJOR / MINOR / SUGGESTION
- Chapter
- Section
- claim
- problem
- why it matters
- evidence
- recommended correction direction

Also include ten architecture questions a skeptical reviewer would ask.

---

## 14. Phase 6 — Opus adjudication

Return to **Opus 5.5 Medium**.

For every BLOCKER or MAJOR item, verify against the source of truth.

Classify each:

```text
ACCEPT
PARTIALLY_ACCEPT
REJECT
NEEDS_HUMAN_DECISION
```

Create:

```text
docs/book/_work/06-adjudication/
  REVIEW-DECISIONS-<range>.md
  AUTHOR-REVISION-INSTRUCTIONS-<range>.md
```

If the Claim Ledger itself appears wrong, do not silently edit it. Create a:

`CLAIM-LEDGER-CORRECTION-PROPOSAL`

with exact code/test/corpus evidence.

Do not rewrite chapters here.

---

## 15. Phase 7 — Approved revisions

Invoke **book-author / Sonnet 5.5 High** again.

Apply only approved adjudication instructions.

Do not incorporate rejected reviewer suggestions.

Create:

`docs/book/_work/07-revision/REVISION-LOG-<range>.md`

For each change record chapter, section, review issue ID, and change made.

Only after review + adjudication + approved revision should chapter text move to `docs/book/chapters/`.

---

## 16. Phase 8 — Mechanical publication work

Invoke **book-production / Composer 2.5 Fast**.

Composer may perform only mechanical tasks:

- validate Markdown;
- validate Mermaid syntax;
- repair internal links;
- normalize headings;
- update figure/table numbering;
- update quiz IDs;
- build figure/table/quiz indexes;
- update TOC;
- check code-reference links;
- detect duplicate IDs;
- detect missing references;
- detect orphan references;
- check print-width code blocks;
- report oversized diagrams.

Composer must not:

- change architecture claims;
- reinterpret code;
- rewrite technical explanations;
- change capability status;
- invent claims.

Create:

```text
docs/book/_work/08-production/
  BUILD-REPORT.md
  BROKEN-REFERENCE-REPORT.md
  PRINT-READINESS-REPORT.md
```

If meaning looks inconsistent, report it. Do not fix it.

---

## 17. Chapter batching

Recommended batches:

```text
Batch 1  Preface + Transformation Mental Model + Mainframe Fundamentals
Batch 2  JCL + PROC + DD
Batch 3  COBOL + Store Semantics + EvidenceGraph
Batch 4  Scheduler + ExecutionSlice + Confidence
Batch 5  Unknowns + Capability + LLM Boundary
Batch 6  COBOL Transformation + Runtime + Equivalence
Batch 7+ HLASM
Later    Application boundaries + Data/Batch/Online transformation + AWS + Cutover
```

Per batch:

```text
Sonnet draft
   ↓
Grok review
   ↓
Opus adjudication
   ↓
Sonnet approved revision
   ↓
Composer production checks
   ↓
Promote to chapters/
```

One-writer rule:

```text
Sonnet   = writer
Grok     = reviewer
Opus     = decision maker
Sonnet   = applies approved fixes
Composer = formatting/assembly only
```

---

## 18. Phase 9 — Public release/security/claim gate

Run with **Opus 5.5 Medium** over the assembled `candidate/` manuscript.

Security review must detect:

- API keys/tokens/passwords;
- connection strings/auth headers;
- `.env` content;
- private endpoints;
- internal URLs/hostnames;
- absolute local paths/usernames;
- commit-author emails unless approved;
- personal/customer/employee information;
- internal ticket IDs unless approved;
- private screenshots;
- secret-looking test values.

IP/license review must confirm:

- ETC-owned excerpts have ownership/release clearance;
- third-party/public-corpus material is attributed;
- licenses are recorded;
- source-derived figures cite source IDs;
- copyrighted prose has not been copied unnecessarily.

Claim review must inspect dangerous wording such as:

```text
fully
all
every
proven
production equivalent
automatically understands
complete migration
zero risk
replaces SMEs
```

Every occurrence must agree with the Claim Ledger.

LLM review must verify the book does not imply that an LLM or API key provides deterministic technical truth.

Provenance-leakage review must search for:

- absolute local paths;
- usernames/home directory names;
- internal repository URLs;
- internal hostnames;
- private environment names;
- copied internal comments.

Create:

```text
docs/book/_work/09-release-review/
  PUBLICATION-SECURITY-REVIEW.md
  PUBLICATION-CLAIM-REVIEW.md
  PUBLICATION-LICENSE-REVIEW.md
  RELEASE-BLOCKERS.md
```

Do not silently remove substantive content.

`docs/book/release/` remains empty while blockers exist.

---

## 19. Approval gates

**Gate A — after repository audit**  
Mandatory human/ChatGPT review before research/authoring.

**Gate B — after Book Contract**  
Confirm outline, terminology, case study, claim limits, chapter dependencies.

**Gate C — per chapter batch**  
No draft moves to `chapters/` without review + adjudication + revision.

**Gate D — final candidate**  
Review the coherent candidate plus Claim Ledger, Capability Matrix, and Code Reference Index.

**Gate E — public release**  
Requires security PASS, claim PASS, license PASS, ownership/release clearance, and zero unresolved publication blocker.

---

## 20. What not to do

Do not:

- ask one model to discover the architecture and write the whole book;
- let public documentation determine what ETC implements;
- let reviewer models silently rewrite chapters;
- let Composer make architectural corrections;
- let authoring agents change ETC source;
- silently move the product baseline;
- confuse compile success with equivalence;
- confuse reference equivalence with z/OS production proof;
- confuse ExecutionSlice with Application/Deployment Unit/Migration Wave;
- let LLM interpretation create deterministic graph truth;
- publish before security/IP/license/ownership gates pass.

---

## 21. START HERE — first Cursor prompt

Open a **new Cursor Agent chat** and select **Claude Opus 5.5 Medium**.

Paste:

```text
Read and follow:

docs/book/ETC-BOOK-PUBLISHING-PLAYBOOK.md
docs/book/AGENTS.md

We are starting the ETC handbook workflow.

First perform PHASE 0 — BOOTSTRAP only.

Verify:
- the product baseline commit;
- dedicated book branch;
- clean/frozen product-code boundary;
- publication denylist;
- required docs/book folder structure;
- custom subagents in .cursor/agents;
- no use of Cloud Agents, Projects or /in-cloud;
- no secret or private-source publication.

If Phase 0 passes, perform PHASE 1 — REPOSITORY ARCHITECTURE AUDIT exactly as
specified in the playbook.

Do NOT invoke Gemini, Sonnet, Grok or Composer yet.
Do NOT write chapters.
Do NOT modify ETC source or tests.

After Phase 1, STOP.

Return:
1. bootstrap result;
2. product baseline commit;
3. audit files created;
4. unresolved architecture questions;
5. contradictory/suspicious claims;
6. publication exclusions;
7. capabilities requiring human confirmation;
8. confirmation that no product code/test file changed.

Wait for my approval before Phase 2.
```

---

## 22. Final operating principle

We are not using multiple models to “write a book.”

We are running a miniature engineering/publishing organization:

```text
Repository + tests + evidence
         ↓
Architectural audit
         ↓
External evidence research
         ↓
Binding book contract
         ↓
Single primary author
         ↓
Independent adversarial review
         ↓
Architecture adjudication
         ↓
Approved revision
         ↓
Mechanical publishing pipeline
         ↓
Security / claim / license gate
         ↓
Final human architecture + learning review
```

The book is an engineering artifact. Every important claim, diagram, code trace, and capability statement must remain traceable to the frozen ETC product baseline or to an explicitly identified public source.
