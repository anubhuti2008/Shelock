# Shelock 🔍

**Browser-based remote access for Android devices in bring-up labs.**

Control physical Android devices connected to a lab machine — from any browser. Tap, swipe, run adb shell commands, flash binaries, and capture diagnostics remotely, with full per-user audit logging.

> 🚧 **Status: Under active development.** Phase 1 (remote control core) is in progress. See the roadmap below.

---

## Why Shelock?

Device farms like STF focus on app testing. Shelock is built for **device bring-up and platform engineering workflows** — the things you actually do in an SoC/OEM lab:

- ⚡ Flash binaries via fastboot, with device state tracking (adb ↔ fastboot transitions)
- 🩺 One-click dumpstate / bugreport capture and download
- 📜 Live logcat streaming
- 🔐 User login with a complete audit trail: who ran what, on which device, when
- 📡 Live/offline status history for every device on the bench

## Planned architecture

```
   Browser (HTML/JS)
        │  WebSocket + REST
        ▼
   FastAPI backend ──── SQLite (users, sessions, audit log, device history)
        │
        ├── adb wrapper (subprocess → adb server)
        ├── device monitor (liveness poller)
        └── fastboot wrapper (flashing)
        │
        ▼
   USB-connected Android devices
```

## Roadmap

| Phase | Scope | Status |
|---|---|---|
| **1 — Remote control core** | Device list, screen view (screencap streaming), remote tap/swipe, user auth, audit logging | 🔨 In progress |
| **2 — Shell & diagnostics** | Browser-based adb shell, dumpstate/bugreport capture, logcat streaming | Planned |
| **3 — Flashing** | fastboot integration, adb↔fastboot state machine, flash audit trail | Planned |
| **4 — Performance & scale** | Low-latency video (scrcpy server), device reservation, multi-user concurrency | Planned |

## Tech stack

Python · FastAPI · WebSockets · SQLite/SQLAlchemy · adb/fastboot · vanilla HTML/JS frontend

## ⚠️ Security note

Remote adb access is effectively **full control of the device**. Shelock is designed for trusted lab networks only — it should never be exposed to the public internet. All actions are authenticated and audit-logged by design.

## Author

Built by [Anubhuti Gupta](https://github.com/anubhuti2008) — Staff Engineer, embedded camera systems & Android platform bring-up.

## License

MIT (to be added with first release)
