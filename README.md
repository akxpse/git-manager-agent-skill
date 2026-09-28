# Git Manager Agent Skill

**Small commits. Preserved behavior. Clear handoffs.**

Git Manager Agent Skill helps Codex turn coding work into small, verified Git checkpoints that people can understand and continue. It guides repository inspection, careful refactoring, branch coordination, validation, and durable handoffs so progress stays recoverable and essential knowledge stays with the code.

**This version supports Codex only.** Support for other agents has not been validated.

Created by **akxpse**. Released under the [MIT license](LICENSE).

## The problem

An agent can accumulate hours of uncommitted work before an unexpected shutdown. A reminder to commit at the end comes too late. Even when the code survives, another developer may struggle to understand what changed, which checks passed, or what remains unfinished without the original chat.

Cleanup creates another risk. Removing logic that looks unused can break hidden callers, edge cases, or behavior on another branch. Passing tests alone cannot prove that a refactor preserved every contract.

This skill addresses those problems with frequent checkpoints, explicit ownership checks, behavior preservation, and recovery context stored in the repository.

## What it does

* Inspects existing work before editing and protects changes owned by other people or agents.
* Uses a dedicated task branch and checks available branch activity for overlapping changes.
* Starts with an audit of project owned code, tests, configuration, and documentation. It resolves concrete findings in reviewable increments before ordinary task implementation.
* Preserves contracts, validation, errors, side effects, ordering, and edge cases during cleanup. Intentional behavior changes require separate authorization.
* Validates each coherent increment, reviews working and staged diffs, then verifies the resulting commit.
* Targets a checkpoint within 15 minutes of active editing. When policy permits, incomplete recovery commits record gaps, failed or unrun checks, and the next action.
* Leaves enough durable context for a developer to continue without the original chat.
* Pushes only when the destination and action are authorized.

The working loop is:

**Understand → select a small increment → implement → validate → review the diff → checkpoint → repeat → hand off**

## Install with a prompt

Open Codex in the Git repository where you want to use the skill. Paste this prompt:

```text
Use $skill-installer to install Git Manager Agent Skill from
https://github.com/akxpse/git-manager-agent-skill
using the directory .agents/skills/git-manager-agent-skill.

Install it for this repository only, into
.agents/skills/git-manager-agent-skill, including its references directory.

Inspect an existing installation before making changes. Preserve local
customizations and ask before replacing conflicting files. Do not modify
AGENTS.md. Report the installed path and how to invoke the skill.
```

Start a new turn after installation. If Codex does not discover the skill, restart the session. Repository discovery uses `.agents/skills/`; see the [official Codex skill documentation](https://developers.openai.com/codex/skills).

For manual installation, copy the entire [.agents/skills/git-manager-agent-skill](.agents/skills/git-manager-agent-skill/SKILL.md) directory into your repository at the same path. It contains only `SKILL.md` and `references/handoff-template.md`. Keep the license notice with redistributed copies.

A working Git installation and an authorized commit identity are required for checkpoints. Validation also requires the tools your project normally uses. The skill itself installs no scripts, hooks, dependencies, or background services.

## Use with a prompt

Replace the bracketed fields, then paste:

```text
Use $git-manager-agent-skill for this task: [describe the change].

Acceptance criteria: [observable outcomes].
Intended base branch: [branch name].

Follow the skill through validation and handoff. Preserve existing behavior
except for the changes requested above. Do not push until I authorize both
the destination and action.
```

On first adoption, expect an audit and remediation across the repository. This can be substantial in an existing project. Later tasks use the completed adoption record and focus on relevant changes. Blocked adoption must be reported; an exception requires explicit approval.

At completion, look for the verified branch and commit, actual validation results, remote status, remaining changes, and the next action. For substantial or incomplete work, follow the repository handoff convention or inspect `docs/handoffs/`.

## Optional repository instructions

To make the workflow an ongoing project convention, ask the repository owner to approve adding this snippet to `AGENTS.md`:

```markdown
Follow [Git Manager Agent Skill](.agents/skills/git-manager-agent-skill/SKILL.md)
when implementing, fixing, refactoring, resuming, or handing off changes.

Initially audit and remediate concrete findings across the repository,
recording completion evidence. Thereafter apply the standards to work
related to the task.

Preserve existing behavior during cleanup. Treat behavior changes as
separately authorized work. Inspect overlapping branches, preserve others'
work, and validate combined changes after authorized integration.

Reviews that only inspect code must not create branches, edits, commits,
or pushes. The skill does not independently authorize pushes or override
repository instructions and ownership boundaries.
```

## Scope and limits

The skill provides instructions. It is not a timer or a guarantee against bugs, interruption, data loss, or agent noncompliance. Local commits do not protect against loss of the disk or workspace. Remote protection requires a successful push to an authorized destination.

Separate worktrees protect files and indexes, but cannot prevent semantic conflicts between branches. Required checks, repository policies, and ownership boundaries still apply. Reviews that only inspect code must not trigger workflow mutations.

## Files and evaluation

* [Skill instructions](.agents/skills/git-manager-agent-skill/SKILL.md)
* [Handoff template](.agents/skills/git-manager-agent-skill/references/handoff-template.md)

The initial local trial passed 15 application tests and additional behavior comparisons. It exposed two workflow gaps that informed stronger instructions for staged diff review and commit context. The revised instructions have structural and scenario reviews, but have not completed another agent trial. Interruption recovery and blocked commits remain untested in that trial.

The dummy application used for evaluation is not included in this distribution. Use a separate disposable repository for further trials.

If upgrading from `git-hygiene-and-handoff`, review the old installation and migrate it deliberately. Avoid leaving both skill directories active.
