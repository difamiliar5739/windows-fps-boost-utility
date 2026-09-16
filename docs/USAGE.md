# Usage Guide

Complete guide to using **Windows FPS Boost Utility** — from first launch to advanced tuning.

---

## 📑 Table of Contents

- [First Launch](#first-launch)
- [Dashboard](#dashboard)
- [Game Profiles](#game-profiles)
- [Optimization Modules](#optimization-modules)
- [Quick Tools](#quick-tools)
- [Performance Overview](#performance-overview)
- [Custom Profiles](#custom-profiles)
- [Rollback](#rollback)
- [Hotkeys](#hotkeys)
- [CLI Mode](#cli-mode)
- [Files & Data](#files--data)
- [FAQ](#faq)

---

## 🚀 First Launch

When you launch the app for the first time:

1. **Run as Administrator** — required to modify registry, services, and power plans.
2. The app creates:
   - `config.json` — from `config.example.json`
   - `settings.ini` — default UI settings
   - `data/data.dat` — logs, FPS history, backups
3. You'll be asked to choose a **Game Profile**: Competitive, Balanced, or Maximum Performance.
4. Click **⚡ Optimize Now** to apply all tweaks.

> ⚠️ A system reboot is recommended after the first optimization.

---

## 🖥️ Dashboard

The main screen shows real-time performance metrics.

### Top KPI Cards

| Card | Meaning | Typical value |
|------|---------|---------------|
| **FPS Boost** | Average FPS increase after optimization | +35% |
| **Latency Reduction** | Network + input latency decrease | −42% |
| **System Response** | Overall system responsiveness score | 98% |
| **Optimization Status** | Current system state | Optimal / Needs Optimization |

### Profile Selector (top-right)

Dropdown with available game profiles. Changing the profile updates the recommended tweaks immediately.

### 🟢 Optimize Now button

Applies every tweak for the selected profile in one click. Progress is shown module by module.

---

## 🎯 Game Profiles

| Profile | Best for | Character |
|---------|----------|-----------|
| **Competitive (Esports)** | CS2, Valorant, Overwatch, Apex | Max FPS, lowest latency, aggressive tweaks |
| **Balanced** | Mixed gaming + work | Safe defaults, moderate impact |
| **Maximum Performance** | Benchmarking, stress tests | Most aggressive, higher power draw & heat |

### What changes per profile

| Tweak | Competitive | Balanced | Maximum |
|-------|:-----------:|:--------:|:-------:|
| Disable GameDVR | ✅ | ✅ | ✅ |
| MMCSS priority High | ✅ | ⚪ | ✅ |
| Disable Nagle | ✅ | ⚪ | ✅ |
| Clear standby list | ✅ | ✅ | ✅ |
| GPU High Performance | ✅ | ⚪ | ✅ |
| HAGS enabled | ✅ | ⚪ | ✅ |
| Aggressive service kill | ⚪ | ⚪ | ✅ |

✅ = enabled · ⚪ = disabled

---

## ⚙️ Optimization Modules

Each module shows `applied / total` tweaks. Click a module card to see the detailed list and toggle individual tweaks.

### ⚙️ System Optimization (18/18)

Windows-level tweaks:
- Disable GameDVR & Game Bar
- Disable fullscreen optimizations
- Set MMCSS (Multimedia Class Scheduler) priority to **High**
- Disable Xbox Game Bar overlay
- Disable telemetry services
- Switch to **High Performance** power plan
- Disable Windows Search indexing on game drives
- Disable Superfetch on SSDs
- …and 10 more

### 📡 Network Optimization (12/12)

Latency and stability:
- Disable Nagle's algorithm (`TcpAckFrequency`, `TCPNoDelay`)
- TCP ACK frequency tuning
- Disable QoS reserved bandwidth (`NonBestEffortLimit = 0`)
- Network throttling index = 0
- Disable auto-tuning for low-latency links
- …and 7 more

### 🧠 Memory Optimization (8/8)

RAM hygiene:
- Clear standby memory list
- Enable **Large System Cache**
- Disable Paging Executive (optional — off by default)
- Clear temp files on start
- …and 4 more

### 🎮 Game Optimization (15/15)

Game-specific:
- Set game process priority to **High**
- Set GPU preference to **High Performance** (`UserGpuPreferences`)
- Enable Hardware-Accelerated GPU Scheduling (HAGS)
- Disable Game Bar overlay per-game
- Disable Variable Refresh Rate conflicts
- …and 10 more

---

## 🛠️ Quick Tools

Available in the right sidebar.

| Tool | Description |
|------|-------------|
| **Game Mode** (toggle) | Enable/disable Windows Game Mode |
| **Memory Cleaner** (button) | Instantly free up RAM (clear standby list) |
| **Startup Manager** (button) | Open a panel to manage startup programs |
| **Service Optimizer** (button) | One-click disable of non-essential services |

> 💡 **Memory Cleaner** is safe to run while gaming — it doesn't kill processes, only clears standby memory.

---

## 📊 Performance Overview

Real-time graphs in a 60-second window. Switch between **Real-time**, **1m**, **5m**, **15m** views.

| Metric | Source | Notes |
|--------|--------|-------|
| **FPS** | PresentMon | Requires the game to run in exclusive fullscreen or borderless |
| **Latency** | NVIDIA Reflex / AMD Anti-Lag | Only on supported GPUs & games |
| **CPU Usage** | Windows Performance Counters | System-wide, not per-process |

### Reading the graphs

- **Flat FPS line** = stable frametimes ✅
- **Spikes** = stutter (check background processes)
- **Latency > 30 ms** = network issue or GPU-bound frame
- **CPU > 90%** = CPU bottleneck

---

## 🧩 Custom Profiles

You can create your own profiles instead of using presets.

1. Sidebar → **Profiles** → **New Profile**
2. Name it (e.g., `Streaming`)
3. Toggle modules and individual tweaks
4. Save — it appears in the profile dropdown

Profiles are stored in `config.json`:

```json
{
  "custom_profiles": {
    "Streaming": {
      "system": { "disable_gamedvr": true, "mmcss_priority": "normal" },
      "network": { "tcp_optimize": true },
      "memory": { "clear_standby_list": false },
      "game": { "gpu_preference": "high_performance" }
    }
  }
}