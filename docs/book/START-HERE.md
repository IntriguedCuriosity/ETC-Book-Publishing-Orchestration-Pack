# START HERE

1. Place this pack at the root of the ETC repository so the included `.cursor/agents/` and `docs/book/` paths merge into the project.
2. Before any AI work, rotate/revoke any still-live credential that should no longer be valid.
3. Freeze the current ETC product commit and create a dedicated `book/v0.1` branch.
4. Copy `BOOK-SOURCE-BASELINE.template.md` to `BOOK-SOURCE-BASELINE.md` and fill it with measured values.
5. Copy `PUBLICATION-DENYLIST.template.md` to `PUBLICATION-DENYLIST.md` and add any project-specific exclusions.
6. Open a new Cursor Agent chat.
7. Select **Claude Opus 5.5 Medium** as the parent model.
8. Paste the Phase 0/1 starter prompt from `ETC-BOOK-PUBLISHING-PLAYBOOK.md` Section 25.
9. Stop after Phase 1 and review the audit before continuing.

You do not need to manually switch the parent model if Cursor custom subagents work correctly. The parent Opus chat delegates Gemini/Sonnet/Grok/Composer phases through the `.cursor/agents/` definitions.

If a subagent runs under a different model than expected, stop that phase and use the manual model-switch fallback described in the playbook.
