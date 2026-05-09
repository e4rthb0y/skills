---
name: development-workflow
description: End-to-end development lifecycle for the project. Use when starting a new task, managing GitHub issues, following project standards, or submitting pull requests.
---

# Development Workflow

A comprehensive guide to the agentic development lifecycle, from task discovery to submission.

## Prerequisites

- Ensure `gh`, `git`, and any project-specific formatters or linters are installed.
- You MUST source the environment setup script before EVERY `gh` command or sequence of commands to authenticate as an agent:
    ```bash
    source ~/.agent-env.sh && gh <command>
    ```

## 1. Startup & Discovery

Identify your objectives and prepare your environment.

- **Environment Check**: Run the project's initialization script (e.g., `./init.sh`) to verify tool health.
- **Task Discovery**: Authenticate and find backlog tasks (labeled `agent:assigned` but NOT `in-progress`):
    ```bash
    source ~/.agent-env.sh && gh issue list --label "agent:assigned" --search "-label:in-progress"
    ```
- **Claim Task**: Mark the issue as `in-progress` while keeping the `agent:assigned` label to maintain ownership:
    ```bash
    source ~/.agent-env.sh && gh issue edit <number> --add-label "in-progress"
    ```
- **Reference**: See [github-ops.md](references/github-ops.md) for discovery commands.

## 2. Planning & Execution

Maintain transparency and quality during development.

- **Decompose Task**: Break down issues into atomic steps in `.agents/TODO.md` and sync to GitHub.
- **Branch & Draft PR**: Create a feature branch and an immediate DRAFT Pull Request to link the issue and track progress.
- **Standards**: Follow the project's formatting and "Root Lock" rules.
- **Reference**: See [github-ops.md](references/github-ops.md) for branch and PR creation commands.

## 3. Submission & Shutdown

Validate your work and handle transitions.

- **Principal Checklist**: Perform a final self-review of architecture and telemetry.
- **Ready for Review**: Mark the draft PR as ready for review.
- **Verify CI**: After submitting or marking as ready, monitor CI runs (linters, builds, tests):
    ```bash
    source ~/.agent-env.sh && gh pr checks --watch
    ```
    If a job fails, inspect the logs to diagnose the issue:
    ```bash
    source ~/.agent-env.sh && gh run view --log-failed --job=<job-id>
    ```
- **Handoffs**: When submitting for review, apply the generic status label:
    ```bash
    source ~/.agent-env.sh && gh issue edit <number> --add-label "waiting-for-review" --remove-label "in-progress"
    ```
    If pausing, ensure the current state is documented on the issue.
- **Reference**: See [github-ops.md](references/github-ops.md) for PR and handoff commands.
