---
name: gsm-phone-unlock-repair
description: GSM device repair and unlock triage — Samsung and MediaTek tooling, ADB over USB/WiFi, and bailout paths without bricking customer hardware.
version: 1.0.0
license: MIT
tags:
  - gsm
  - android
  - repair
  - unlock
  - harleycoder
agent: any
---

# GSM Phone Unlock / Repair Triage

Field workflow for the phone-repair lane (the 3x/day $100 revenue
target). Covers Samsung ADB, MediaTek UART/dump paths, and EDL for
Qualcomm. Mirrors the Dell-side bench: mtkclient/edl/heimdall + ADB.

## When to use

Customer phone: stuck boot, FRP locked, no autorun, dead after OTA,
needs network/sim unlock on supported hardware.

## Workflow

1. Intake: model (Settings → About → Model number), Android version,
   carrier, symptom, whether it's carrier-subsidized (unlock rules
   differ), backup state.
2. Power/boot check: charger vs no-charge, download mode reachable?
3. Get a working data link FIRST:
   - Samsung: ADB over USB (then `adb tcpip 5555` for WiFi lane).
   - MediaTek: mtkclient preloader mode (vol-up + connect), `mtk r
     preloader` for a full read before any write.
   - Qualcomm: EDL via 9008; heimdall for Samsung Odin images.
4. Read BEFORE write: dump preloader/boot/NVRAM to the job folder.
   This is the rollback path that keeps us legal and safe.
5. Unlock/repair ladder:
   - FRP removal: only via manufacturer-legal paths (device reset with
     verified Google login, or supported tool) — no grey-market backdoors.
   - Network unlock: carrier portal or manufacture-supported service;
     NCK/UMT only where the activation tool validates legality.
6. Verify: boot, IMEI present (matches sticker), ADB sees device, SIM
   registers, Wi-Fi/camera/touch all test.
7. Record: model, IMEI, paths used, dumps taken, result, hours.

## Guardrails

- Never touch customer accounts/data without written consent.
- Read-first-dump always; zero-write to unknown devices.
- Unlock legality varies — always check the carrier's official policy
  and only use supported tools.

## Output

Working phone + job record (IMEI, dump hashes, steps) feeding the
HarleyCoder memory and the Second Chance Act employment narrative.