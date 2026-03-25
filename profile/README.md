<p align="center">
  <img src="https://raw.githubusercontent.com/XDCIndia/.github/main/profile/xdc-india-logo.png" width="120" alt="XDC Innovation Labs">
</p>

<h1 align="center">XDC Innovation Labs</h1>

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

## 📊 At a Glance: Why Upgrade from v2.6.8?

| What You Care About | v2.6.8 (Now) | Best Alternative | Your Gain |
|:--------------------|:-------------|:-----------------|:----------|
| **💾 Disk Space** | ~2 TB archive | **Reth: ~700 GB** | **65% smaller** — Save $50-100/mo |
| **⚡ Sync Speed** | ~3 blocks/sec | **GP5: 85 blocks/sec** | **28x faster** — Hours not weeks |
| **🚀 RPC Speed** | ~50 ms response | **Reth: ~3 ms** | **17x faster** — Snappy dApps |
| **💰 Server Costs** | 1-2 nodes/server | **Reth: 10-12 nodes** | **6-10x density** — Same hardware, more capacity |
| **🛡️ Security** | Single Go runtime | **4 different runtimes** | **CVE isolation** — 75% blast radius reduction |
| **🔧 Maintenance** | Manual restarts | **SkyNet auto-heal** | **Self-healing fleet** |

### Quick Picks

| If You Want... | Choose | Because |
|:---------------|:-------|:--------|
| Fastest upgrade, same codebase | **GP5** | 28x sync, drop-in replacement |
| Cheapest archive node | **Reth** | 65% less disk, lowest RAM |
| Best RPC performance | **Erigon** | 10x throughput, no stalls |
| Enterprise .NET stack | **Nethermind** | JIT EVM, native APM tooling |

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

> What XDC Innovation Labs is building — 4 clients, full observability, self-healing

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

## Architecture Comparison

> XDC 2.6.8 is a fork of Go-Ethereum 1.8.3 (2017). The table below compares fundamental design characteristics against the current generation of Ethereum-compatible clients — independent of XDPoS porting status.

