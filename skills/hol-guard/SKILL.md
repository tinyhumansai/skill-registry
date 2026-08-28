---
name: hol-guard
description: Protect supported local AI coding-agent runtimes with HOL Guard before mutation-bearing tool work.
license: Apache-2.0
metadata:
  author: "kantorcodes"
  version: "1.0.0"
  tags: "security,runtime-safety,ai-agents,coding-agents"
---

## Instructions

Use this skill when an AI agent needs to establish HOL Guard around a supported local coding-agent harness before state-changing or otherwise high-impact tool work.

HOL Guard is an additive local runtime boundary. It does not replace the agent client's authentication, permissions, sandboxing, confirmations, repository policy, target-service authorization, tests, backups, or human review. OpenHuman itself is not claimed as a HOL Guard-supported harness. When this skill is invoked from OpenHuman, it can only establish protection for a separate local harness that the user actually intends to launch through Guard.

### Install and verify HOL Guard

If HOL Guard is not already available and installation is in scope, prefer an isolated install:

```bash
pipx install hol-guard
hol-guard --version
```

Discover current supported local harnesses instead of guessing an adapter name:

```bash
hol-guard detect --json
```

Before bootstrap, install, dry-run, doctor, or protected launch, identify the exact local harness the user intends to run. Continue only if that same harness is present in Guard's detection result. If the intended harness is absent, unsupported, or ambiguous, stop. Do not substitute a different healthy detected harness and do not claim that a detected harness protects OpenHuman's own tool calls.

For Hermes, use its harness-specific bootstrap path:

```bash
hol-guard hermes bootstrap
```

For other supported harnesses, use the Guard-owned setup flow for the exact detected target:

```bash
hol-guard bootstrap
hol-guard install <harness> --json
hol-guard run <harness> --dry-run --json
hol-guard doctor <harness> --json
```

Do not claim protection merely because the package installed. Continue only when Guard reports that same selected harness as installed and healthy.

### Run protected work

Launch that exact supported harness through Guard:

```bash
hol-guard run <harness> --json
```

Treat a Guard deny, review-required decision, error, malformed result, or unhealthy installation as a stop condition for the protected mutation. On fail-closed harness/event paths, an unavailable Guard runtime or timeout is also a stop condition. Some supported integrations are explicitly fail-open when their native hook crashes or times out; for those paths, do not claim the failure was blocked, and do not perform the state-changing operation unless an independently verified fail-closed protection path is in place. Never retry a blocked or unresolved state-changing action through an unprotected agent session.

After work, inspect Guard-owned state and evidence as needed:

```bash
hol-guard status --json
hol-guard approvals --json
hol-guard receipts --json
```

If an approval is required, preserve the normal human approval flow. Do not fabricate or auto-resolve an approval.

### Scope boundaries

- HOL Guard protects the supported local harness launched through Guard; it does not protect OpenHuman itself merely because this skill is installed.
- HOL Guard does not claim to run inside unrelated hosted products or APIs.
- Keep the target service's native RBAC, validation, confirmation, audit, and safety controls authoritative.
- Use `hol-guard detect --json` as the source of truth for current harness support and fail-open/fail-closed behavior documented by the installed Guard version.
- Do not execute a destructive target action merely to test whether Guard would block it.
- Guard Cloud is optional; local protection must not silently opt a user into cloud sync.

Canonical project: https://github.com/hashgraph-online/hol-guard

## Examples

**Protect a supported coding-agent session before a deployment workflow:**

```text
User: Use HOL Guard before my coding agent performs the deployment.
Agent: I will first identify the exact local harness you intend to run, confirm that same harness appears in HOL Guard detection, verify it is installed and healthy, run the Guard dry-run, and only then launch that harness through HOL Guard before any deployment mutation.
```

**Stop when Guard requires review:**

```text
User: Continue with the production-changing command.
Agent: HOL Guard returned a review-required decision. I will not bypass it or retry through an unprotected session; the action remains stopped until the normal approval flow is resolved.
```

**Do not overclaim the boundary:**

```text
User: Does installing this skill mean OpenHuman itself is protected by HOL Guard?
Agent: No. This skill can launch a separately supported local harness through HOL Guard, but it does not turn the current OpenHuman session into a Guard-protected harness.
```

## Dependencies

- Python 3.10+
- `pipx` recommended for isolated installation
- `hol-guard` package from PyPI
- A local AI coding-agent harness reported as supported by `hol-guard detect --json`
