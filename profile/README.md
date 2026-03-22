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
┌──────────────────────────────────────────────────────┐
│                    XDC Network                        │
│                  (XDPoS Consensus)                    │
├──────────────────────────────────────────────────────┤
│                                                      │
│              ┌─────────────────┐                     │
│              │  XDC v2.6.8     │  ← Single client    │
│              │  (geth fork)    │    for ALL nodes     │
│              └────────┬────────┘                     │
│                       │                              │
│              ┌────────┴────────┐                     │
│              │  eth/62 + eth/63│  ← Legacy P2P only  │
│              │  + eth/100 (v2) │                     │
│              └────────┬────────┘                     │
│                       │                              │
│    ┌─────────┬────────┼────────┬──────────┐         │
│    │ Node 1  │ Node 2 │ Node 3 │ Node N   │         │
│    │ v2.6.8  │ v2.6.8 │ v2.6.8 │ v2.6.8   │         │
│    └─────────┴────────┴────────┴──────────┘         │
│                                                      │
│    Monitoring: ❌ Basic ethstats only                 │
│    Alerting:   ❌ None                               │
│    Auto-heal:  ❌ Manual restarts                    │
│    Diversity:  ❌ Single client = single point of    │
│                   failure (bug takes down ALL nodes)  │
└──────────────────────────────────────────────────────┘
```

**Risks:**
- 🔴 Single client bug → entire network affected
- 🔴 No monitoring beyond basic ethstats
- 🔴 No auto-recovery from crashes/stalls
- 🔴 No cross-client validation

---

## 🚀 Future-Ready Architecture (Multi-Client + SkyNet)

> What XDC India is building — 4 clients, full observability, self-healing

```
┌──────────────────────────────────────────────────────────────────────┐
│                         XDC Network                                   │
│                     (XDPoS v1 + v2 Consensus)                        │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  ┌──────────┐           │
│  │   GP5    │  │  Erigon  │  │Nethermind │  │   Reth   │           │
│  │  (Go)    │  │  (Go)    │  │   (C#)    │  │  (Rust)  │           │
│  │ 28x fast │  │ eth/62+63│  │ StateRoot │  │ Pipeline │           │
│  │ HBSS+PBSS│  │  MDBX    │  │  Bypass   │  │  Sync    │           │
│  └────┬─────┘  └────┬─────┘  └────┬──────┘  └────┬─────┘           │
│       │              │             │              │                  │
│  ┌────┴──────────────┴─────────────┴──────────────┴─────┐           │
│  │              Unified P2P Layer                        │           │
│  │      eth/62 + eth/63 + eth/100 (XDPoS v2)           │           │
│  │      135 mainnet + 28 apothem official bootnodes     │           │
│  │      Cross-node fleet peering (6 trusted nodes)      │           │
│  └──────────────────────┬───────────────────────────────┘           │
│                         │                                            │
├─────────────────────────┴────────────────────────────────────────────┤
│                                                                      │
│  ┌─────────────── SkyNet (Network Brain) ───────────────────┐       │
│  │                                                           │       │
│  │  ┌──────────────┐  ┌──────────────┐  ┌───────────────┐  │       │
│  │  │   Dashboard  │  │   REST API   │  │   Alerting    │  │       │
│  │  │  skynet.     │  │  api.        │  │  Telegram +   │  │       │
│  │  │  xdcindia.com│  │  xdcindia.com│  │  Email        │  │       │
│  │  └──────────────┘  └──────────────┘  └───────────────┘  │       │
│  │                                                           │       │
│  │  ┌──────────────┐  ┌──────────────┐  ┌───────────────┐  │       │
│  │  │ Fleet Health │  │  Sync        │  │  Cross-Client │  │       │
│  │  │ Monitoring   │  │  Progress    │  │  Validation   │  │       │
│  │  │ CPU/Mem/Disk │  │  ETA/Rate    │  │  Block Match  │  │       │
│  │  └──────────────┘  └──────────────┘  └───────────────┘  │       │
│  └───────────────────────────────────────────────────────────┘       │
│                                                                      │
│  ┌─────────────── SkyOne (Node Agent) ──────────────────────┐       │
│  │                                                           │       │
│  │  Runs on EVERY node (Docker sidecar)                     │       │
│  │                                                           │       │
│  │  ✅ Heartbeat every 60s → SkyNet API                     │       │
│  │  ✅ Auto-heal: restart crashed containers                │       │
│  │  ✅ Sync stall detection + peer re-injection             │       │
│  │  ✅ Storage/IOPS monitoring                              │       │
│  │  ✅ Client-agnostic (works with GP5/Erigon/NM/Reth)     │       │
│  │  ✅ Registered on SkyNet with unique nodeId              │       │
│  └───────────────────────────────────────────────────────────┘       │
│                                                                      │
│  ┌─────────────── Ethstats (Live View) ─────────────────────┐       │
│  │  stats.xdcindia.com — Real-time block propagation        │       │
│  │  All clients report: GP5, Erigon, Nethermind, Reth       │       │
│  └───────────────────────────────────────────────────────────┘       │
│                                                                      │
├──────────────────────────────────────────────────────────────────────┤
│                         Fleet (7 Servers)                             │
│                                                                      │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐            │
│  │  test  │ │ xdc01  │ │ xdc02  │ │ xdc03  │ │  prod  │            │
│  │ GP5×2  │ │ GP5+Er │ │ GP5+Er │ │ GP5    │ │GP5+Er+v│            │
│  │ 168    │ │  125   │ │  109   │ │  113   │ │  213   │            │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────┘            │
│  ┌────────┐ ┌────────┐                                              │
│  │  apo   │ │ xdc07  │  14 GP5 + 3 Erigon + 1 NM + 1 Reth         │
│  │ GP5×2  │ │ GP5    │  = 19 nodes total                           │
│  │  183   │ │  71.4  │                                              │
│  └────────┘ └────────┘                                              │
│                                                                      │
│  Networks: Mainnet (Chain 50) + Apothem Testnet (Chain 51)          │
│  Schemes:  HBSS (Hash) + PBSS (Path) for state diversity            │
└──────────────────────────────────────────────────────────────────────┘
```

**Benefits:**
- 🟢 **Client diversity** — Bug in one client? 3 others keep running
- 🟢 **Cross-client validation** — Compare block hashes across GP5/Erigon/NM/Reth
- 🟢 **Self-healing** — SkyOne auto-restarts crashed nodes, re-injects peers
- 🟢 **Full observability** — SkyNet dashboard, API, alerts, sync tracking
- 🟢 **Fleet management** — 7 servers, 19 nodes, both networks, both state schemes
- 🟢 **Enterprise tooling** — One-command deployment via `xdc` CLI
- 🟢 **28x faster sync** — GP5 optimizations (batch size, multi-peer, reduced delay)

---

## 📊 Live Dashboards

| Dashboard | URL | Description |
|-----------|-----|-------------|
| SkyNet | [skynet.xdcindia.com](https://skynet.xdcindia.com) | Fleet health + sync progress |
| Ethstats | [stats.xdcindia.com](https://stats.xdcindia.com) | Real-time block propagation |
| SkyNet API | [api.xdcindia.com](https://api.xdcindia.com) | REST API for node data |

## 👨‍💻 Team

Built by **[Anil Chinchawale](https://github.com/AnilChinchawale)** and contributors.

---

<p align="center">
  <a href="https://xdcindia.com">xdcindia.com</a> •
  <a href="https://t.me/AnilChinchawale">Telegram</a> •
  <a href="https://github.com/XDCIndia">GitHub</a>
</p>
