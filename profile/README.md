# 🇮🇳 XDC India

**Multi-client blockchain infrastructure for [XDC Network](https://xdc.org)**

Building client diversity and enterprise-grade tooling for the XDC ecosystem.

---

## 🔧 What We Build

### Blockchain Clients
| Client | Language | Status | Description |
|--------|----------|--------|-------------|
| **[GP5](https://github.com/XDCIndia/go-ethereum)** | Go | 🟢 Active | Next-gen geth fork with XDPoS v1+v2 consensus |
| **[Erigon-XDC](https://github.com/XDCIndia/erigon-xdc)** | Go | 🟢 Active | High-performance Erigon fork for XDC |
| **[Nethermind-XDC](https://github.com/XDCIndia/xdc-nethermind-private)** | C# | 🟢 Active | .NET client with XDPoS consensus |
| **[Reth-XDC](https://github.com/XDCIndia/reth)** | Rust | 🟡 In Progress | Reth fork — fastest execution layer |

### Infrastructure
| Project | Description |
|---------|-------------|
| **[XDC Node Setup](https://github.com/XDCIndia/xdc-node-setup)** | Enterprise-grade node deployment toolkit with CLI |
| **[SkyNet](https://skynet.xdcindia.com)** | Network monitoring dashboard + API |
| **[Ethstats](https://stats.xdcindia.com)** | Real-time node statistics |

---

## 🌐 Network Coverage

- **XDC Mainnet** (Chain 50) — 7+ nodes across 7 servers
- **XDC Apothem Testnet** (Chain 51) — Full coverage
- **Multi-client sync** — GP5, Erigon, Nethermind running in parallel

## 📊 Live Dashboards

| Dashboard | URL |
|-----------|-----|
| SkyNet | [skynet.xdcindia.com](https://skynet.xdcindia.com) |
| Ethstats | [stats.xdcindia.com](https://stats.xdcindia.com) |
| SkyNet API | [api.xdcindia.com](https://api.xdcindia.com) |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│              XDC Network (Layer 1)           │
├──────────┬──────────┬──────────┬────────────┤
│   GP5    │  Erigon  │Nethermind│   Reth     │
│  (Go)    │  (Go)    │  (C#)   │  (Rust)    │
├──────────┴──────────┴──────────┴────────────┤
│         XDPoS v1 + v2 Consensus              │
├─────────────────────────────────────────────┤
│    SkyNet Monitoring  │  Ethstats  │  CLI    │
└─────────────────────────────────────────────┘
```

## 🤝 Team

Built by **[Anil Chinchawale](https://github.com/AnilChinchawale)** and contributors.

## 📫 Contact

- Website: [xdcindia.com](https://xdcindia.com)
- GitHub: [@XDCIndia](https://github.com/XDCIndia)
- Telegram: [@AnilChinchawale](https://t.me/AnilChinchawale)
