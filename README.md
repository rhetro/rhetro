# Rhetro

**Structural Designer / Architect of the Cognitive Operating System**

I am developing the **Cognitive Operating System**, an AI architecture that explores meaning through structural configuration and topology, rather than statistical text generation (LLMs). 

In parallel to this research, I build independent systems-level tools that address structural limitations in Rust—focusing on representation, compile-time evaluation, and memory-efficient execution. 

These tools are not components of the Cognitive OS, but arise from the same structural principles.

> All my DSL engines (Axioma / Axiomabuf / Opejson / Opeyml / Xopsy / Xopsyml / Emlex) are implemented using pure macro_rules! only — without any procedural macros, syn, quote, or AST generation.
> Each engine performs compile-time structural computation — topology projection, path routing, pattern recognition, and static capacity planning — entirely through declarative macro expansion on raw token streams.
> No proc-macro overhead. No AST construction. Runtime behavior is reduced to the minimal operations required by the underlying data model (e.g., serde_json where applicable).

---

# Structural Principle

These systems are not isolated optimizations, utilities, or experimental Rust crates.

They are different projections of the same computational philosophy:

dynamic computation is progressively eliminated and replaced with deterministic structural routing.

Rather than relying on runtime interpretation, comparison, synchronization, borrow arbitration, or repeated structural traversal, the system resolves as much computation as possible into topology, coordinate projection, static routing, and pre-verified execution geometry.

Across the toolchain, this appears in different forms:

* mutable access transformed into verified disjoint topology
* ordering transformed into spatial routing
* hierarchical data transformed into coordinate space
* dynamic traversal transformed into static pointer paths
* synchronization transformed into deterministic convergence geometry

The objective is not conventional optimization.

The objective is to eliminate entire categories of runtime computation before execution begins.

---

# 📦 The Toolchain Overview

I recently designed and built the following foundational components to address specific architectural limitations in Rust:

