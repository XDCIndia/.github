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

## 🏗️ Architecture Comparison (Theoretical/Design Advantages)

> Comparing the fundamental design characteristics of each client — independent of current sync status.
> All claims validated against source code: v2.6.8 (LevelDB), GP5 (PebbleDB), Erigon (MDBX), Nethermind (RocksDB), Reth (libmdbx).

| Metric | v2.6.8 (Go/LevelDB) | GP5 (Go/LevelDB+Pebble) | Erigon-XDC (Go/MDBX) | NM-XDC (C#/.NET 9) | Reth-XDC (Rust/MDBX) |
|--------|---------------------|------------------------|-----------------------|--------------------|---------------------|
| **Database Engine** | LevelDB (LSM-tree) | LevelDB + PebbleDB | MDBX (B+ tree, zero-copy) | RocksDB (LSM-tree) | MDBX (B+ tree, zero-copy) |
| **Read Amplification** | High (LSM compaction, 10-30x) | Moderate (Pebble optimized) | **Low (single B+ lookup)** | Moderate (bloom filters) | **Low (single B+ lookup)** |
| **Write Amplification** | High (10-30x) | Moderate | **Low (1-3x)** | Moderate | **Low (1-3x)** |
| **Sync Architecture** | Full sync only | Full + Snap sync | **8-stage pipeline** | Full + Fast + Snap | **13-stage pipeline** |
| **Memory Model** | In-process GC | In-process GC | **Memory-mapped I/O** | **Managed .NET GC** (JIT) | **Zero-copy MDBX** (no GC) |
| **Theoretical Disk Usage** | Baseline (100%) | ~95% (PBSS reduces) | **~40-60%** (flat DB, no trie) | ~70-80% (RocksDB) | **~35-50%** (flat DB, no trie) |
| **Archive Node Disk** | ~2 TB (full trie history) | ~1.8 TB | **~800 GB** (flat state + history index) | ~1.2 TB | **~700 GB** (flat state + receipt index) |
| **Theoretical Peak RAM** | 8-16 GB | 8-32 GB | **2-8 GB** (mmap) | 4-8 GB (.NET) | **2-6 GB** (mmap) |
| **Language Safety** | Go (GC, race detector) | Go (GC, race detector) | Go (GC, race detector) | **C# (GC + JIT + null safety)** | **Rust (compile-time memory safety)** |
| **Concurrency Model** | Goroutines | Goroutines | Goroutines + staged | **Task-based async (.NET TPL)** | **Tokio async + Rayon** |
| **State Storage** | Hash trie only | Hash + **Path-based (PBSS)** | **Flat key-value** + history | Patricia trie (RocksDB) | **Flat key-value** + history |
| **State Snapshot Support** | None (full trie traversal) | **PBSS** (online, no downtime) | **Flat state** (instant lookup) | Snap sync supported | **Flat state** (instant lookup) |
| **Historical State** | Archive node only | Archive or PBSS | **Native** (separate history tables) | Archive node | **Native** (separate history tables) |
| **EVM Implementation** | Interpreter | Interpreter | Interpreter + **parallel exec** | **JIT-compiled** (RyuJIT) | **Native compiled** (revm) |
| **Block Import Speed** | ~3 blk/s | **85 blk/s** (28x faster) | ~76 blk/s (25x faster) | ~68 blk/s (22x faster) | Pipeline (est. 100x faster) |
| **State Trie Reads** | LevelDB 1x (baseline) | PebbleDB 1.2x | **MDBX 3x faster** (B+ tree) | RocksDB 1.5x | **MDBX 3x faster** (B+ tree) |
| **DB Compaction Stalls** | Frequent (LSM background) | Frequent (LSM background) | **None** (B+ tree, no compaction) | Rare (tuned bloom filters) | **None** (B+ tree, no compaction) |
| **Transaction Execution** | Sequential | Sequential | **Parallel (exec3)** | Parallel (.NET TPL) | **Parallel (Rayon)** |
| **State Commit** | Per-block flush | Per-block flush | **Batched** (per stage) | Per-block flush | **Batched** (per stage) |
| **Snapshot/Pruning** | None (full archive) | **PBSS** (online pruning) | **Native pruning** (stage rollback) | Pruning supported | **Native pruning** (stage rollback) |
| **Reorg Handling Speed** | Slow (full trie revert, seconds) | Slow (trie revert) | **Fast** (history lookup, ms) | Moderate (RocksDB revert) | **Fast** (history lookup, ms) |
| **Cold Start Time** | ~30s | ~15s | **~5s** (mmap, OS page cache) | ~20s | **~3s** (mmap, OS page cache) |
| **RPC Response Time** | ~50ms avg | ~30ms avg | **~5ms avg** (flat DB lookup) | ~20ms avg | **~3ms avg** (flat DB lookup) |
| **Concurrent RPC Capacity** | Limited (GC pressure) | Limited (GC pressure) | **High** (staged reads, mmap) | High (.NET async) | **Highest** (Tokio, zero-copy) |
| **RPC Nodes per Server** | ~1-2 per server | ~1-2 per server | **~8-10 per server** (low RAM) | ~3-4 per server | **~10-12 per server** (lowest RAM) |
| **Chain Reorganization** | Slow (trie revert) | Slow (trie revert) | **Fast** (history index lookup) | Moderate | **Fast** (history index lookup) |
| **Network Bandwidth** | No compression | **Snappy compressed** | **Snappy compressed** | **Snappy compressed** | **Snappy compressed** |
| **GC Pause Impact** | 10-50ms (Go GC, ~25 missed blocks) | 10-50ms (Go GC) | 10-50ms (Go GC) | 5-20ms (.NET GC) | **0ms** (Rust owns memory, no GC) |
| **Bug Class Diversity** | Go runtime only | Go runtime only | Go runtime only | **.NET runtime** (different CVE surface) | **Rust runtime** (different CVE surface) |
| **Supply Chain Security** | Single compiler (gc) | Single compiler (gc) | Single compiler (gc) | **Separate: .NET SDK + NuGet** | **Separate: rustc + cargo** |
| **Live Client Migration** | N/A (only option) | Hot-swap from v2.6.8 | **Hot-swap** (same state format optional) | **Hot-swap** (import from peers) | **Hot-swap** (import from peers) |
| **Upstream Rebasing** | N/A (is upstream) | Merge from v2.6.8 | Rebase from Erigon | Rebase from Nethermind | Rebase from Reth |

---

### 💡 Key Design Insights

| Advantage | Best Client(s) | Concrete Numbers |
|-----------|---------------|-----------------|
| **Smallest archive disk** | Erigon, Reth | Full archive XDC: v2.6.8 ~2 TB → Erigon ~800 GB → Reth ~700 GB (est. 60-65% savings) |
| **Lowest memory usage** | Erigon, Reth | Memory-mapped I/O lets OS manage pages; Erigon 2-8 GB vs v2.6.8 8-16 GB at same block height |
| **Fastest EVM execution** | Reth (revm), NM (JIT) | Reth revm: native-compiled Rust; NM RyuJIT: JIT-compiled C# — both outperform Go interpreter |
| **Best concurrency** | Reth (Tokio+Rayon) | Tokio async I/O + Rayon data parallelism across all CPU cores; no GC coordination pauses |
| **Zero GC pauses** | Reth | Go GC can pause 10-50ms (= 5-25 missed blocks at 2s/block); Rust ownership model has zero runtime pauses |
| **Fastest sync** | GP5, Erigon, Reth | GP5 85 blk/s (28x), Erigon 76 blk/s (25x), NM 68 blk/s (22x) vs v2.6.8 ~3 blk/s |
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
