# Publication Denylist

The following must not be copied into public-bound book content without explicit approval:

- `.env` and environment files
- API keys, tokens, passwords and credentials
- connection strings and authentication headers
- private endpoints and internal URLs/hostnames
- absolute local home paths and usernames
- commit-author emails unless approved
- customer-specific identifiers
- employee or other personal information
- internal ticket IDs unless approved
- private screenshots
- private corpora
- corporate source snippets without release clearance
- secret-bearing configuration
- unpublished internal architecture names where release status is unclear

Use sanitized markers such as:

`[REDACTED SECRET — API credential]`
`[INTERNAL URL OMITTED]`
`[PRIVATE PATH OMITTED]`
