# Rhetro

**Structural Designer / Architect of the Cognitive Operating System**

I am developing the **Cognitive Operating System**, an AI architecture designed to generate meaning through structural configuration and topology, rather than relying on statistical text generation (LLMs). 

To support this, I build systems-level tools that focus on structural representation, compile-time evaluation, and memory-efficient runtime execution.

## 🔭 The Toolchain
I recently designed and built the following foundational components to address specific architectural limitations in Rust:

* **[Ordex](https://github.com/rhetro/ordex)** — A strict, generational arena allocator designed for multi-mutable graph topologies. It enables simultaneous mutable access to multiple elements without per-access heap allocations. (Driving 100 FPS on Wasm for 4,000 nodes in real-time Lotka-Volterra simulations).
* **[Axioma](https://github.com/rhetro/axioma)** — Compile-time declarative macros for static JSON-to-Matrix topology projection.
* **[Axiomabuf](https://github.com/rhetro/axiomabuf)** — A 1-pass, zero-allocation static macro-router for Protocol Buffers. It structurally eliminates panic paths to achieve DRAM physical limit throughput (~1.36 GB/s) via push-driven delegation.
* **[Xopsy](https://github.com/rhetro/xopsy)** — A structural pattern-matching DSL for JSON diagnostics.
* **[Opejson](https://github.com/rhetro/opejson)** — Surgical macros that provide safe auto-vivification for JSON manipulation in Rust.
* **[Opeyml](https://github.com/rhetro/opeyml)** — The strict YAML counterpart to `opejson`. Reduces complex topological mutations down to pure, static memory operations without runtime parsing.


## 🧠 Focus
* **Non-LLM AI:** Meaning-driven intelligence via structural cognition.
* **Mechanical Sympathy:** Optimizing high-level data structures for hardware realities (e.g., cache locality, register-level checks).
* **Compile-time Abstraction:** Moving dynamic evaluations to compile-time resolution via macros.

## 🔗 Links & Contact
* **Research:** [Cognitive Operating System (Zenodo)](https://doi.org/10.5281/zenodo.18191421)
* **Updates & Visual Demos:** [Non-Linear Network Boids Simulation (Lotka-Volterra Model / Rust + Wasm)](https://rhetro.pages.dev/rust/ordex/)
* **Architecture Discussion:** [Discord Server](https://discord.com/invite/Eb5xxSr96b) 
* **Contact:** `rhetro@rhetroxc.com` (For consulting, sponsorships, and core research inquiries)
