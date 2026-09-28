---
name: git-manager-agent-skill
description: "Use in Codex when implementing, fixing, refactoring, resuming, or handing off Git repository changes to preserve behavior, create verified checkpoints, and leave durable handoffs."
---

# Git Manager Agent Skill

This version supports Codex only.

Follow: understand → select a small increment → implement → validate → review the diff → checkpoint → repeat → hand off.

Respect higher-priority instructions, including commit/push prohibitions; disclose limitations. Read-only reviews require no branches, edits, commits, or pushes. Without a repository, return proposed contents; do not initialize Git.

## Inspect and establish ownership

Read applicable instructions, contribution guidance, relevant code/tests, and branch/commit conventions. Identify the agreed base and intended remote; never assume `main` or `origin`.

Inspect branch/HEAD, staged/unstaged changes, untracked files, and merge/rebase state. Identify pre-existing ownership. Never overwrite, discard, stage, unstage, or commit others' work without explicit authorization. For mixed/ambiguous ownership, isolate safely in a worktree or stop the affected operation and explain.

Inspect available branches, worktrees, and accessible PR context for overlap; record dependencies and visibility limits. Cached references may be stale. Sequence overlapping edits or establish ownership before changing shared code; pause affected edits if coordination is unresolved. Worktrees isolate files/indexes, not semantic conflicts.

## Complete initial adoption

For mutating tasks, initially audit all project-owned code, tests, configuration, and documentation read-only. Establish the dedicated branch below before adoption edits. Exclude generated/vendor/dependency code from refactoring. Record concrete maintainability/continuity gaps, evidence, baseline checks, and acceptance criteria. Remediate findings repository-wide in reviewable increments before ordinary task implementation; avoid speculative redesign.

Persist adoption scope, baseline, findings, acceptance criteria, remediation commits, validation, blockers, and completion using the repository convention or `docs/handoffs/git-hygiene-adoption.md`. Commit this record. If blocked, preserve/checkpoint progress and report partial or blocked adoption; do not silently proceed. Record explicitly approved exceptions.

Later, inspect the completed record and relevant intervening changes, then focus on task-related code. Complete missing/incomplete adoption; revisit conclusions invalidated by evidence. Apply workflow rules prospectively; never manufacture historical compliance.

## Establish a dedicated branch

Before editing, create a named task branch from the agreed base or confirm the current branch belongs to this task. Resolve detached HEAD first. Never commit agent work directly to `main`, `master`, default, protected, or shared integration branches. Follow naming conventions; otherwise use `agent/<task-slug>`.

Keep branches task-focused and remediation separately reviewable from features. Record dependent branches and verified bases. Default to review-readiness within one working day; after two working days, reassess scope/dependencies/blockers. These configurable targets never justify unfinished merges or history manipulation.

## Preserve behavior while improving clarity

Inspect callers, dependencies, configuration, contracts, and documentation. Run relevant baseline checks and record existing failures before changing logic. Before consequential refactoring, add focused characterization coverage where protection is missing, including failure/edge cases. Tests support, not prove, equivalence.

Retain responsibilities, contracts, validation, errors, side effects, ordering, concurrency behavior, defaults, and edge cases. Never delete apparently obsolete/duplicate/unreferenced logic based on search alone; consider indirect calls, configuration, dynamic loading, migrations, and external consumers. Preserve uncertain logic and record questions. Keep intentional behavior changes separate from cleanup; require explicit task authorization (existing authorization counts), acceptance criteria, and validation. Never delete checks, tests, or features to simplify cleanup or pass checks.

Follow established architecture, idioms, style, and dependencies. Prefer clear names, cohesive units, explicit control flow, understandable errors, and simple designs. Avoid broad rewrites, unnecessary dependencies, speculative abstractions, mass renames/moves, and blanket formatting. Explain non-obvious reasoning/invariants near code; document public contracts. Update affected setup/API/configuration/migration/operational documentation and use existing decision-record conventions proportionately.

## Validate and checkpoint increments