| Metric | XDC 2.6.8 (Geth 1.8.3) | GP5 (Geth 1.14) | Erigon v3 | Nethermind | Hyperledger Besu | Reth |
|--------|------------------------|-----------------|-----------|------------|-----------------|------|
| **Base / Year** | Geth 1.8.3, 2017 | Geth 1.14, 2024 | Custom, 2024 | .NET 8, 2024 | Java 21, 2024 | Rust, 2024 |
| **Database Engine** | LevelDB (LSM-tree) | LevelDB + PebbleDB | MDBX (B+ tree, zero-copy) | RocksDB (LSM-tree) | RocksDB (Bonsai tries) | MDBX (B+ tree, zero-copy) |
| **Read Amplification** | High — LSM compaction 10-30x | Moderate — Pebble optimized | Low — single B+ tree lookup | Moderate — bloom filters | Moderate | Low — single B+ tree lookup |
| **Write Amplification** | High — 10-30x | Moderate | Low — 1-3x | Moderate | Moderate | Low — 1-3x |
| **DB Compaction Stalls** | Frequent (LSM background compaction) | Frequent | None — B+ tree, no compaction | Rare (tuned bloom filters) | Rare | None — B+ tree, no compaction |
| **State Storage Model** | Hash-based trie only | Hash trie + Path-based (PBSS) | Flat key-value + history index | Patricia trie (RocksDB) | Bonsai Tries (layered) | Flat key-value + history index |
| **Archive Disk (ETH equiv.)** | ~12 TB est. | ~10 TB | ~2.5 TB | ~4 TB | ~8 TB | ~3 TB |
| **State Pruning** | None — full archive only | Online via PBSS (no downtime) | Online, continuous | Online, automatic | Online (Bonsai) | Online, automatic |
| **Historical State Access** | Full trie traversal per query | Full trie traversal | Direct flat lookup — ms | Direct lookup | Bonsai layered lookup | Direct flat lookup — ms |
| **Reorg Handling** | Full trie revert — seconds | Full trie revert | History index lookup — ms | Moderate | Moderate | History index lookup — ms |
| **Memory Model** | In-process GC | In-process GC | Memory-mapped I/O (mmap) | Managed .NET GC (JIT) | JVM GC (G1/ZGC) | Zero-copy MDBX — no GC |
| **Peak RAM** | 8–16 GB | 8–16 GB | 2–8 GB | 4–8 GB | 4–8 GB | 2–6 GB |
| **GC Pause** | 10–50 ms (Go GC) | 10–50 ms | 10–50 ms (Go GC) | 5–20 ms (.NET GC) | 5–15 ms (JVM ZGC) | 0 ms — Rust, no GC |
| **Cold Start Time** | ~30s | ~15s | ~5s (mmap + OS page cache) | ~20s | ~25s | ~3s (mmap + OS page cache) |
| **Sync Architecture** | Full sync only | Full + Snap sync | 8-stage pipeline | Full + Fast + Snap | Full + Fast + Snap | 13-stage pipeline |
| **Block Import Speed** | ~3 blk/s | ~85 blk/s (28x) | ~76 blk/s (25x) | ~68 blk/s (22x) | ~50 blk/s (17x) | Est. pipeline — fastest |
| **Snap Sync** | No | Yes | Yes | Yes | Yes | Yes |
| **P2P Protocol** | eth/63 only | eth/68 | eth/68 | eth/68 | eth/68 | eth/68 |
| **Network Bandwidth** | No compression | Snappy compressed | Snappy compressed | Snappy compressed | Snappy compressed | Snappy compressed |
| **EVM Implementation** | Go interpreter | Go interpreter | Go interpreter + parallel exec | JIT-compiled (RyuJIT) | JVM JIT | Native compiled (revm, Rust) |
| **Parallel EVM Execution** | No | No | Yes (exec3) | Partial (.NET TPL) | No | Roadmap |
| **Transaction Execution** | Sequential | Sequential | Parallel (exec3) | Parallel (.NET TPL) | Sequential | Parallel (Rayon) |
| **RPC Latency (eth_call)** | ~50 ms avg | ~30 ms avg | ~5 ms avg | ~20 ms avg | ~15 ms avg | ~3 ms avg |
| **Concurrent RPC Capacity** | Low — GC pressure, single writer | Low — GC pressure | High — staged reads, mmap | High — .NET async | High — Vertx async | Highest — Tokio + zero-copy |
| **RPC Nodes per Server** | 1–2 per server | 1–2 per server | 8–10 per server | 3–4 per server | 3–4 per server | 10–12 per server |
| **JSON-RPC Coverage** | Partial subset | Full + debug | Full + trace | Full + trace | Full + trace | Full + trace |
| **EIP Baseline** | ~EIP-161 (2017) | EIP-4844 | EIP-4844 | EIP-4844 | EIP-4844 | EIP-4844 |
| **Language Safety** | Go — GC, race detector | Go — GC, race detector | Go — GC, race detector | C# — GC + JIT + null safety | Java — GC + null safety | Rust — compile-time memory safety, no CVE class |
| **Concurrency Model** | Goroutines | Goroutines | Goroutines + staged pipeline | Task-based async (.NET TPL) | Vertx event loop | Tokio async + Rayon |
| **Security Audits** | None on record | Partial | Partial | Independent | Independent (Consensys) | Independent |
| **Enterprise Support** | No | No | No | Partial | Yes — Consensys backed | No |
| **Runtime CVE Surface** | Go runtime only | Go runtime only | Go runtime only | .NET runtime (separate CVE set) | JVM runtime (separate CVE set) | Rust runtime (separate CVE set) |
| **Supply Chain** | Single compiler (gc) | Single compiler (gc) | Single compiler (gc) | .NET SDK + NuGet | JDK + Maven | rustc + cargo |

---

