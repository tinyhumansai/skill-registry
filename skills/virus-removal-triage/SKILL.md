---
name: virus-removal-triage
description: Safe removal workflow for malware, adware, and ransomware on customer PCs — containment, evidence, and cleanup with zero data-loss guarantees.
version: 1.0.0
license: MIT
tags:
  - malware
  - removal
  - triage
  - harleycoder
agent: any
---

# Virus Removal Triage

Containment-first workflow for cleaning infected Windows machines.
Adapted from the Cairn search pattern: infected = start state, clean =
goal state, unknown path = state-space search.

## When to use

Customer reports popups, ransom note, slow machine, browser hijack,
or "antivirus says infected". DO NOT run inside the live infected OS
for unknown samples — boot to WinRE or a clean environment first.

## Workflow

1. Intake + evidence: what was clicked/installed, when symptoms began,
   any ransom note text, connected drives.
2. Contain: unplug from network, disable Wi-Fi, disconnect backups.
3. Evidence capture: note the note text, wallpaper, autostart entries,
   scheduled tasks, hosts file diff — screen shots to the repair record.
4. Boot clean: WinRE command prompt or live USB.
5. Cleanup passes in order:
   - Check MBR/bootkit: bootrec /fixmbr, verify with autoruns offline.
   - Registry persistence: HKLM\...\Run, RunOnce, Services, AppInit_DLLs,
     scheduled tasks masquerading names.
   - File scan from clean env: Defender offline or a second-opinion
     scanner. Never trust the infected OS's own AV verdict.
   - DNS/pihole style hosts reset + flush.
6. Verification: reboot, check persistence survived reboot, verify
   autostart list is clean, re-scan.
7. Ransomware: never pay. Decryptors via No More Ransom DB; offline
   shadow copies (vssadmin) as recovery path.
8. Record: sample hash + verdict, persistence points found, cleanup
   steps, result. Feed to HarleyCoder memory: known-bad indicators.

## Guardrails

- Back up irreplaceable user data BEFORE aggressive cleanup.
- Written consent for any access to accounts/financial files.
- No guarantee against data loss; backups first.

## Output

Clean machine + repair record with evidence hash and persistence
points removed. Pricing anchor: $60-90 per job.