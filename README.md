# Tiferet Quantum

**Tiferet-Quantum** is a polymorphic extension of [Tiferet](https://github.com/greatstrength/tiferet):
a Domain-Driven Design framework whose Abstract Core
(`DomainObject`, `DomainEvent`, `Aggregate`, `Service`) is reused rather
than rewritten. This repository tests that those building blocks are a
Pythonic realization of the Multi-Level Intermediate Representation
(MLIR) dialect / operation / pass model, proved in a quantum compilation
domain that enforces physical law at the domain boundary and lowers to
existing Python quantum toolchains.

This repository is the software artifact for:

> **Ontology as Infrastructure: Bridging Multi-Level Intermediate
> Representations and Domain-Driven Design in Quantum Systems**

The domain is not implemented yet. What exists today is the study
surface: the conference abstract, the domain vision statement, and the
core domain distillation.

Implementation is specified as a **Request for Prototype (RFP)** — a
public issue that states one domain theory, its motivation, and the
acceptance criteria for testing that theory on a prototype branch. An
RFP is not a **Technical Requirements Document (TRD)**. A TRD is the
later trunk specification used to reconstruct a frozen catalog of named
artifacts, or to hotfix a mechanical defect, on the main line. The first
proof in this repository is 13 RFPs.

## The claim

MLIR is the right multi-level compiler architecture. Its cost of entry —
C++, TableGen, CMake, and a multi-million-line LLVM tree — is accidental
complexity, not essential complexity. Quantum software currently pays
that cost or else falls back to OpenQASM string round-trips between
PennyLane, Qiskit, Cirq, and specialized mappers.

Tiferet-Quantum keeps one checked circuit model in Python and talks to
those tools through service interfaces. Linear typing (no-cloning) and
coupling legality are domain rules. Placement search, simulation, and
MLIR / LLVM code generation stay in the libraries that already do them
well. New domains and backends extend the same abstract core; they do
not fork it.

## Documents

- [`docs/quantum/abstract.md`](docs/quantum/abstract.md) — abstract
  and keywords
- [`docs/quantum/domain-vision.md`](docs/quantum/domain-vision.md) —
  value proposition (the bet, the benefits, the non-goals)
- [`docs/quantum/core-domain-distillation.md`](docs/quantum/core-domain-distillation.md) —
  ubiquitous language, pipeline, agnostic/variable seam, and the 13 RFPs

Read the vision first. The distillation depends on the framing it
establishes.

## Intended pipeline

> **Ingest** → **Verify** → **Synthesize** → **Optimize** → **Map** → **Emit**

Four axes of variation, named so each RFP can own one edge:

1. **B** — gate basis (Clifford+T first)
2. **G** — hardware coupling topology
3. **S** — optimization strategy
4. **D** — emission dialect (OpenQASM, MLIR `quantum`, MLIR `mqtopt`,
   later Quantum Intermediate Representation (QIR))

## Prototype slice

The first proof is 13 RFPs. Each item is one falsifiable predicate.
Author an RFP with `tiferet-author-rfp` and implement it on the
prototype branch. Do not write a TRD for this work. The numbered list
and the follow-on work live in Section 10 of the distillation.

1. Application skeleton
2. Quantum value objects
3. Circuit aggregate
4. Linear typing
5. Circuit ingest
6. Coupling validation
7. Basis synthesis
8. Local optimization
9. Mapping service and MQT QMAP
10. OpenQASM emission
11. MLIR dialect emission
12. Compile feature workflow
13. GHZ case study (Hopf et al., SCA/HPCAsia 2026)

## Status

| Piece | State |
| --- | --- |
| Study documents | Draft on `master` |
| `quantum/` package | Not started |
| Application wiring | Not started |
| Tests | Not started |

## Setup (when implementation starts)

**Prerequisites:** Python 3.10+, pip

```bash
git clone https://github.com/Ashatz/tiferet-quantum.git
cd tiferet-quantum
python -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
```

Expected runtime dependencies, once the corresponding RFPs land:

- [tiferet](https://github.com/greatstrength/tiferet)
- [mqt.core](https://github.com/munich-quantum-toolkit/core) /
  [mqt.qmap](https://github.com/munich-quantum-toolkit/qmap)
- Optional later edges: PennyLane / Catalyst, PyZX, Qiskit, Cirq

## Related work this study answers

Hopf, P., Ochoa, E., Stade, Y., Rovara, D., Quetschlich, N., Florea,
I. A., Izaac, J., Wille, R., and Burgholzer, L. (2026). *Integrating
Quantum Software Tools with(in) MLIR.* SCA/HPCAsia 2026.
https://doi.org/10.1145/3773656.3773658

That paper shows why quantum groups bounce off MLIR and how a
PennyLane–MQT plugin lowers the barrier inside LLVM. This project asks
whether the same dialect / pass / plugin shape can be declared in
Tiferet first, with those libraries as injectable edges.

## License

[MIT](LICENSE) © 2026 Andrew Shatz.
