---
name: Update GitHub Info
on:
  schedule:
    - cron: '0 06 * * *'
  workflow_dispatch: {}
permissions:
  contents: read
  pull-requests: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.com
    - github.blog
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: false
    fallback-as-issue: false
---

## Instructions for the agent

- Read the repository file `notes/mona-notes.md`.
- Use the GitHub Blog and the GitHub Changelog as official sources.
- Web fetch `https://github.blog/latest/` and `https://github.blog/changelog/`.
- Aggregate relevant items and update `site/content/github-info.md`.
- Produce the new file content as the `combined_content` safe output.
- Open a pull request for Mona to review the proposed website update.
- Use `github.create-pull-request` (declared in `safe-outputs`) to propose
  the change instead of writing directly to `main`.

## Notes

- The workflow runs daily at 06:00 UTC and may be triggered on demand.
- The `github.create-pull-request` tool is given `access: edit` so the agent
  can open PRs. The workflow uses `safe-outputs` so only a proposed PR is
  created rather than committing straight to `main`.