| **Fastest RPC** | Erigon, Reth | Flat DB: Erigon ~5ms avg, Reth ~3ms avg vs v2.6.8 ~50ms (trie traversal + LevelDB read amplification) |
| **10x RPC density** | Erigon, Reth | Low RAM (2-6 GB) means 8-12 RPC nodes per server vs 1-2 with v2.6.8 — same hardware, 10x capacity |
| **Instant reorg recovery** | Erigon, Reth | History stored as indexed deltas — reorg is a lookup, not a full trie recompute (seconds → milliseconds) |
| **Best historical queries** | Erigon, Reth | Temporal history stored natively in separate tables — no archive node or replay needed |
| **Different bug classes** | NM (C#), Reth (Rust) | A Go runtime exploit (CVE in gc runtime) cannot affect .NET or Rust clients simultaneously |
| **Defense in depth** | NM + Reth | Three separate compilers (gc, .NET SDK, rustc) + three package ecosystems = supply chain attack surface split three ways |
| **Easiest upstream rebase** | GP5 | Same Go/geth codebase as v2.6.8 — minimal merge conflicts, fastest to carry XDPoS patches forward |

---

## 🔄 Why Switch? (v2.6.8 → New Client)

> What operators gain by running each alternative client

### → GP5 (Immediate upgrade, same codebase)
- **28x faster sync** — resync from scratch in hours instead of weeks
- **PBSS state** — online pruning without stopping the node; no more ever-growing disk
- **Snap sync** — new validators join the network in minutes, not days
- **Snappy compression** — 20-30% less bandwidth on a busy peer

### → Erigon-XDC (Best for archive / RPC operators)
- **60% less disk** — full archive node at ~800 GB vs ~2 TB; saves $50-100/month on NVMe cloud storage
- **10x RPC throughput** — flat B+ tree lookups at ~5ms vs ~50ms trie+LevelDB traversal
- **No compaction stalls** — LevelDB/RocksDB compaction can pause I/O for minutes; MDBX never does
- **Run 8-10 RPC nodes per server** — 2-8 GB RAM per instance instead of 8-16 GB
- **Instant reorgs** — history index means chain reorgs complete in milliseconds

### → Nethermind-XDC (Best for .NET/enterprise environments)
- **JIT-compiled EVM** — RyuJIT-optimized execution of smart contracts, measurable throughput gains on heavy blocks
- **Lower GC latency** — .NET GC pauses 5-20ms vs Go's 10-50ms; more consistent block times
- **Independent CVE surface** — .NET runtime vulnerabilities are separate from Go runtime CVEs
- **Parallel transaction processing** — TPL task scheduler distributes EVM workload across all cores
- **Enterprise ecosystem** — .NET tooling, profilers, APM agents (Datadog, New Relic) work natively

### → Reth-XDC (Best for high-load RPC / validator infrastructure)
- **Zero GC pauses** — Rust ownership model eliminates runtime garbage collection entirely; no missed blocks under load
- **~700 GB archive** — smallest footprint of any client; Rust + MDBX flat storage
- **~3ms RPC latency** — zero-copy MDBX reads + Tokio async = lowest latency at highest concurrency
- **12+ RPC nodes per server** — 2-6 GB RAM, lowest of all clients
- **Memory safety by construction** — compile-time borrow checker prevents buffer overflows, use-after-free, data races — entire classes of CVEs structurally impossible

---

## 🛡️ Why Multi-Client Matters

| Risk | Single Client | Multi-Client |
|------|--------------|--------------|
| **Consensus bug** | 🔴 100% network affected | 🟢 Only 25% affected |
| **Zero-day exploit** | 🔴 Entire network vulnerable | 🟢 Diverse attack surface |
| **Performance issue** | 🔴 No alternative | 🟢 Switch to faster client |
| **State corruption** | 🔴 No cross-validation | 🟢 Compare across 4 clients |
| **Upgrade rollout** | 🔴 Big bang, all at once | 🟢 Canary deploy, one at a time |
| **Supply chain attack** | 🔴 Single package ecosystem | 🟢 3 compilers, 3 ecosystems |
| **Runtime CVE** | 🔴 All nodes on same Go runtime | 🟢 Go + .NET + Rust runtimes |

> *Ethereum's multi-client approach prevented catastrophic failures during The Merge. XDC Innovation Labs brings the same resilience to XDC Network.*

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
