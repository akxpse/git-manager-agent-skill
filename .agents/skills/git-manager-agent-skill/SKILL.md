---
name: git-manager-agent-skill
description: "Use in Codex when implementing, fixing, refactoring, resuming, or handing off Git changes to preserve behavior, assess security, verify checkpoints, and leave durable handoffs."
---

# Git Manager Agent Skill

Codex only. Follow: understand → select increment → implement → validate → review diff → checkpoint → repeat → hand off.

Respect higher-priority instructions, including commit/push prohibitions; disclose limitations. Read-only reviews must not create branches, edit, commit, or push. Without a repository, propose contents; do not initialize Git.

## Inspect ownership and branches

Read applicable instructions, contribution guidance, relevant code/tests, and branch/commit conventions. Identify agreed base/destination; never assume `main` or `origin`.

Inspect branch/HEAD, staged/unstaged changes, untracked files, and merge/rebase state. Identify ownership. Never overwrite, discard, stage, unstage, or commit others' work without explicit authorization. Isolate ambiguous ownership in a worktree or stop affected operations.

Inspect available branches/worktrees and accessible PRs for overlap; record dependencies and visibility limits, including stale references. Coordinate overlapping edits or pause. Worktrees isolate files/indexes, not semantic conflicts.

Before editing, create a named task branch from the agreed base or confirm same-task ownership. Resolve detached HEAD first. Never commit agent work to `main`, `master`, default, protected, or shared integration branches. Follow conventions; otherwise use `agent/<task-slug>`.

Keep branches focused and remediation separately reviewable. Record dependencies/bases. Target review-readiness within one working day; reassess scope/blockers after two. These configurable targets never justify unfinished merges or history manipulation.

## Complete initial adoption

For mutating tasks, initially audit all project-owned code, tests, configuration, and documentation read-only. Exclude generated/vendor/dependency code from refactoring. Record evidence-backed maintainability, continuity, and security findings, baseline checks, and acceptance criteria. On the task branch, remediate repository-wide before ordinary implementation; avoid speculative redesign.

Persist scope, baseline, findings, criteria, remediation commits, validation, blockers, and completion using repository conventions or `docs/handoffs/git-hygiene-adoption.md`. Commit the record. If blocked, preserve/checkpoint progress; report partial/blocked adoption and record approved exceptions. Never silently bypass adoption.

Later, verify the completed record and intervening changes, complete missing adoption, and revisit invalidated findings; otherwise focus on task-related code. Never manufacture historical compliance.

## Preserve behavior and clarity

Inspect callers, dependencies, configuration, contracts, and documentation. Run baseline checks; record failures. Before consequential refactoring, add missing characterization coverage, including failure/edge cases. Tests support, not prove, equivalence.

Retain responsibilities, contracts, validation, errors, side effects, ordering, concurrency, defaults, and edge cases. Never delete apparently obsolete/duplicate/unreferenced logic based on search alone; consider indirect calls, configuration, dynamic loading, migrations, and external consumers. Preserve uncertainty and record questions. Behavior changes require separate task authorization, criteria, and validation; existing authorization counts. Never remove checks, tests, or features to simplify cleanup or pass checks.

Follow architecture, idioms, style, and dependencies. Prefer clear names, cohesive units, explicit control flow/errors, and simple designs. Avoid broad rewrites, unnecessary dependencies, speculative abstractions, mass renames/moves, and blanket formatting. Explain non-obvious invariants/reasoning near code; document public contracts. Update affected setup/API/configuration/migration/operational documentation and existing decision records proportionately.

## Assess security

During adoption, inspect project files, hidden configuration, manifests/lockfiles, and available history. Before checkpoints inspect changed/staged content; before pushing inspect outgoing commits. Use approved secret scanners with redacted output for API keys, tokens, passwords, and private keys. Never print secret values or test credentials against services. If suspected live secrets would enter a commit/push, stop that operation, preserve files, and report redacted locations. Request owner rotation/revocation; deleting current text does not remove historical exposure. Never rewrite history automatically.

