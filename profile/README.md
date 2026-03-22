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
| **SkyNet** | Network monitoring dashboard — 7 servers, 14+ nodes |
| **Ethstats** | Real-time block propagation and peer statistics |

## 🌐 Network

- **Mainnet** (Chain 50) — 7+ GP5 nodes syncing across 7 servers
- **Apothem** (Chain 51) — Full testnet coverage
- **4 clients** running in parallel for client diversity

## 📊 Architecture

```
┌──────────────────────────────────────────────┐
│              XDC Network (Layer 1)            │
├──────────┬──────────┬───────────┬────────────┤
│   GP5    │  Erigon  │ Nethermind│    Reth    │
│  (Go)    │  (Go)    │   (C#)   │   (Rust)   │
├──────────┴──────────┴───────────┴────────────┤
│          XDPoS v1 + v2 Consensus              │
├──────────────────────────────────────────────┤
│   SkyNet Monitoring  │  Ethstats  │   CLI     │
└──────────────────────────────────────────────┘
```

## 👨‍💻 Team

Built by **[Anil Chinchawale](https://github.com/AnilChinchawale)**

---

<p align="center">
  <a href="https://xdcindia.com">xdcindia.com</a> •
  <a href="https://t.me/AnilChinchawale">Telegram</a> •
  <a href="https://github.com/XDCIndia">GitHub</a>
</p>
