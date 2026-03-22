<p align="center">
  <img src="https://raw.githubusercontent.com/XDCIndia/.github/main/profile/xdc-india-logo.png" width="120" alt="XDC India">
</p>

<h1 align="center">🇮🇳 XDC India</h1>

<p align="center">
  <strong>Multi-client blockchain infrastructure for <a href="https://xdc.org">XDC Network</a></strong><br>
  Building client diversity and enterprise-grade tooling for the XDC ecosystem.
</p>

<p align="center">
  <a href="https://xdcindia.com">Website</a> •
  <a href="https://skynet.xdcindia.com">SkyNet</a> •
  <a href="https://stats.xdcindia.com">Ethstats</a> •
  <a href="https://api.xdcindia.com">API</a>
</p>

---

## 🔧 Blockchain Clients

| Client | Language | Branch | Status | Description |
|--------|----------|--------|--------|-------------|
| **GP5** | Go | `xdc-network` | 🟢 Active | Next-gen geth fork — XDPoS v1+v2, 28x sync speed |
| **Erigon-XDC** | Go | `feature/xdc-network` | 🟢 Active | High-performance Erigon — eth/62-63 protocol |
| **Nethermind-XDC** | C# | `main` | 🟢 Active | .NET client — state root bypass, 300K+ blocks |
| **Reth-XDC** | Rust | `xdcnetwork-rebase` | 🟡 WIP | Fastest execution layer — FCU feeder sync |

## 🛠️ Infrastructure

| Project | Description |
|---------|-------------|
| **XDC Node Setup** | Enterprise CLI toolkit — Docker, multi-client, SkyNet monitoring |
| **SkyNet** | Network health monitoring — fleet-wide dashboards + API |
| **SkyOne** | Per-node monitoring agent — auto-heal, heartbeats, alerts |
| **Ethstats** | Real-time block propagation and peer statistics |

---

## 🏗️ Current Architecture (Single Client)

> How XDC Network runs today — one client, limited tooling

```
┌───────────────────────────────────────────────┐
│               XDC Network                      │
│            (XDPoS Consensus)                   │
├───────────────────────────────────────────────┤
│                                               │
│           ┌─────────────────┐                 │
│           │  XDC v2.6.8     │ ← Single client │
│           │  (geth fork)    │   for ALL nodes  │
│           └────────┬────────┘                 │
│                    │                          │
│   ┌────────┬───────┼───────┬────────┐        │
│   │ Node 1 │ Node 2│ Node 3│ Node N │        │
│   │ v2.6.8 │ v2.6.8│ v2.6.8│ v2.6.8 │        │
│   └────────┴───────┴───────┴────────┘        │
│                                               │
│   Monitoring: ❌ Basic ethstats only          │
│   Alerting:   ❌ None                         │
│   Auto-heal:  ❌ Manual restarts              │
│   Diversity:  ❌ Single point of failure      │
└───────────────────────────────────────────────┘
```

---

## 🚀 Future-Ready Architecture (Multi-Client + SkyNet)

> What XDC India is building — 4 clients, full observability, self-healing

```
┌────────────────────────────────────────────────────────────┐
│                     XDC Network                             │
│                 (XDPoS v1 + v2 Consensus)                  │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  ┌────────┐  ┌────────┐  ┌──────────┐  ┌────────┐        │
│  │  GP5   │  │ Erigon │  │Nethermind│  │  Reth  │        │
│  │  (Go)  │  │  (Go)  │  │  (C#)   │  │ (Rust) │        │
│  └───┬────┘  └───┬────┘  └───┬──────┘  └───┬────┘        │
│      └───────────┴───────────┴──────────────┘             │
│              Unified P2P Layer                             │
│      eth/62 + eth/63 + eth/100 (XDPoS v2)                │
├────────────────────────────────────────────────────────────┤
│                                                            │
│  ┌──────────── SkyNet (Network Brain) ────────────┐       │
│  │  Dashboard │ REST API │ Alerting │ Fleet Health │       │
│  └────────────────────────────────────────────────┘       │
│                                                            │
│  ┌──────────── SkyOne (Node Agent) ───────────────┐       │
│  │  Heartbeats │ Auto-heal │ Stall Detection      │       │
│  │  Storage Monitor │ Client-agnostic             │       │
│  └────────────────────────────────────────────────┘       │
│                                                            │
│  ┌──────────── Ethstats (Live View) ──────────────┐       │
│  │  Real-time block propagation across all clients │       │
│  └────────────────────────────────────────────────┘       │
└────────────────────────────────────────────────────────────┘
```