Review relevant data flows for injection, broken authentication/authorization, unsafe deserialization, path traversal, insecure cryptography/TLS, sensitive logging, and excessive permissions. Use available project security checks. Assess direct/transitive package versions against current authoritative advisories; record affected versions, reachability, and fixes. Do not infer safety from package names, missing tools, or empty results.

Record scope/history limits, commands/outcomes, dated advisory references, severity, confidence, baseline versus introduced findings, false positives, and unrun checks/reasons in adoption/handoff records. Redact evidence. Do not upload code, secrets, or dependency inventories to external scanners without authorization. Missing tools/connectivity mean incomplete assessment; do not install tooling without authorization. Prioritize concrete risks; no blind upgrades, forced audit fixes, removed safeguards, or suppressed findings. Apply authorized, tested fixes. Unresolved actionable findings block affected delivery pending remediation or an explicitly approved exception. Never claim security certification.

## Validate and checkpoint

State acceptance criteria and logical increments; keep trivial tasks trivial. Commit each coherent increment before another substantial increment, including related tests/docs. Separate unrelated changes without splitting coupled work artificially.

Before normal commits:

- Run relevant checks and readable behavior/regression tests.
- Review working and complete staged diffs for lost conditions/defaults, side effects, ordering, and weakened validation.
- Account for the entire index; stage only reviewed task-owned paths/hunks. Isolate/stop unrelated staged work.
- Check secrets, debug output, artifacts, and scope; never blindly bulk-stage or commit-all.
- Inspect staged output before committing in a separate tool call.
- Include non-obvious rationale and exact validation commands/outcomes, including failed/unrun checks, in nontrivial commit bodies.

Follow message conventions; otherwise use descriptive subjects and rationale/validation bodies. Avoid vague/empty commits. Verify success, record actual identifiers, and inspect remaining changes; never invent results.

Target checkpoints within 15 minutes of active editing, checked at task/tool boundaries. Prefer earlier completed increments. Checkpoint before lengthy operations, risky changes, interruptions, handoffs, or session end. This is not a timer/service.

Normal commits are coherent and validated. When a checkpoint is due or interruption threatens incomplete progress, commit only on task branches where policy permits: use conventions or `wip(<scope>): checkpoint <progress>`. Record working behavior, gaps, failed/unrun checks, and next action. Ownership, diff, and secret checks still apply. Never present recovery as tested, complete, or review-ready.

If blocked, preserve files, report the exact blocker immediately, and establish permitted recovery before substantial further editing. Persist recovery notes; disclose them uncommitted, not checkpoints. Never bypass hooks, signing, permissions, or identity requirements.

## Integrate and protect

Never automatically merge, rebase, cherry-pick, delete branches, rewrite history, force-push, destructively reset, clean, stash, or disable safeguards as hygiene.

For authorized integration, inspect the ancestor and both versions; preserve both intended behaviors, never blindly choose one conflict side. Review/validate combined changes; stop conflicting requirements. Reassess overlap/validation when bases advance; disclose unverified integration.

Local commits cannot protect against disk/workspace/repository loss or guarantee power-loss safety. Push only explicitly authorized task branches/destinations after reviewing outgoing commits; verify success. Never force-push or push all/protected branches. Do not change remotes/credentials/identity without authorization. Unauthorized/unavailable pushes leave local-only exposure; staging, stashes, and attempted pushes are not remote backups.

## Hand off

Persist incomplete recovery context in commit bodies. For nontrivial/incomplete work, commit notes using repository conventions or `docs/handoffs/<task-slug>.md` and [the template](references/handoff-template.md). Trivial completed changes need a useful commit and final summary.

Keep enduring knowledge in documentation/code. Verify developers without chat can locate entry points, understand constraints, run checks, and modify safely. Fix confusing code; never imply human review occurred unless it did.

Ready requires satisfied criteria, passed required checks or approved exceptions, understandable code, current documentation, and committed work. Otherwise report precise gaps. Clean trees prove neither correctness nor completeness; never discard unrelated work.

Report verified branch/commit, task-owned versus pre-existing changes, and remote status: local only, confirmed pushed, or not committed with blocker.

Guidance reduces risk; it cannot guarantee secure code, bug-free refactoring, recovery, data preservation, or compliance.
