# ETC Book Publishing Orchestration Pack

This repository contains the Cursor orchestration pack for the **Enterprise Transformation Copilot (ETC)** handbook workflow.

## Purpose

The pack coordinates a controlled multi-model book-production workflow:

- Claude Opus 5.5 Medium — parent/coordinator, architecture audit, adjudication, release gate
- Gemini 3.8 Flash High — public technical evidence research
- Claude Sonnet 5.5 High — primary technical author and approved revisions
- Grok 4.7 High — adversarial architecture reviewer
- Composer 2.5 Fast — mechanical publication maintenance

## Important

This repository contains **only the publishing/orchestration pack**. It does not contain ETC product source code, private corpora, credentials, internal URLs, or proprietary project material.

After downloading, place the pack at the root of the ETC repository and start with:

`docs/book/START-HERE.md`

The handbook workflow is designed to remain private until the security, claim, license, and ownership/release gates pass.
