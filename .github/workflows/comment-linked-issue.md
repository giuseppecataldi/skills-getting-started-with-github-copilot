---
name: Comment Linked Issue
description: Commenta automaticamente una GitHub Issue quando il commit contiene un riferimento tipo #1.
on: push

permissions:
  contents: read
  issues: read

tools:
  github:
    mode: gh-proxy
    toolsets: [issues]

safe-outputs:
  add-comment:

timeout-minutes: 5
---

# Comment Linked Issue Agent

You are an agentic workflow that runs whenever a commit is pushed.

## Context

The pushed commit SHA is:

`${{ github.event.head_commit.id }}`

The repository is:

`${{ github.repository }}`

The GitHub server URL is:

`${{ github.server_url }}`

## Goal

Analyze the pushed commit and determine whether its commit message references a GitHub Issue.

A valid issue reference is any GitHub issue number written as:

- `#1`
- `refs #1`
- `fixes #1`
- `closes #1`
- `resolves #1`

## Instructions

1. Inspect the commit identified by the provided commit SHA.
2. Read the commit message.
3. Extract the first issue number in the format `#number`.
4. If no issue number is present, do nothing.
5. If an issue number is present, add a comment to that issue.

## Comment format

Add this comment to the linked issue:

```text
🤖 Agentic workflow detected a commit linked to this issue.

Commit:
https://github.com/${{ github.repository }}/commit/${{ github.event.head_commit.id }}
