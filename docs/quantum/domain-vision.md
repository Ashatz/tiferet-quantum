# Domain Vision Statement — Quantum Compilation

**Status:** Draft · **Domain:** `quantum` · **Code:** `quantum/` · **Branch:** `master`

## The bet

Quantum software engineering today is bottlenecked by fragmented toolchains
and fragile string-based exchange formats. Developers assemble quantum
programs in high-level frameworks like PennyLane, Qiskit, or Cirq, only to
serialize them into unstructured OpenQASM text files when delegating to
specialized placement, routing, or verification tools. This ad hoc
round-tripping destroys program hierarchy, obscures multi-level control flow,
and defers basic physical mistakes until something expensive actually runs.

Modern compiler infrastructure such as MLIR is the architectural answer:
named operation vocabularies at several levels of detail, structured control
flow, and values that are written once and then consumed. But using it as
shipped imposes an engineering barrier that most quantum groups cannot
absorb — C++ template metaprogramming, TableGen code generators, intricate
CMake builds, and a compiler footprint that alienates physicists and domain
scientists.

Our bet is that **compiler mechanics and domain rules do not require that
C++ accidental complexity**. By modeling quantum compilation as a declared,
domain-driven architecture in Python, we can catch physical violations —
a qubit used twice, or a two-qubit gate on unconnected hardware — at the
domain boundary, while still orchestrating placement, optimization, and MLIR
generation through existing Python libraries.

## What this domain makes real

The `quantum` domain is a verified software platform for representing,
checking, transforming, and lowering quantum computation. It takes in a
circuit description, enforces physical and algebraic rules on that
description, and drives modular compilation pipelines across more than one
execution backend — so a single circuit model can reach classical
simulators, quantum-specific tools, and reconfigurable hardware targets
without being rewritten for each of them.

## What we get for it

### 1. Physical mistakes caught before execution

Quantum circuits have strict physical constraints: a qubit cannot be
cloned, non-adjacent physical qubits cannot interact without a SWAP (an
exchange of two qubit positions), and rotation angles must match the
target gate set. The domain checks qubit lifecycles and hardware
connectivity as soon as a circuit is built. Invalid instruction sequences
fail with a named error at the file and rule that broke, instead of
failing later on a simulator or a physical device.

### 2. Several backends, one circuit model

Instead of converting circuits back and forth through lossy text files,
the domain keeps one in-memory circuit model. That same model can be
placed and routed by the Munich Quantum Toolkit, simplified by diagrammatic
tools such as PyZX, decomposed into a standard gate set, or compiled into
MLIR text (`quantum`, `mqtopt`, `quake`) and QIR binaries.

### 3. Compiler work that stays in Python

Domain scientists, algorithm developers, and compiler engineers work with
declared Python objects rather than thousands of lines of TableGen or
low-level LLVM passes. A new gate, a new connectivity rule, or a new
optimization step can be authored, tested, and composed without rebuilding
the compiler.

## The core of the work

The quantum domain runs in four discrete phases:

1. **Declare and ingest.** Capture a quantum program as named qubits,
   registers, gates, and a hardware connectivity graph, keeping classical
   parameters and structured control flow intact.
2. **Verify.** Ensure each qubit is produced and consumed exactly once, and
   that two-qubit operations respect the target device's connectivity.
3. **Transform.** Run pluggable steps — gate commutation, T-depth
   reduction, initial placement, and SWAP routing — as declared domain
   operations.
4. **Emit.** Lower the checked, transformed circuit into MLIR dialect text,
   OpenQASM 3.0, QIR, or a simulator task through injectable services.

The design commitment is that **the domain model is the single source of
truth**. Gate operations, connectivity constraints, and compilation stages
are explicit, immutable domain artifacts. Tiferet supplies the shared
building blocks; this domain supplies the quantum rulebook.

## What it deliberately does not do

* **It does not generate hardware pulses.** Nanosecond-scale microwave
  shaping belongs to target-specific control runtimes such as Qiskit Pulse
  or Qblox drivers.
* **It does not write a new quantum simulator.** State-vector propagation,
  decision-diagram simulation, and tensor-network contraction are delegated
  to existing libraries (MQT DDSIM, PennyLane Lightning, Qiskit Aer)
  behind service interfaces.
* **It does not schedule classical HPC clusters.** Multi-node execution
  belongs to the application session and runtime layers, not this domain.

---

*Companion document:* `docs/quantum/core-domain-distillation.md` — the
detailed walkthrough of the domain's vocabulary, behaviors, and the
relationships between its parts.