---

## ⚡ XDC v2.6.8 vs Multi-Client Comparison

| Feature | XDC v2.6.8 (Current) | GP5 | Erigon-XDC | Nethermind-XDC | Reth-XDC |
|---------|---------------------|-----|------------|----------------|----------|
| **Language** | Go | Go | Go | C# | Rust |
| **Sync Speed** | ~180 blk/min | **5,100 blk/min** ⚡ | ~500 blk/min | ~86 blk/s | Pipeline |
| **State Scheme** | Hash only | **Hash + Path (PBSS)** | MDBX | Hash | MDBX |
| **Disk Usage** | High (~2TB) | Moderate | **Low (~500GB)** | Moderate | **Lowest** |
| **Memory** | 8-16GB | Up to 32GB | **2-4GB** | 8-16GB | **2-4GB** |
| **P2P Protocol** | eth/62, 63, 100 | eth/62, 63, 100 | eth/62, 63 | eth/62, 63, 100 | eth/100 (WIP) |
| **Consensus** | XDPoS v1+v2 | XDPoS v1+v2 | XDPoS v1+v2 | XDPoS v1+v2 | XDPoS v1 (WIP) |
| **Snap/Fast Sync** | ❌ | ❌ (full only) | ✅ Stage-based | ❌ | ✅ Pipeline |
| **Pruning** | ❌ | ✅ (PBSS) | ✅ (native) | ✅ | ✅ (native) |
| **SkyNet Monitoring** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Auto-heal** | ❌ | ✅ (SkyOne) | ✅ (SkyOne) | ✅ (SkyOne) | ✅ (SkyOne) |
| **Cross-client Validation** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Production Ready** | ✅ Stable | 🟡 Syncing | 🟡 7.4M blocks | 🟡 300K blocks | 🔴 ECIES blocked |

## 🛡️ Why Multi-Client Matters

| Risk | Single Client | Multi-Client |
|------|--------------|--------------|
| **Consensus bug** | 🔴 100% network affected | 🟢 Only 25% affected |
| **Zero-day exploit** | 🔴 Entire network vulnerable | 🟢 Diverse attack surface |
| **Performance issue** | 🔴 No alternative | 🟢 Switch to faster client |
| **State corruption** | 🔴 No cross-validation | 🟢 Compare across 4 clients |
| **Upgrade rollout** | 🔴 Big bang, all at once | 🟢 Canary deploy, one at a time |

> *Ethereum's multi-client approach prevented catastrophic failures during The Merge. XDC India brings the same resilience to XDC Network.*

---

## 📊 Live Dashboards

| Dashboard | URL | Description |
|-----------|-----|-------------|
| SkyNet | [skynet.xdcindia.com](https://skynet.xdcindia.com) | Fleet health + sync progress |
| Ethstats | [stats.xdcindia.com](https://stats.xdcindia.com) | Real-time block propagation |
| SkyNet API | [api.xdcindia.com](https://api.xdcindia.com) | REST API for node data |

## 👨‍💻 Team

Built by **dAI Team**

---

<p align="center">
  <a href="https://xdcindia.com">xdcindia.com</a> •
  <a href="https://t.me/AnilChinchawale">Telegram</a> •
  <a href="https://github.com/XDCIndia">GitHub</a>
</p>
