---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
model: gpt-5.6-sol
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit: true
  web-fetch:
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
---

Read `notes/mona-notes.md` and the existing `site/content/github-info.md` first. Fetch each of these sources with the web-fetch tool:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Use only confirmed, relevant updates from those sources. Revise `site/content/github-info.md` with short, practical guidance that helps developers learn GitHub, follows Mona's editorial notes, and fits the existing page. Link each new factual update to its source. Do not invent details or change any other file.

If neither source contains a useful update for the page, make no edits and call `noop` with a brief reason. Otherwise, propose the change through the `create-pull-request` safe output, with a concise summary and source links in the PR description so Mona can review it. Do not push changes directly to `main` or use another mechanism to create or update a pull request.