| Name | Category | LOC | Dependency | Purpose |
|------|----------|-----|------------|---------|
| **RZAF (private)** | Structural Static Analyzer | 1100 | none | A static analysis engine that identifies vulnerabilities and state transitions by treating source code as pure structural topology, entirely bypassing AST generation. |
| **[Zan-sort](https://github.com/rhetro/zan-sort)** · [crates.io](https://crates.io/crates/zan-sort) | Execution Primitives | 500 | none | Hardware-oriented O(N) sorting engine saturating DRAM throughput via single-pass disjoint routing. |
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

---

# 🔭 The Toolchain

### What I Solve — The Missing Layer in Modern Computing
Modern languages and runtimes cannot natively express the following concepts:
* **Simultaneous mutable aliasing**
* **Deterministic execution on non-linear topologies**
* **Compile-time structural proofs**
* **Hardware-synchronous state convergence**
* **Zero-overhead structural mutation of dynamic data**

These are not mere targets for "performance tuning"; they represent structural impossibilities within the current computational model. My work focuses on developing the toolchains required to reconstruct these missing primitives.

<br><br>

## **Structural Execution Primitives**

<br>

### **[Zan-sort](https://github.com/rhetro/zan-sort) — Hardware-Oriented O(N) Sorting Engine**
> A structural sorting engine that abandons comparison-based evaluation entirely, treating ordering strictly as a hardware memory bandwidth saturation problem.

Most sorting implementations are limited by their misalignment with modern CPU memory hierarchies. `zan-sort` abandons the `Ord` trait, reducing the ordering rule to a single absolute `u64` key (`SortKey`). It achieves near-linear scaling through a hardware-adaptive pipeline:

* **Single-Pass Disjoint Routing:** For DRAM-bound datasets, dynamic precision scaling and global prefix-sum offsets assign disjoint write regions to threads. This enables lock-free parallel scatter writes with no atomics or shared mutable state.
* **Cache-Hierarchy Alignment:** Processing transitions across register-level insertion (N ≤ 16), L1-optimized comparison fallback, and L2-bound Structure of Arrays (SoA) bucketing with bitmap collision resolution.
* **Minimal Sufficient Structure:** Removes multi-pass histograms, thread coordination, and auxiliary algorithms—retaining only the mechanisms required to saturate theoretical memory throughput.

These architectural constraints yield the following empirical results:
* **100M elements:** 678 ms on 8 cores (vs. `rayon::par_sort_unstable` at 954 ms)  
* **5M elements:** 34.8 ms single-threaded (vs. `std::sort_unstable` at 154.8 ms)

<br>

### **[Ordex](https://github.com/rhetro/ordex) — Deterministic Aliasing & Generational Arena**
> A memory model that makes Rust’s “impossible” case—simultaneous mutable aliasing to multiple elements—deterministic with near-zero overhead relative to memory access.

A generational arena that preserves near-sequential memory access characteristics while resolving the structural limitation of simultaneous mutable aliasing in Rust.
* **Memory Layout Optimization:** `Option<Index>` is compressed to 8 bytes via Null Pointer Optimization (NPO), maintaining a compact representation that maximizes cache density without degrading access performance.
* **Simultaneous Access for N ≤ 16 (`align!`):** Performs verification using fixed-size stack arrays, enabling fully unrolled, bounded constant-time verification with zero heap allocation.
* **Simultaneous Access for N > 16 (`ordex`):** Switches to a batch verification model using O(N log N) sorting and O(N) linear scanning, aligning access patterns toward sequential traversal and achieving amortized zero allocations in high-frequency loops.

<br>

### **[Ordag](https://github.com/rhetro/ordag) — Static DAG Prover & Execution Engine**
> A compile-time prover that mathematically guarantees the absence of Read/Write conflicts in non-linear topologies, eliminating runtime safety checks entirely.

An execution engine that completely eliminates runtime borrow checking and complex locking mechanisms, which are typical bottlenecks in DAG processing. By utilizing Kahn's algorithm and stream ID tracking, it parses graph structures at compile time, mathematically proving the absolute absence of Read/Write data conflicts. This bypasses runtime safety validation entirely, generating a pure execution plan with zero allocation that maximizes hardware memory bandwidth.

<br>

### **[Ordent](https://github.com/rhetro/ordent) — Hardware-Synchronous Wave Router**
> A deterministic phase-collapse engine that converts Kuramoto synchronization into integer-based, SIMD-aligned hardware operations.

A hardware router designed to force "deterministic state collapse" on non-linear topologies. Using the Kuramoto model (synchronization phenomenon) as a mechanism, it computes phase synchronization across an entire network directly on silicon. It processes over 120 million edge computations per second (100,000 nodes, 800,000 edges in ~6.45ms/tick) on a single thread through the following optimizations:
* Drops heavy floating-point modulo operations, treating phase as a `u32` integer overflow (Binary Angle Measurement / BAM) for zero-cost calculation.
* Maintains topology in a Compressed Sparse Row (CSR) format, flipping the computation axis from edge-centric to node-centric to fundamentally eliminate data races.
* Achieves 100% SIMD (`f32x8`) lane saturation via a branchless Taylor series expansion.

<br><br>

## Static Projection & Compilation

### **[Axioma](https://github.com/rhetro/axioma) — Compile-Time JSON-to-Matrix Projection**
> A compile-time topology projector that treats JSON not as text, but as a static matrix of coordinates.

A declarative macro library that projects dynamic, hierarchical JSON structures directly into static 2D coordinate spaces (sparse matrices) at compile time. It completely avoids runtime parsing and heap allocations (`Vec`, `HashMap`), reaching values directly via O(1) jump tables. By eliminating procedural macros entirely, it compiles even massive JSON payloads in milliseconds.

<br>

### **[Axiomabuf](https://github.com/rhetro/axiomabuf) — 1-Pass Static Macro-Router for Protobuf**
> A zero-allocation Protocol Buffers router that replaces byte-parsing with structural routing.

A zero-allocation Protocol Buffers router designed for systems requiring extreme throughput. By eliminating per-byte boundary checks and mathematically proving memory space safety upfront, it eradicates LLVM panic paths and fixes branch prediction. Nested messages are handled via push-driven closure delegation, recording a throughput of ~1.36 GB/s, which approaches the physical limits of single-threaded DRAM sequential reads.

<br><br>

## Dynamic Data Surgery & Diagnostics

### **[Opejson](https://github.com/rhetro/opejson) / [Opeyml](https://github.com/rhetro/opeyml) — Compile-Time Path Router & Auto-vivification**
> A structural surgery DSL that converts deep path operations into static pointer chains, eliminating runtime parsing entirely.

Deep path operations on dynamic data (such as auto-vivification, which generates non-existent trees while assigning) typically carry the heavy overhead of runtime string path parsing. These DSLs expand path declarations (e.g., `.users[0].name`) entirely into static pointer chains and native memory access instructions at compile time. By neutralizing path parsing to zero, they execute millions of structural mutations per second and instant multi-dimensional array allocations (`mesh!`) at near bare-metal speeds.

<br>

### **[Xopsy](https://github.com/rhetro/xopsy) / [Xopsyml](https://github.com/rhetro/xopsyml) — Zero-Allocation Structural Pattern Matcher**
> A structural matcher that bypasses Rust’s borrow-checker limitations by operating directly on topology, not text.

Standard Rust struggles with extracting multiple mutable references (`&mut`) deep within JSON or YAML nests, often leading to strict borrow checker errors (E0499/E0502) or massive `if let` chains. These DSLs solve this via CPS and a Two-Phase Pointer-Relay Architecture (strictly separating pure evaluation from unsafe binding). They explore target nodes via stack-only pointer arithmetic and extract safe mutable references with zero runtime memory allocation.

---

# 🔍 Focus
* **Non-LLM AI:** Meaning-driven intelligence via structural cognition.
* **Mechanical Sympathy:** Optimizing high-level data structures for hardware realities (e.g., cache locality, register-level checks).
* **Compile-time Abstraction:** Moving dynamic evaluations to compile-time resolution via macros.

---

# 🧩 Parallel Tools
Additional structural tools that coexist with the Cognitive OS toolchain.

<br>

### **RZAF — Structural Static Analyzer**
> A static analysis engine that identifies logical vulnerabilities and state transitions by treating source code as pure structural topology, entirely bypassing conventional parsing and data-flow analysis.

Standard static analyzers are bottlenecked by heavy memory allocations (AST generation) and often become paralyzed by the complexity of global data-flow tracking. RZAF discards these dynamic interpretations entirely. By projecting the codebase directly into a structural space, it locates deep invariants and physical sinks (e.g., panic paths, unsafe boundaries) through localized topological constraints.

* Topological Context Retention: Instead of attempting to trace global data-flow across complex logic, RZAF perfectly preserves localized semantic meaning. It tracks structural boundaries (such as scope depth) and mutable state transitions purely as spatial relationships, pinpointing diagnostic targets without dynamic traversal.
* Zero-Allocation Diagnostic Routing: By eliminating tree construction and dynamic heap allocation on the execution path, the engine processes structural evaluations directly. This allows it to achieve pinpoint diagnostic accuracy at near bare-metal execution speeds.
* Deterministic Structural Isolation: Target signatures, macros, and structural invariants are isolated into completely flat, disjoint topographies. This thoroughly prevents the memory fragmentation and traversal overhead typical of object-oriented syntax analysis.

> ** Status: Internal / Proprietary Tool**
> Due to its extreme efficacy in rapid zero-day discovery and physical vulnerability mapping across production codebases, RZAF is maintained as a strictly private internal tool. It is utilized exclusively for independent security research and private auditing.

<br>

### **[Emlex](https://github.com/rhetro/emlex) — Compile-Time S-Expression Math Engine**  
A compile-time S-expression DSL built entirely with `macro_rules!`, treating mathematics as a structural object rather than a runtime computation. It fully parses S-expressions using declarative macros, constructs ASTs via Continuation-Passing Style (CPS) to bypass recursion limits, and regenerates reverse DSL forms for structural optimization (e.g., `exp(ln(x)) → x`).  
Evaluation is deferred into non‑capturing function pointers, enabling LLVM Dead Code Elimination (DCE) to erase unused ASTs and enforce zero runtime overhead. Emlex provides dual engines—real-number DSL `eml!` and complex-number DSL `ceml!`—capable of evaluating expressions such as Euler’s identity at compile time.

---

# 🔗 Links & Contact
* **Research:** [Cognitive Operating System (Zenodo)](https://doi.org/10.5281/zenodo.18191421)
* **Updates & Visual Demos:** [Non-Linear Network Boids Simulation (Lotka-Volterra Model / Rust + Wasm)](https://rhetro.pages.dev/rust/ordex/)
* **Architecture Discussion:** [Discord Server](https://discord.com/invite/Eb5xxSr96b) 
* **Contact:** `rhetro@rhetroxc.com` (For consulting, sponsorships, and core research inquiries)
