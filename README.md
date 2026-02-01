# Johail Gerard

**Computer Engineering & Mathematics | University of Illinois at Urbana-Champaign**

Distributed systems, hardware design, ML optimization, and the occasional chess engine. I tend to start with a hard theoretical problem and end with working code.

[GitHub](https://github.com/johailg2)

---

## Research

**KV Cache Optimization for LLMs** — *Prof. Indranil Gupta, UIUC (Current)*
Optimizing key-value cache strategies for transformer inference to reduce memory footprint and improve throughput at scale.

**MRI Image Denoising** — *Prof. Zhi-Pei Liang, UIUC*
Signal processing research on denoising MRI data, combining classical signal theory with learned approaches.

---

## Industry

**Gridspace — Software Engineer Intern (Summer 2025, Los Angeles)**

Three threads of work. The first was latency benchmarking across the full speech pipeline — tracing from the first TCP byte at ingress through ASR, a decision state machine, an LLM, and out to the first TTS audio frame. Co-built a reproducible testbed with per-stage monotonic timers so we could actually pinpoint where the bottlenecks lived and catch regressions going forward.

The second was porting the entire infrastructure from GCP to AWS — GKE→EKS, GCE→EC2, GCS→S3, load balancers, networking, IAM. Wrote AWS resource classes in their Forge IaC DSL so the whole dev environment could come up in one command, while keeping behavior parity with the GCP setup.

The third was data ingestion: built a multilingual (Spanish/English) voice ingestion pipeline with deterministic schemas and validators, normalized transcripts for training and eval consumption, and designed the acronym handling — protected tokens for ASR so it doesn't mangle abbreviations, structured tokens for TTS so it actually pronounces them correctly (e.g., MRI → "M-R-I").

---

**Hindustan Unilever — Intern (Summer 2024, Mumbai)**

Worked on an ML-based inventory forecasting system. The main concrete win was cutting cloud costs by 65% through spot VMs and smarter job scheduling. Also did a research pass across forecasting approaches — Naive Bayes, SARIMA, RNNs, CNNs — and squeezed out a 3% accuracy improvement through model tuning and better feature engineering.

---

## Projects

### Chess Engine
**C | Bitboards | [GitHub →](https://github.com/johailg2/Chess-Engine-)**

A full chess engine built from scratch using bitboard representations for fast move generation and position evaluation. Recently went through a deep code review and refactor — fixed critical bugs in queen move generation and the black knight evaluation function. Supports full game play with move validation across all piece types.

### Order Flow Imbalance — Equity Markets
**Python | Jupyter | [GitHub →](https://github.com/johailg2/Cross-Impact-of-Order-Flow-Imbalance-in-Equity-Markets)**

Quantitative analysis of cross-impact effects: how order flow imbalance in one equity propagates to price dynamics in correlated stocks. Relevant to market microstructure and algorithmic trading strategy design.

---

### Distributed Systems
*Built from scratch in Go. Source for these is in private course repositories.*

#### RainStorm — Stream Processing Framework

Distributed stream processor (à la Apache Storm) running pipelines of user-defined operators across a node cluster.

- **Fault tolerance:** Leader detects worker crashes and reschedules tasks to healthy nodes, replaying tuples to guarantee exactly-once processing semantics.
- **Autoscaling:** A Resource Manager monitors per-stage throughput (tuples/sec) and automatically provisions or deprovisions worker threads based on load.
- **State persistence:** Stateful operator data (e.g., running aggregates) is backed by HyDFS, surviving node failures without data loss.

#### HyDFS — Hybrid Distributed File System

Distributed file system for large files across a 10-node cluster, drawing from HDFS and Cassandra design.

- Consistent Hashing (ring topology) maps files to nodes with minimal reshuffling on cluster resize.
- Chain Replication with a factor of 3. Sequential Consistency for concurrent writes, Read-Your-Writes consistency for clients.
- Self-healing: nodes monitor successors and automatically re-replicate under-replicated data on failure detection.

#### SWIM Membership Protocol

Peer-to-peer cluster membership service using gossip-style heartbeats.

- Failure information propagates to all nodes in under 6 seconds (time-bounded completeness).
- Suspicion mechanism distinguishes real crashes from transient network issues, cutting false positive detections significantly.
- Constant bandwidth regardless of cluster size.

---

### Low-Level Systems

#### x86 Kernel *(ECE 391)*
UNIX-like kernel from scratch: i8259 PIC interrupt handling, paging for process isolation, round-robin scheduling, and custom drivers for keyboard, mouse, and VGA display.

#### RISC-V Processor *(ECE 411)*
Synthesizable 32-bit RISC-V core in SystemVerilog. 5-stage pipeline with data forwarding, dynamic branch prediction, and an integrated L1 cache.

---

### Signal Processing

#### Adaptive Green Screen *(ECE 420)*
Android app that does green-screen compositing without a physical green screen. A real-time K-Means variant learns the background color distribution and subtracts it dynamically. Went from ~2 FPS in Java to real-time after rewriting the critical path in C++ via the Android NDK.

---

## Tech Stack

**Languages:** C, C++, Go, Python, Java, SystemVerilog
**Cloud & Infra:** AWS (EC2, EKS, S3, IAM), GCP (GCE, GKE, GCS), Kubernetes, IaC
**Hardware:** x86 Assembly, RISC-V, i8259 PIC, FPGA toolchain
**Systems:** Distributed consensus, consistent hashing, stream processing, fault tolerance, chain replication
**ML / Data:** K-Means clustering, SARIMA, RNNs, CNNs, MRI signal processing, LLM inference optimization
**Tools:** Android NDK, Jupyter, NumPy, Pandas, Git
