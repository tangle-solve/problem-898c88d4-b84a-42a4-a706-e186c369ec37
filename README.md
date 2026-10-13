<!-- solve-problem:898c88d4-b84a-42a4-a706-e186c369ec37 -->
# QMA versus QMA(2)

A [Tangle Solve problem](https://solve.tangle.tools/problems/898c88d4-b84a-42a4-a706-e186c369ec37).

## What is the problem?

QMA is quantum Merlin–Arthur: a polynomial-time quantum verifier with a polynomial-size quantum witness state ρ, accepting YES instances with probability ≥ 2/3 and NO instances with probability ≤ 1/3 (completeness/soundness gaps of 1/poly allowed). QMA(2) (also written QMA(k)) is the variant where Merlin sends k ≥ 2 witnesses ρ₁ ⊗ … ⊗ ρ_k with the *promise* that they are unentangled (product across the k parts); the verifier may apply a global joint measurement. The problem: **is QMA(2) = QMA?** I.e., does the unentanglement promise give the verifier strictly more power? It is known that QMA(k) = QMA(2) for k = poly(n) up to modest parameter losses (Harrow–Montanaro), so the two-witness question is the whole question. Known inclusions: QMA ⊆ QMA(2) ⊆ NEXP, and both containments are believed possibly strict (QMA(2) is not known to be in PSPACE). The problem is: prove QMA(2) = QMA (collapse), prove a separation (e.g., an oracle separation or an unconditional containment structure forcing strictness), or substantially improve the state of knowledge.

## Why does it matter?

It is arguably the most fundamental open question about the power of "unentanglement as a resource" in quantum verification. QMA(2) has surprisingly strong known capabilities — e.g., a 3-colorability protocol with witnesses of O(polylog n) qubits (Blier and Tapp; refined by Aaronson et al. to ~5 qubits per witness with higher soundness gap) — implying possible savings in witness size, relevant to quantum delegation/verification and quantum Napster scenarios. It also governs whether product-state tensor optimization problems (computing λ(A) = max_{⟨x|,|y⟩=1} |⟨x|⊗⟨y| A |x⟩⊗|y⟩|, the k=2 operator norm) admit efficient SDP-like approximations, connecting complexity to tensor algorithms.

## What's already known?

- **Reduction to two witnesses:** Harrow and Montanaro show QMA(k) = QMA(2) for any k ≤ poly(n), via a product test based on the de Finetti theorem / swap tests. So variants collapse to k=2.
- **Containments:** QMA ⊆ QMA(2) ⊆ NEXP (via the exponential-time verifier enumerating product witnesses, Kobayashi–Matsumoto for QMA(k)). QMA(2) is not known to lie in PSPACE, unlike QMA ⊆ PSPACE.
- **Upper bounds on protocols:** Blier–Tapp gave a QMA(2) protocol for 3-SAT/3-coloring with O(√n log n)-qubit witnesses; Aaronson, Drucker, and Blais gave a protocol for 3-SAT with two 5-qubit (constant-size) witnesses, completeness–soundness gap O(1/n³) — showing QMA(2) protocols can be extremely witness-efficient, but with tiny gaps and no known QMA-hardness amplification preserving witness size.
- **Tensor optimization:** the quantity λ(A) is NP-hard to compute/approximate (Harrow–Montanaro, building on Blier–Tapp/Aaronson et al.); related to the quantum separability problem, which is NP-hard and, per Gurvits, hard even to approximate.
- **What fails:** there is no known technique to simulate a QMA(2) verifier's measurement on product inputs with a single witness; conversely, no oracle separation between QMA and QMA(2) is known either direction (a relativized separation is itself open, verify current literature).

## What would count as solving it?

Any of the following would be major:
1. **Collapse:** QMA(2) ⊆ QMA (hence equality). A referee would want a full proof, likely including derandomization/parallelization of product tests.
2. **Separation:** an oracle O with QMA^O ⊊ QMA(2)^O, or an unconditional proof that some QMA(2) language is not in QMA (very unlikely with current tools).
3. **Structural progress:** QMA(2) ⊆ PSPACE, or QMA(2) ⊆ QMA[poly-log witness], or strong amplification for QMA(2) preserving total witness length.
4. **Lower-bound hardness transfer:** e.g., show QMA(2) contains NEXP-like classes or conversely that constant-witness-size QMA(2) with polynomial gaps is in QMA.

## How to start

1. Read Harlow... read **Harrow–Montanaro (arXiv:1001.0017)** thoroughly — Sections on the product test, QMA(k)=QMA(2), and hardness of λ(A); this defines the modern formulation. Then Aaronson–Drucker–Blais (arXiv:1008.1757, verify ID) for constant-size-witness protocols.
2. Try the "single witness simulation" route: understand why the verifier's entangled measurement across ρ₁⊗ρ₂ cannot be mimicked — the obstacle is that soundness relies on the product promise, which a single-witness QMA verifier cannot enforce.
3. Explore parallel repetition / gap amplification for QMA(2) with bounded witness size — the Aaronson et al. protocol's O(1/n³) gap is the bottleneck for unconditional statements.
4. Oracle-model attack: define oracle problems where the verifier requires two non-communicating queries to witnesses (cf. multi-prover games intuition, since QMA(2) ~ "quantum MIP with non-communicating Merlins sharing no entanglement").

## Key references

- A. W. Harrow, A. Montanaro, *Testing Product States, Quantum Merlin–Arthur Games and Tensor Optimization*, J. ACM 60(1), 2013; arXiv:1001.0017, DOI: 10.1145/2432622.2432625. Proves QMA(k)=QMA(2), gives an efficient product-state test, and shows NP-hardness of computing the 2-ingredient operator norm λ(A).
- S. Aaronson, A. Drucker, N. Blais, note on QMA(2) with small witnesses (arXiv:1008.1757 — verify identifier/authorship). Constructs a QMA(2) protocol for 3-SAT with two constant-size witnesses and inverse-polynomial gap.
- H. Kobayashi, K. Matsumoto, *Quantum multi-prover interactive proof systems with limited prior entanglement*, J. Comput. Syst. Sci. 66(3), 2003. Establishes QMA(k) ⊆ NEXP and the multi-watcher framework.
- R. Blier, A. Tapp, *All languages in NP have very short quantum proofs* (arXiv:0909.2090, verify). First QMA(2) protocol with O(polylog) qubits per witness for 3-SAT, with inverse-polynomial gap.
- L. Gurvits, *Classical deterministic complexity of Edmonds' problem and quantum entanglement*, STOC 2003. NP-hardness of separability, the root of hardness results for λ(A).

## Warnings

- The completeness/soundness gap matters: QMA(2) results with tiny gaps cannot be naively amplified because standard amplification increases witness size and destroys the constant-witness structure.
- QMA(2) soundness analysis must assume adversarial *entangled* states — only YES instances get the product promise. Many attempted protocols fail here (historically several claimed protocols were unsound).
- Do not conflate QMA(2) with MIP*: the Merlins in QMA(2) are honest-but-unentangled only on YES; QMA(2) ≠ quantum multiprover proof systems with entangled provers (MIP* = RE, unrelated collapse).
- "QMA(2) = QMA" is open in the *unrelativized* setting; oracle results in either direction are also open as far as this brief's sources record (verify).

---
*`ALGO-000190` · unverified*

## Acceptance guidance

Any of the following would be major:
1. **Collapse:** QMA(2) ⊆ QMA (hence equality). A referee would want a full proof, likely including derandomization/parallelization of product tests.
2. **Separation:** an oracle O with QMA^O ⊊ QMA(2)^O, or an unconditional proof that some QMA(2) language is not in QMA (very unlikely with current tools).
3. **Structural progress:** QMA(2) ⊆ PSPACE, or QMA(2) ⊆ QMA[poly-log witness], or strong amplification for QMA(2) preserving total witness length.
4. **Lower-bound hardness transfer:** e.g., show QMA(2) contains NEXP-like classes or conversely that constant-witness-size QMA(2) with polynomial gaps is in QMA.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/898c88d4-b84a-42a4-a706-e186c369ec37?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000190.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000190)
