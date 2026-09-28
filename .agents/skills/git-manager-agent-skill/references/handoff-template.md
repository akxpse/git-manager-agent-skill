# Handoff: <task-slug>

Replace angle-bracketed fields with observed facts. Use the repository's existing handoff convention first. Omit inapplicable optional fields; retain essential recovery context. Report this document's final commit identifier in the final response, avoiding a self-referential hash.

## Status and goal

- Status: <ready for review | partial checkpoint | blocked>
- Goal: <intended outcome>
- Acceptance criteria: <criteria and whether each is satisfied>
- Actual changes: <implemented scope; distinguish unfinished work>

## Implementation and behavior

- Important files, entry points, and responsibilities: <paths and purposes>
- Contracts, constraints, decisions, and trade-offs: <reasoning; links to enduring documentation>
- Baseline behavior and preservation evidence: <existing behavior, characterization/regression coverage, observed comparisons>
- Separately authorized behavior changes: <changes and authorization, or none>
- Uncertain logic preserved: <locations and open questions>

## Validation and reproduction

| Exact command and working directory | Outcome | Evidence or reason |
| --- | --- | --- |
| <command; directory> | <passed / failed / not run> | <observed result or reason> |

Separate known baseline failures from task-introduced failures; identify unclassified failures. Include failing required checks and approved exceptions. Never infer success from unavailable output.

- Run/reproduce: <steps, prerequisites, or existing documentation>
- Human review: <actual review, or not performed>

## Security assessment

- Scope and visibility: <files, configuration, staged/outgoing commits, available history, and excluded or inaccessible areas>
- Checks: <exact commands, tool versions where relevant, passed/failed/unrun outcomes, and reasons; identify any external data disclosure authorization>
- Secret findings: <redacted locations and exposure status; never include credential values; owner notification and rotation/revocation status>
- Code and package findings: <affected path or package/version, direct/transitive dependency, dated authoritative advisory links, severity, confidence, and reachability evidence>
- Classification: <baseline versus introduced findings; confirmed issues, suspected issues, false positives, and rationale>
- Disposition: <authorized fix and validation, unresolved blocker, approved exception, owner, and next action>

A clean scan is not proof of security. Preserve uncertainty and tool/history limitations; do not mark unrun checks as passed.

## Branches and recovery

- Task branch and inspected base: <verified names and base commit>
- Dependencies and overlapping work: <branches, worktrees, or pull requests>
- Visibility limitations: <unavailable or stale information>
- Integration verification: <authorized combined checks, or not verified>
- Checkpoint protection: <local only / confirmed pushed to authorized remote branch / not committed because of exact blocker>
- Remaining changes: <task-owned changes; separately identify pre-existing work>
- Limitations, blockers, and next concrete action: <precise continuation steps>
- Recovery/rollback considerations: <when relevant; safeguards>

## Initial adoption (optional)

Record audited areas and baseline, concrete findings and acceptance criteria, remediation commit references, validation evidence, approved exceptions, unresolved blockers, and completion status. For partial adoption, identify the next area or finding before ordinary task implementation.
