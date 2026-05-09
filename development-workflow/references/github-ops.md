# GitHub & Git Operations

Technical commands for managing the development lifecycle.

## Task Discovery

- **List My Active Tasks**: `gh issue list --label "agent:assigned" --label "in-progress"`
- **List Backlog**: `gh issue list --label "agent:assigned" --search "-label:in-progress"`
- **View Details**: `gh issue view <id>`

## Task Lifecycle

- **Claim Task**: `gh issue edit <id> --add-label "agent:assigned"`
- **Start Progress**:
    ```bash
    source ~/.agent-env.sh && \
    gh issue edit <id> --add-label "in-progress" && \
    git checkout -b feature/issue-<id> && \
    gh pr create --title "Fix: [Task Name]" --body "Fixes #<id>" --draft
    ```
- **Atomic Breakdown**: Comment on the PR or issue: `gh issue comment <id> --body "### Atomic Task Breakdown\n- [ ] Task 1..."`

## Development

- **Committing**: Use conventional commits (e.g., `feat: ...`, `fix: ...`).
- **Pushing**: `git push origin HEAD`

## Submission

- **Mark Ready**: `gh pr ready <pr-number>`
- **Verify CI**: `gh pr checks --watch`
- **Inspect Failed Logs**: `gh run view --log-failed --job=<job-id>`
- **Handoffs**: `gh issue edit <id> --add-label "waiting-for-review" --remove-label "in-progress"`