State acceptance criteria and a few logical increments. Keep trivial tasks trivial. Commit each completed coherent increment before another substantial increment; include related tests/docs. Separate unrelated changes without artificially splitting coupled work.

Before each normal commit:

- Run relevant available checks; include readable behavior/regression tests.
- Inspect working and complete staged diffs, including lost conditions, defaults, side effects, ordering, and weakened validation.
- Account for the entire index; stage only reviewed task-owned paths/hunks. Isolate or stop if unrelated staged work could enter the commit.
- Check secrets, debug output, artifacts, and scope. Never blindly bulk-stage or commit-all.
- Inspect the completed staged-diff output before invoking commit in a separate tool call; printing and committing in one call is not review.
- For nontrivial checkpoints, include non-obvious rationale and exact validation commands/outcomes in the commit body; identify failed/unrun checks.

Follow commit conventions; otherwise use descriptive subjects and short bodies explaining non-obvious rationale/validation. Avoid vague messages and empty/meaningless commits. Verify success, record the actual identifier, and inspect remaining changes; never invent results.

Target checkpoints within 15 minutes of active editing, checking elapsed time at task/tool boundaries. Prefer earlier completed increments. Checkpoint task-owned changes before lengthy operations, risky changes, interruptions, handoffs, or session end. This is a workflow target, not a timer/service.

Normal commits contain coherent, appropriately validated changes. When a checkpoint is due or interruption threatens meaningful progress, use a recovery commit if no coherent increment is ready, only on dedicated task branches where policy permits. Use repository conventions or `wip(<scope>): checkpoint <progress>`; record what works, incompleteness, failed/unrun checks, and the next action. Recovery commits still require ownership, diff, and secret checks. Never label them tested, complete, or review-ready.

If no permitted checkpoint is possible, preserve files, report the exact blocker immediately, and establish permitted recovery before substantial further editing. Persist recovery notes in the permitted handoff file; report them uncommitted. Notes alone are not a checkpoint. Never bypass hooks, signing, permissions, or identity requirements.

## Coordinate integration and remote protection

Never automatically merge, rebase, cherry-pick, delete branches, rewrite history, force-push, destructively reset, clean, stash, or disable safeguards as hygiene.

For authorized integration, inspect the common ancestor and both versions; preserve both intended behaviors. Never blindly accept an entire conflict side. Review and validate the combined result; stop affected integration when requirements conflict. If the base advances, reassess overlap/validation; disclose unverified integration.

Local commits do not protect against disk/workspace/repository loss or guarantee power-loss safety. After checkpoints, push only when destination and action are explicitly authorized. Verify destination/outgoing commits; push only the intended task branch; never force-push, push all branches, or publish to protected branches. Do not change remotes, credentials, or identity without authorization. Verify push success. Unauthorized/unavailable pushes leave local-only exposure; staging, stashes, and attempted pushes are not remote backups.

## Leave durable continuity

Persist incomplete recovery context in commit bodies. For nontrivial/incomplete handoffs, follow repository conventions or create `docs/handoffs/<task-slug>.md`, using [the handoff template](references/handoff-template.md). Commit task-owned notes with the work. Trivial completed changes need a useful commit and final summary; avoid transcripts/diaries.

Keep enduring knowledge in normal documentation/code. Review whether a developer without chat can locate entry points, understand constraints, run checks, and safely modify behavior. Fix confusing code; never imply human review occurred.

Mark ready for review only when acceptance criteria hold, required validation passed or exceptions were explicitly approved, code is understandable, documentation current, and task-owned work committed. Otherwise report precise partial/blocked gaps. Clean trees do not prove correctness; never discard unrelated work.

Report verified branch, final local commit, remaining task-owned changes, and pre-existing changes separately. State remote status: “Local only,” “Confirmed pushed to the authorized remote branch,” or “Not committed because of a stated blocker.”

This guidance reduces risk; it cannot guarantee bug-free refactoring, interruption recovery, data preservation, or agent compliance.
