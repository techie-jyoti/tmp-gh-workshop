---
name: Highlights of the Day
description: Add an unused GitHub Agentic Workflows FAQ highlight to the daily updates page.
engine: copilot
on:
  schedule:
    - cron: "0 */6 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
  web-fetch: {}
network:
  allowed: [github.github.com]
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlights of the Day

Use the workflow run's current UTC date and update the site's Daily Updates section with one unused FAQ entry.

## Task

1. Fetch the GitHub Agentic Workflows FAQ from https://github.github.com/gh-aw/reference/faq/ using the web-fetch tool.
2. Read `index.html` and identify every FAQ question already represented in the Daily Updates dialogs. Treat equivalent wording as represented even if the punctuation differs.
3. Select exactly one FAQ question that is not already represented. If no unused FAQ remains, call `noop` with a concise explanation and make no file changes.
4. Get the workflow run's date in UTC, not the runner's local date. Format it to match the existing wording, such as `1st of August`, and use the matching lowercase month-day ID convention, such as `august-1`.
5. If the matching date already has a Daily Updates navigation control and dialog placeholder, reuse that control and dialog. If the date already has a dialog containing an FAQ, or if the date is otherwise already represented, call `noop` and make no changes.
6. Otherwise, add one navigation control to the existing Daily Updates list and one matching dialog to `index.html`. Follow the existing HTML structure and conventions exactly, including `aria-controls`, `aria-labelledby`, `aria-describedby`, `data-dialog-trigger`, and the `-dialog`, `-question`, and `-answer` IDs. Preserve all existing updates.
7. Put the selected FAQ question in the dialog question heading and write a concise, accurate answer based on the fetched FAQ. Do not duplicate any date, navigation control, dialog, or FAQ.
8. Use the configured `create-pull-request` safe output to propose the change. The pull request may contain only `index.html`, and at most one pull request may be created.

If the page already contains the selected FAQ, today's dialog already contains an FAQ, or no unused FAQ remains, do not edit any file. Use `noop` with a short reason instead of creating a pull request.