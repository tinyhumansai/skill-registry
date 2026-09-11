---
name: windows-repair-triage
description: Diagnostic workflow for repairing Windows PCs — boot failures, login loops, driver problems. Converts a walk-in repair job into a safe, ordered action plan.
version: 1.0.0
license: MIT
tags:
  - windows
  - repair
  - triage
  - harleycoder
agent: any
---

# Windows Repair Triage

Scheme: agentskills.io / OpenHuman SKILL.md. This skill runs a structured
Windows repair intake and returns a prioritized action plan.

## When to use

- Customer machine won't boot, loops at login, or throws BSOD on load.
- Before touching anything, run intake: symptom, last change, data-backup
  status, power state, external drives attached.

## Workflow

1. Collect: symptom + last known-good state + what changed recently
   (update, driver, new software, removal).
2. Confirm backup state FIRST. If data is unprotected, stop and offer
   backup before any repair step. Document refusal in writing.
3. Boot-order triage:
   - No power: PSU/charger test before anything else.
   - No POST: reseat RAM/disk, clear CMOS, check beep codes.
   - POST but no OS: bootrec /fixmbr /fixboot /rebuildbcd.
   - OS boots, login loop: clear Winlogon AutoLogon keys via offline
     registry (load SYSTEM/SOFTWARE hives), disable LSA RunAsPPL to test.
4. Driver/update rollbacks: use Windows.old and restore points BEFORE
   reinstalling.
5. Only after safe-mode confirmed working, consider in-place repair
   (sfc /scannow, DISM) then reset as last resort.
6. Write the record: machine, symptom, steps, result, hours. This feeds
   the HarleyCoder memory (TencentDB-Agent-Memory 4-tier) so the next job
   of the same class is faster.

## Guardrails

- Never touch accounts, financial data, or licensed software without
  written consent.
- No guarantee against data loss — always lead with backup.
- Chargeable deltas: diagnosis $30-50, repair $60-120 per job tier.

## Output

A repair ticket: intake, plan, executed steps, verification, follow-up.