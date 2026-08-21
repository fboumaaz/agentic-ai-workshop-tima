---
name: Weekly Report Status
description: Publish a concise weekly repository activity report.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Generate and publish one concise activity report for this repository.

Use the GitHub tools to inspect the previous seven full days ending at workflow
start in UTC. Cover commits, issues, and pull requests, including useful counts
and links or short descriptions for the activity found in each category.

Create exactly one new issue using the configured `create-issue` safe output. Use
a title that starts with `[weekly-report] ` and a GitHub-flavored Markdown body.
If there was no activity in the window, still create the issue and state clearly
that no commits, issues, or pull requests occurred.