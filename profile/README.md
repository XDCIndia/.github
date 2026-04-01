# XDCIndia — Multi-Client XDC Network Infrastructure

> Running the most diverse node fleet on XDC Network: **4 clients, 5 servers, 1 chain**.

---

## 🔬 Post-Quantum Cryptography Leadership

**XDC is one of the few L1 blockchains with working Falcon signature code.**

We have implemented and demonstrated [NIST FIPS 206 Falcon-512/1024](https://csrc.nist.gov/pubs/fips/206/final) post-quantum signatures integrated with XDC's XDPoS consensus — replacing ECDSA with lattice-based cryptography that is resistant to quantum computer attacks.

| Resource | Link |
|---|---|
| 🌐 Quantum Overview Page | [xdc.network/quantum.html](https://xdc.network/quantum.html) |
| 🌿 Proof-of-Concept Branch | [poc_falcon branch (go-XDC)](https://github.com/XDCIndia/go-XDC/tree/poc_falcon) |
| 📄 NIST FIPS 206 Standard | [Falcon Algorithm](https://csrc.nist.gov/pubs/fips/206/final) |

### Research Credits
- **Ritesh Kakkad** — Initial Falcon integration research & implementation (March 2024)
- **Gary** — Extended research, XDPoS v2 compatibility analysis (August 2025)

---

## 🌐 Multi-Client Node Fleet

XDCIndia operates **4 independent XDC clients** all syncing mainnet simultaneously — enabling true client diversity and reducing single-implementation risk.

| Client | Technology | Status | Latest Block |
|---|---|---|---|
| **GP5 (XDC-Geth)** | Go-Ethereum fork | ✅ Active | ~12.5M |
| **Erigon-XDC** | Erigon v3 port | ✅ Active | ~12.2M |
| **Nethermind-XDC** | .NET Nethermind port | ✅ Active | ~12.5M |
| **Reth-XDC** | Rust Reth port | 🔄 Syncing | ~12.5M |

Live node metrics: [net.xdc.network](https://net.xdc.network)

---

## 📦 Snapshot Downloads

Fast-sync your XDC node with pre-built snapshots — skip months of sync time.

| Client | Snapshot | Size |
|---|---|---|
| GP5 (Geth) | [gp5-mainnet-12220900.tar.gz](https://xdc.network/snapshots/gp5-mainnet-12220900.tar.gz) | 9.1 GB |
| Erigon | [erigon-mainnet-11194447.tar.gz](https://xdc.network/snapshots/erigon-mainnet-11194447.tar.gz) | 12 GB |
| Nethermind | [nm-mainnet-12194099.tar.gz](https://xdc.network/snapshots/nm-mainnet-12194099.tar.gz) | 9.0 GB |
| Reth | [reth-mainnet-12220900.tar.gz](https://xdc.network/snapshots/reth-mainnet-12220900.tar.gz) | 19 GB |

📥 All snapshots: [xdc.network/snapshots/](https://xdc.network/snapshots/)

---

## 🗂️ Key Repositories

| Repo | Description |
|---|---|
| [erigon-xdc](https://github.com/XDCIndia/erigon-xdc) | Erigon v3 port with XDPoS consensus |
| [xdcindia-website](https://github.com/XDCIndia/xdcindia-website) | XDCIndia.com website |
| [go-XDC](https://github.com/XDCIndia/go-XDC) | GP5 fork with XDPoS v1/v2 + Falcon PoC |
| XDCStats-private | Internal node monitoring dashboard |
| xdc-nethermind-private | Nethermind XDPoS port (internal) |
| reth-xdc | Rust Reth XDPoS port |

---

## 🌍 Why Multi-Client Matters

Running 4 independent implementations of the same blockchain protocol is one of the strongest guarantees of correctness and resilience in distributed systems.

- **No single point of failure** — if one client has a bug, 3 others keep the chain alive
- **Consensus validation** — agreement across Geth, Erigon, Nethermind, and Reth proves block validity
- **Client diversity** — the gold standard in Ethereum post-Merge; XDC achieves it today
- **Quantum readiness** — migration is safer when multiple codebases can be upgraded independently

---

<sub>XDCIndia · Building client diversity for XDC Network · [xdcindia.com](https://xdcindia.com)</sub>
