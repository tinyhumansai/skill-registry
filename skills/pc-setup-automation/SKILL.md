---
name: pc-setup-automation
description: Turnkey new-PC setup — Windows hardening, driver installs, privacy pruning, and a repeatable customer checklist that makes the lane profitable.
version: 1.0.0
license: MIT
tags:
  - windows
  - setup
  - automation
  - harleycoder
agent: any
---

# PC Setup Automation

Repeatable new-PC / refresh setup sold as a fixed service. Anchored at
$75-100/job, ~1.5 hours at bench speed. Uses the Dell bench pipeline:
Sysinternals suite + winget + registry policy tooling.

## When to use

New machine out of the box, reinstall after reset, or "make it fast
and private" refresh on a customer laptop.

## Workflow

1. Intake form: purpose (gaming/work/school), must-keep apps, account
   needs (local vs Microsoft), printers/peripherals, backup parent.
2. Baseline: record model, serial, OS build, driver inventory.
3. Updates first: Windows Update loop to current, then chipset/graphics
   NIC from manufacturer (not third-party updaters).
4. Removal pass: purge trialware and preinstalled bundles per a
   conservative list (never touch OEM recovery partitions).
5. Privacy pass: telemetry off, advertising ID off, delivery
   optimization off, location for non-required apps off — all via
   documented regkeys, written down for the customer.
6. Hardening (bundle it): UAC at notify, Defender on + tamper tools,
   firewall on, updates automatic, BitLocker where supported.
7. Application deck: agree the app list up front, install via winget
   manifest, save the manifest to the job folder for repeatability.
8. Verification + handoff: reboot clean, benchmark boot time, checklist
   signed in plain language, first-backup scheduled.

## Guardrails

- No account/financial access without written consent.
- Preserve OEM recovery; never remove without asking.
- Written records feed HarleyCoder memory + employment narrative.

## Output

Configured PC + manifest + signed checklist + scheduled backups.
Pricing anchor: $75-100 per job.