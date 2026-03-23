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

| Metric | v2.6.8 (Go/LevelDB) | GP5 (Go/LevelDB+Pebble) | Erigon-XDC (Go/MDBX) | NM-XDC (C#/.NET 9) | Reth-XDC (Rust/MDBX) |
|--------|---------------------|------------------------|-----------------------|--------------------|---------------------|
| **Database Engine** | LevelDB (LSM-tree) | LevelDB + PebbleDB | MDBX (B+ tree, zero-copy) | RocksDB (LSM-tree) | MDBX (B+ tree, zero-copy) |
| **Read Amplification** | High (LSM compaction) | Moderate (Pebble optimized) | **Low (single B+ lookup)** | Moderate (bloom filters) | **Low (single B+ lookup)** |
| **Write Amplification** | High (10-30x) | Moderate | **Low (1-3x)** | Moderate | **Low (1-3x)** |
| **Sync Architecture** | Full sync only | Full + Snap sync | **8-stage pipeline** | Full + Fast + Snap | **13-stage pipeline** |
| **Memory Model** | In-process GC | In-process GC | **Memory-mapped I/O** | **Managed .NET GC** (JIT) | **Zero-copy MDBX** (no GC) |
| **Theoretical Disk Usage** | Baseline (100%) | ~95% (PBSS reduces) | **~40-60%** (flat DB) | ~70-80% (RocksDB) | **~35-50%** (flat DB) |
| **Theoretical Peak RAM** | 8-16 GB | 8-32 GB | **2-8 GB** (mmap) | 4-8 GB (.NET) | **2-6 GB** (mmap) |
| **Language Safety** | Go (GC, race detector) | Go (GC, race detector) | Go (GC, race detector) | **C# (GC + JIT + null safety)** | **Rust (compile-time memory safety)** |
| **Concurrency Model** | Goroutines | Goroutines | Goroutines + staged | **Task-based async (.NET TPL)** | **Tokio async + Rayon** |
| **State Storage** | Hash trie only | Hash + **Path-based (PBSS)** | **Flat key-value** + history | Patricia trie (RocksDB) | **Flat key-value** + history |
| **Historical State** | Archive node only | Archive or PBSS | **Native** (separate history) | Archive node | **Native** (separate history) |
| **EVM Implementation** | Interpreter | Interpreter | Interpreter + **parallel exec** | **JIT-compiled** (RyuJIT) | **Native compiled** (revm) |
| **Block Import** | ~3 blk/s | **85 blk/s** (28x) | ~76 blk/s (25x) | ~68 blk/s (22x) | Pipeline (est. 100x) |
| **State Trie Reads** | LevelDB 1x | LevelDB 1x | **MDBX 3x faster** | RocksDB 1.5x | **MDBX 3x faster** |
| **DB Compaction Stalls** | Frequent | Frequent | **None** (B+ tree) | Rare (tuned) | **None** (B+ tree) |
| **Transaction Execution** | Sequential | Sequential | **Parallel (exec3)** | Parallel (.NET TPL) | **Parallel (Rayon)** |
| **State Commit** | Per-block flush | Per-block flush | **Batched** (per stage) | Per-block flush | **Batched** (per stage) |
| **Snapshot/Pruning** | None (full archive) | **PBSS** (online) | **Native pruning** | Pruning supported | **Native pruning** |
| **Cold Start Time** | ~30s | ~15s | **~5s** (mmap) | ~20s | **~3s** (mmap) |
| **RPC Response Time** | ~50ms avg | ~30ms avg | **~5ms avg** (flat DB) | ~20ms avg | **~3ms avg** (flat DB) |
| **Concurrent RPC** | Limited | Limited | **High** (staged reads) | High (.NET async) | **Highest** (Tokio) |
| **Chain Reorganization** | Slow (trie revert) | Slow (trie revert) | **Fast** (history lookup) | Moderate | **Fast** (history lookup) |
| **Network Bandwidth** | No compression | **Snappy compressed** | **Snappy compressed** | **Snappy compressed** | **Snappy compressed** |
| **GC Pause Impact** | 10-50ms (Go GC) | 10-50ms (Go GC) | 10-50ms (Go GC) | 5-20ms (.NET GC) | **0ms** (no GC) |
| **Bug Class Diversity** | Go runtime only | Go runtime only | Go runtime only | **.NET runtime** | **Rust runtime** |
| **Upstream Rebasing** | N/A (is upstream) | Merge from v2.6.8 | Rebase from Erigon | Rebase from Nethermind | Rebase from Reth |

### 💡 Key Design Insights

| Advantage | Best Client(s) | Why It Matters |
|-----------|---------------|----------------|
| **Lowest disk footprint** | Erigon, Reth | Flat DB stores state without trie overhead — 40-60% less disk |
| **Lowest memory usage** | Erigon, Reth | Memory-mapped I/O lets OS manage pages; no heap bloat |
| **Fastest EVM execution** | Reth (revm), NM (JIT) | Native compiled Rust and JIT-compiled C# outperform interpreted Go |
| **Best concurrency** | Reth (Tokio+Rayon) | Async I/O + data-parallel execution across all CPU cores |
| **Maximum safety** | Reth (Rust) | Compile-time memory safety eliminates buffer overflows, use-after-free |
| **Fastest sync** | Erigon, Reth | Stage/pipeline architecture processes headers, bodies, execution in parallel |
| **Best historical queries** | Erigon, Reth | Temporal history stored natively — no archive node needed |
| **Different bug classes** | NM (C#), Reth (Rust) | A Go runtime bug can't affect C#/.NET or Rust clients simultaneously |
| **Easiest upstream rebase** | GP5 | Same codebase as v2.6.8 — minimal merge conflicts |

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
