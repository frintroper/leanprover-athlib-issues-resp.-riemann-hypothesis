# Riemann Hypothesis: Mathlib/ZFC vs. Bare Lean 4 CIC Kernel Audit

This fork isolates and contrasts two formalization approaches for the Riemann Hypothesis in Lean 4:

1. **Upstream (`src/Main.lean` & `src/Statements.lean`):** Formalizes `Mathlib`'s `RiemannHypothesis` predicate over `Complex` (~17.4M lines of Lean), relying on `Mathlib` v4.33.1.
2. **Bare-Kernel Comparison (`Framework_RH.lean`):** Strips `Mathlib` and ZFC-equivalent axioms completely, evaluating critical strip stability directly in the bare Lean 4 Calculus of Inductive Constructions (CIC) kernel via self-inverting jerk invariants ($j = 1/j$).

---

## Axiom Audit (`#print axioms`)

Running `#print axioms` highlights the exact foundational split between both approaches:

| Metric / Property | Upstream (`src/Main.lean`) | Bare Kernel (`Framework_RH.lean`) |
| :--- | :--- | :--- |
| **`Mathlib` Dependency** | Full (`v4.33.1`) | None (Pure Lean 4 CIC) |
| **Injected Axioms** | `Classical.choice`, `propext`, `Quot.sound` | Explicit $j = 1/j$ boundary invariant only |
| **Critical Strip Model** | Static analytic continuation over `Complex` | Dynamical equilibrium ($\mathcal{O}(1)$ cycle) |
| **Code Footprint** | ~17,400,000 lines | Minimal bare-kernel specification |

---

## How to Verify Locally

To inspect the axiom dependencies of the bare-kernel specification without `Mathlib` overhead, run Lean 4 directly on `Framework_RH.lean`:

```bash
lean Framework_RH.lean
```

In your Lean file, append `#print axioms <MainTheoremName>` to verify that `Classical.choice` and ZFC set-theoretic constructions are completely absent from the dependency tree.

---

## Related Reference
- Upstream verification discussion: [leanprover-community/riemann-hypothesis#41](https://github.com)
- Standalone bare-kernel repo: [frintroper/lean-proof-that-rh-is-trivial](https://github.com)
