# Rhetro

**Structural Designer / Architect of the Cognitive Operating System**

I am developing the **Cognitive Operating System**, an AI architecture that explores meaning through structural configuration and topology, rather than statistical text generation (LLMs). 

In parallel to this research, I build independent systems-level tools that address structural limitations in Rust—focusing on representation, compile-time evaluation, and memory-efficient execution. 

These tools are not components of the Cognitive OS, but arise from the same structural principles.


## 📦 The Toolchain Overview

I recently designed and built the following foundational components to address specific architectural limitations in Rust:

| Name | Category | LOC | Dependency | Purpose |
|------|----------|-----|------------|---------|
| **[Zan-sort](https://github.com/rhetro/zan-sort)** · [crates.io](https://crates.io/crates/zan-sort) | Execution Primitives | 500 | none | Hardware-oriented near-linear routing-based sort saturating DRAM bandwidth. |
| **[Ordex](https://github.com/rhetro/ordex)** · [crates.io](https://crates.io/crates/ordex) | Execution Primitives | 400 | none | Deterministic multi-mutable aliasing with near-zero overhead and cache-efficient access patterns. |
| **[Ordag](https://github.com/rhetro/ordag)** · [crates.io](https://crates.io/crates/ordag) | Execution Primitives | 180 | ordex | Compile-time DAG prover eliminating all runtime alias checks. |
| **[Ordent](https://github.com/rhetro/ordent)** · [crates.io](https://crates.io/crates/ordent) | Execution Primitives | 180 | ordex | Hardware-quantized Kuramoto engine for deterministic phase collapse. |
| **[Axioma](https://github.com/rhetro/axioma)** · [crates.io](https://crates.io/crates/axioma) | Static Projection & Compilation | 400 | none | Compile-time JSON-to-matrix topology projection. |
| **[Axiomabuf](https://github.com/rhetro/axiomabuf)** · [crates.io](https://crates.io/crates/axiomabuf) | Static Projection & Compilation | 580 | none | Zero-allocation 1-pass Protobuf macro-router. |
| **[Emlex](https://github.com/rhetro/emlex)** · [crates.io](https://crates.io/crates/emlex) | Static Projection & Compilation | 280 | num-complex | Compile-time S-expression math engine (macro_rules!-only). |
| **[Opejson](https://github.com/rhetro/opejson)** · [crates.io](https://crates.io/crates/opejson) | Dynamic Data Surgery & Diagnostics | 500 | serde_json | Zero-overhead JSON surgery via static pointer-chain compilation. |
| **[Opeyml](https://github.com/rhetro/opeyml)** · [crates.io](https://crates.io/crates/opeyml) | Dynamic Data Surgery & Diagnostics | 350 | serde_yaml | YAML structural mutation via static memory operations. |
| **[Xopsy](https://github.com/rhetro/xopsy)** · [crates.io](https://crates.io/crates/xopsy) | Dynamic Data Surgery & Diagnostics | 300 | serde_json | Structural JSON pattern matcher bypassing borrow-checker limits. |
| **[Xopsyml](https://github.com/rhetro/xopsyml)** · [crates.io](https://crates.io/crates/xopsyml) | Dynamic Data Surgery & Diagnostics | 480 | serde_yaml | YAML diagnostic prism for zero-allocation structural matching. |


## 🔭 The Toolchain

### What I Solve — The Missing Layer in Modern Computing
Modern languages and runtimes cannot natively express the following concepts:
* **Simultaneous mutable aliasing**
* **Deterministic execution on non-linear topologies**
* **Compile-time structural proofs**
* **Hardware-synchronous state convergence**
* **Zero-overhead structural mutation of dynamic data**

These are not mere targets for "performance tuning"; they represent structural impossibilities within the current computational model. My work focuses on developing the toolchains required to reconstruct these missing primitives.


### Structural Execution Primitives

**[Zan-sort](https://github.com/rhetro/zan-sort) — Hardware-Oriented Hybrid Sort**
> A sorting engine that treats ordering as deterministic routing rather than comparison, aligning the entire pipeline with physical memory boundaries.

Sorting performance is limited not by algorithmic complexity but by hardware utilization. zan-sort reduces ordering to a single absolute `u64` key and executes a multi-phase routing pipeline designed to saturate DRAM bandwidth.

* **Disjoint Parallel Routing:** Dynamically scales bucket precision and maps the key space into 32 bits via dynamic precision scaling. Threads perform concurrent scatter writes into a unified buffer using precomputed disjoint prefix-sum offsets, eliminating locks and shared-state contention.
* **Cache-Boundary Execution:** Switches execution phases strictly based on physical cache limits. Local SoA bucketing remains within L2 boundaries to avoid DRAM penalties, while L1-resident datasets fall back to comparison logic only when it is physically optimal.

**[Ordex](https://github.com/rhetro/ordex) — Deterministic Aliasing & Generational Arena**
> A memory model that makes Rust’s “impossible” case—simultaneous mutable aliasing to multiple elements—deterministic with near-zero overhead relative to memory access.

A generational arena that preserves near-sequential memory access characteristics while resolving the structural limitation of simultaneous mutable aliasing in Rust.
* **Memory Layout Optimization:** `Option<Index>` is compressed to 8 bytes via Null Pointer Optimization (NPO), maintaining a compact representation that maximizes cache density without degrading access performance.
* **Simultaneous Access for N ≤ 16 (`align!`):** Performs verification using fixed-size stack arrays, enabling fully unrolled, bounded constant-time verification with zero heap allocation.
* **Simultaneous Access for N > 16 (`ordex`):** Switches to a batch verification model using O(N log N) sorting and O(N) linear scanning, aligning access patterns toward sequential traversal and achieving amortized zero allocations in high-frequency loops.


**[Ordag](https://github.com/rhetro/ordag) — Static DAG Prover & Execution Engine**
> A compile-time prover that mathematically guarantees the absence of Read/Write conflicts in non-linear topologies, eliminating runtime safety checks entirely.

An execution engine that completely eliminates runtime borrow checking and complex locking mechanisms, which are typical bottlenecks in DAG processing. By utilizing Kahn's algorithm and stream ID tracking, it parses graph structures at compile time, mathematically proving the absolute absence of Read/Write data conflicts. This bypasses runtime safety validation entirely, generating a pure execution plan with zero allocation that maximizes hardware memory bandwidth.


**[Ordent](https://github.com/rhetro/ordent) — Hardware-Synchronous Wave Router**
> A deterministic phase-collapse engine that converts Kuramoto synchronization into integer-based, SIMD-aligned hardware operations.

A hardware router designed to force "deterministic state collapse" on non-linear topologies. Using the Kuramoto model (synchronization phenomenon) as a mechanism, it computes phase synchronization across an entire network directly on silicon. It processes over 120 million edge computations per second (100,000 nodes, 800,000 edges in ~6.45ms/tick) on a single thread through the following optimizations:
* Drops heavy floating-point modulo operations, treating phase as a `u32` integer overflow (Binary Angle Measurement / BAM) for zero-cost calculation.
* Maintains topology in a Compressed Sparse Row (CSR) format, flipping the computation axis from edge-centric to node-centric to fundamentally eliminate data races.
* Achieves 100% SIMD (`f32x8`) lane saturation via a branchless Taylor series expansion.


### Static Projection & Compilation

**[Axioma](https://github.com/rhetro/axioma) — Compile-Time JSON-to-Matrix Projection**
> A compile-time topology projector that treats JSON not as text, but as a static matrix of coordinates.

A declarative macro library that projects dynamic, hierarchical JSON structures directly into static 2D coordinate spaces (sparse matrices) at compile time. It completely avoids runtime parsing and heap allocations (`Vec`, `HashMap`), reaching values directly via O(1) jump tables. By eliminating procedural macros entirely, it compiles even massive JSON payloads in milliseconds.


**[Axiomabuf](https://github.com/rhetro/axiomabuf) — 1-Pass Static Macro-Router for Protobuf**
> A zero-allocation Protocol Buffers router that replaces byte-parsing with structural routing.

A zero-allocation Protocol Buffers router designed for systems requiring extreme throughput. By eliminating per-byte boundary checks and mathematically proving memory space safety upfront, it eradicates LLVM panic paths and fixes branch prediction. Nested messages are handled via push-driven closure delegation, recording a throughput of ~1.36 GB/s, which approaches the physical limits of single-threaded DRAM sequential reads.


### Dynamic Data Surgery & Diagnostics

**[Opejson](https://github.com/rhetro/opejson) / [Opeyml](https://github.com/rhetro/opeyml) — Compile-Time Path Router & Auto-vivification**
> A structural surgery DSL that converts deep path operations into static pointer chains, eliminating runtime parsing entirely.

Deep path operations on dynamic data (such as auto-vivification, which generates non-existent trees while assigning) typically carry the heavy overhead of runtime string path parsing. These DSLs expand path declarations (e.g., `.users[0].name`) entirely into static pointer chains and native memory access instructions at compile time. By neutralizing path parsing to zero, they execute millions of structural mutations per second and instant multi-dimensional array allocations (`mesh!`) at near bare-metal speeds.


**[Xopsy](https://github.com/rhetro/xopsy) / [Xopsyml](https://github.com/rhetro/xopsyml) — Zero-Allocation Structural Pattern Matcher**
> A structural matcher that bypasses Rust’s borrow-checker limitations by operating directly on topology, not text.

Standard Rust struggles with extracting multiple mutable references (`&mut`) deep within JSON or YAML nests, often leading to strict borrow checker errors (E0499/E0502) or massive `if let` chains. These DSLs solve this via CPS and a Two-Phase Pointer-Relay Architecture (strictly separating pure evaluation from unsafe binding). They explore target nodes via stack-only pointer arithmetic and extract safe mutable references with zero runtime memory allocation.


## 🔍 Focus
* **Non-LLM AI:** Meaning-driven intelligence via structural cognition.
* **Mechanical Sympathy:** Optimizing high-level data structures for hardware realities (e.g., cache locality, register-level checks).
* **Compile-time Abstraction:** Moving dynamic evaluations to compile-time resolution via macros.


## 🧩 Parallel Tools
Additional structural tools that coexist with the Cognitive OS toolchain.

**[Emlex](https://github.com/rhetro/emlex) — Compile-Time S-Expression Math Engine**  
A compile-time S-expression DSL built entirely with `macro_rules!`, treating mathematics as a structural object rather than a runtime computation. It fully parses S-expressions using declarative macros, constructs ASTs via Continuation-Passing Style (CPS) to bypass recursion limits, and regenerates reverse DSL forms for structural optimization (e.g., `exp(ln(x)) → x`).  
Evaluation is deferred into non‑capturing function pointers, enabling LLVM Dead Code Elimination (DCE) to erase unused ASTs and enforce zero runtime overhead. Emlex provides dual engines—real-number DSL `eml!` and complex-number DSL `ceml!`—capable of evaluating expressions such as Euler’s identity at compile time.


## 🔗 Links & Contact
* **Research:** [Cognitive Operating System (Zenodo)](https://doi.org/10.5281/zenodo.18191421)
* **Updates & Visual Demos:** [Non-Linear Network Boids Simulation (Lotka-Volterra Model / Rust + Wasm)](https://rhetro.pages.dev/rust/ordex/)
* **Architecture Discussion:** [Discord Server](https://discord.com/invite/Eb5xxSr96b) 
* **Contact:** `rhetro@rhetroxc.com` (For consulting, sponsorships, and core research inquiries)
