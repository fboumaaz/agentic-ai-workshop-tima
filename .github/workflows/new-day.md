---
name: New Day
description: Add the current UTC date to the site's daily updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

Update the site's daily activity marker in `index.html`.

Use the workflow run's UTC date from `date -u`, not the agent's local clock.
Format the date using the existing Daily Updates wording and conventions in
`index.html` (for example, `1st of August`).

Use `tools.edit` to make the smallest possible change to `index.html`:

- Add the UTC date to the existing Daily Updates navigation.
- Add one matching accessible `<dialog>` that confirms the daily update ran.
- Follow the existing HTML structure, ID conventions, date wording, and styling.
- Preserve every existing daily update and do not modify `styles.css`.
- Before editing, check whether the UTC date already exists. If it does, make
  no change and call `noop`.
- Do not duplicate a date, navigation control, or dialog.

If `index.html` changed, create at most one pull request with the configured
`create-pull-request` safe output. The pull request may contain only
`index.html`. If no change is needed, call `noop` with a brief explanation.