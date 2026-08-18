# Ontology as Infrastructure: Bridging Multi-Level Intermediate Representations and Domain-Driven Design in Quantum Systems

**Status:** Draft · **Kind:** Abstract · **Domain:** `quantum` · **Branch:** `master`

## Abstract

As computational paradigms scale toward radical physical heterogeneity, compiler toolchains face a structural bottleneck: the divergence between high-level domain models and low-level execution mechanics. In quantum software engineering this friction is acute. Workflows remain split between scientific frameworks that exchange circuits as lossy text (e.g., OpenQASM) and multi-level compilers such as MLIR, whose C++, TableGen, and CMake overhead bars most domain specialists from extending the stack.

We present an architectural paradigm that treats **ontology as infrastructure**, establishing a structural isomorphism among **Domain-Driven Design (DDD)**, **Multi-Level Intermediate Representations (MLIR)**, and **General Systems Theory**. Dialect namespaces map to bounded contexts, operations to domain events, SSA values to immutable value objects, and transformation passes to deterministic feature workflows. Formal system metaphors then let compilers hold domain vocabularies as modular, stable intermediate representations.

We realize the paradigm in **Tiferet** and validate it in **Tiferet-Quantum**, a polymorphic extension of that abstract core: a pure-Python quantum compilation domain that inherits Tiferet's unopinionated building blocks, enforces physical invariants at the domain boundary, and remains open to further domain and backend extension while lowering to existing MLIR dialects and quantum toolchains.

**Keywords:** Domain-Driven Design, MLIR, Quantum Compilation, Ontology, Systems Theory

---

*Companion documents:* `docs/quantum/domain-vision.md`, `docs/quantum/core-domain-distillation.md`.
