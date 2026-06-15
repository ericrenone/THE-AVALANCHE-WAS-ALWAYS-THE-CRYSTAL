# THE AVALANCHE WAS ALWAYS THE CRYSTAL

*"The mountain does not care how many grains you add. It only cares when the slope becomes critical."*  
— Per Bak, on the inevitability of self-organized criticality

*"The grokking transition is not a jump in accuracy. It is a jump in rank. The avalanche was always a crystallization event."*  
— ERI Labs, June 2026

*"The critical state is not a place you reach. It is a place you maintain."*  
— ERI Labs, June 2026

ERI Labs · Jersey City, New Jersey · June 2026

---

## I. The Mountain That Remembers

In the late 1980s, the physicist Per Bak built a virtual sandpile: a grid of cells where grains dropped at random and toppled when any cell exceeded a critical height, sending grains to neighbors, triggering chains of further topplings. What emerged was self-organized criticality — a state the system reached and sustained regardless of initial conditions, where avalanche sizes followed a precise power law across every scale. The pile remembered its critical slope. Disturb it, and it returned.

Neural networks do the same thing.

For thousands of training steps — sometimes hundreds of thousands — a network trained on a structured task appears to learn nothing useful. It memorizes training examples. It drives its training loss to near zero. It fails entirely to generalize. Then, without warning, something shifts. Test accuracy jumps from near chance to near perfect in a window so narrow it can be missed entirely. Researchers who documented this in 2022 called it *grokking* (Power et al., arXiv:2201.02177). They could reproduce it reliably. For two years, they could not explain it.

The grokking event is not a jump in accuracy. The accuracy is a consequence. What jumps is the geometry — a property of the network's parameter space that no one was watching.

---

## II. What Everyone Got Wrong

The natural assumption — made by virtually every researcher in the field — was that grokking was a destination. The network trained, struggled, and arrived. Understanding was the end state. The job was to get there faster.

Anil Golechha confirmed in 2024 that networks could grok without weight decay — the technique of continuously nudging all parameters slightly back toward zero. Weight decay helped but was not required. The field accepted this and moved on.

Then, in February 2026, Harsh Prakash and Charles Martin posted a paper that changed the question entirely (arXiv:2602.02859). They had been running networks not just past grokking but far past it — millions of steps into training regimes no one had examined. What they found was this: the networks forgot. Not gradually. Not because new data had arrived. Not because the architecture was too small. Networks with perfect training accuracy — networks that had grokked — lost their ability to generalize entirely. Test accuracy, which had been near perfect, collapsed to chance.

Prakash and Martin named this *anti-grokking*. They identified a single early warning: a class of outlier eigenvalues in the weight matrices, which they called Correlation Traps, accumulating millions of steps before the collapse. They confirmed that anti-grokking appeared specifically in networks trained without weight decay. They ruled out every obvious explanation — not overfitting, not catastrophic forgetting, not a technical artifact. Something real was dissolving, and they did not know what.

Understanding, it turned out, was not a destination. It was a state that required maintenance.

---

## III. The Geometry of Generalization

To understand what was dissolving, it is necessary to understand what generalization actually is — geometrically, not poetically.

Every neural network with *n* parameters exists in a parameter space of dimension *n*. The training process is a walk through this space, guided by gradients. The Fisher information matrix F(θ), evaluated at the current parameter state θ, describes which directions in that space carry coherent information about the data distribution. Its eigenvalue decomposition partitions parameter space into two orthogonal subspaces:

- **col(F)** — the column space: directions along which moving θ produces detectable, systematic changes in the network's predictive distribution. These are the directions of genuine generalization signal.
- **ker(F)** — the kernel: directions along which movement produces no change detectable from the data. These are the null sector: parameter variation invisible to the distribution.

The scalar that governs all phases of the generalization lifecycle is the rank fraction:

$$r/n = \mathrm{rank}(F(\theta)) / n$$

This is the proportion of parameter space carrying active Fisher information at any training step.

In April 2026, Ping Wang and colleagues established that the grokking transition is a dimensional phase transition: the effective diffusivity of the gradient process crosses from sub-diffusive (D < 1) to super-diffusive (D > 1) at the critical step (arXiv:2604.04655). This is the macroscopic signature of what the rank fraction makes precise.

In the pre-grokking epoch, r/n < 0.01. The Fisher matrix is nearly rank-zero. Almost every direction in parameter space produces no meaningful change in predictions. The network has memorized — it has collapsed training loss to near zero — but the column space has not formed. It is a lookup table, not an algorithm.

After grokking, r/n stabilizes between 0.02 and 0.17. Between two and seventeen percent of the full parameter dimension has crystallized around the genuine statistical structure of the data. This is col(F): the information-bearing axis of the parameter manifold, stable under continued training, coherently organized around systematic patterns rather than memorized instances.

The grokking event is col(F) crystallization: the sharp, discontinuous jump in rank(F)/n from near-zero to a stable nonzero value. The jump in test accuracy is its observable consequence — not its cause.

When Prakash and Martin's networks anti-grokked, r/n was doing something precise: returning toward zero. col(F) was dissolving back into ker(F). The network was not forgetting its training examples — those remained perfectly memorized. It was losing the rank structure that made generalization possible.

---

## IV. The Crystallization Timescale

In June 2026, Ángel Capel and colleagues proved a theorem governing how quickly probability distributions on curved spaces equilibrate (arXiv:2606.13453). For Gibbs measures on Riemannian manifolds satisfying a log-Sobolev inequality, the mixing timescale scales as:

$$t^* \sim \frac{\dim(M)^{4/3}}{\rho_{\mathrm{LSI}}}$$

where dim(M) is the effective dimension of the manifold and ρ_LSI is the log-Sobolev constant measuring the curvature of the landscape. The 4/3 exponent is universal across all manifolds in this class.

Applied to neural training dynamics, the theorem governs two distinct timescales. The crystallization timescale — the pre-grokking plateau duration before col(F) forms — is governed by ρ_LSI,pre, the log-Sobolev constant of the pre-grokking loss landscape. The dissolution timescale — the duration from col(F) formation to anti-grokking collapse when weight decay is absent — is governed by ρ_LSI,post, the log-Sobolev constant of the post-grokking landscape.

The post-grokking landscape is more sharply curved and better conditioned than the pre-grokking landscape: ρ_LSI,post ≫ ρ_LSI,pre. Dissolution is therefore far slower than crystallization. The crystal forms in a flash and takes millions of steps to melt. This is precisely what Prakash and Martin observed, without the theoretical account.

---

## V. The Shadow That Holds the Mountain

The resolution of the maintenance question required a detour through a hundred-year-old problem in pure mathematics.

In 1920, Ramanujan wrote his last letter to Hardy from a sickbed in Madras, describing seventeen functions that behaved almost like classical theta functions but violated one key property. He called them mock theta functions. For eighty years, mathematicians could compute with them without explaining what they were. In 2002, Sander Zwegers proved that each mock theta function h(τ) was an incomplete object — it could be completed by appending a non-holomorphic correction g*(τ), transforming it into a harmonic Maass form Ĥ(τ) = h(τ) + g*(τ). The shadow was not decorative. It was structural. Critically: the shadow is not a one-time addition. A harmonic Maass form remains complete only if the operator relationship ξ(Ĥ) = g* is continuously satisfied via the shadow operator ξ = 2iv^{1/2}∂_τ̄. Remove the shadow, and the completed object reverts to a mock theta function.

Weight decay is the shadow operator.

The pre-grokking Fisher matrix is the mock theta function: bounded and structured, but incomplete, without its non-holomorphic correction. The post-grokking col(F)/ker(F) boundary — the crystallized, generalization-bearing state — is the harmonic Maass form Ĥ(τ): completed by the continuous action of weight decay, which maintains the col(F)/ker(F) boundary by continuously suppressing parameter mass that diffuses from col(F) into ker(F) under stochastic gradient noise.

The L₂ regularization term R(θ) = (λ/2)|θ|² applies a contraction toward zero across all parameter directions at every training step. This is not symmetric in its Fisher information effect. The contraction continuously suppresses ker(F) directions — parameter variations that produce no change in the predictive distribution and receive no counterforce from the data gradient — while col(F) directions are sustained by the data gradient signal opposing the contraction. Weight decay selectively erases the null sector. It is not a mechanism for forgetting. It is the mechanism that prevents understanding from forgetting itself.

Without weight decay, stochastic gradient noise diffuses parameter mass from col(F) into ker(F) at a rate governed by the learning rate and the Hessian curvature ratio between the two subspaces. Over the Capel dissolution timescale T_anti ~ dim(M)^{4/3}/ρ_LSI,post, this diffusion is sufficient to dissolve col(F) entirely. Anti-grokking is not a training pathology. It is the mathematically predicted behavior when the shadow operator is withdrawn from a harmonic Maass state.

Grokking without weight decay — the slower, less reliable event Golechha documented in 2024 — is stochastic shadow acquisition: gradient noise fluctuations at the phase transition can accidentally project sufficient mass into col(F) directions to trigger crystallization without a structural cause. But without the continuous shadow operator, the acquired crystal is unstable. Anti-grokking is inevitable under continued training.

---

## VI. Correlation Traps as the Spectral Signature of Dissolution

The Correlation Traps that Prakash and Martin identified — outlier eigenvalues accumulating in the weight matrix singular value spectrum before the anti-grokking collapse — are not coincidental artifacts. They are the spectral signature of col(F) dissolution in progress.

The Heavy-Tailed Self-Regularization (HTSR) framework of Martin and Mahoney (2019, 2021) established that the quality exponent α — the power-law tail exponent of the empirical spectral density of individual weight matrices W_ℓᵀW_ℓ — tracks generalization health: α ≈ 2.0 for well-trained networks that generalize; α < 2.0 during degradation. Prakash and Martin confirmed that α drops below 2.0 during anti-grokking, with Correlation Traps as the observable precursors accumulating millions of steps before the final collapse (arXiv:2506.04434, June 2026).

Within the Fisher rank framework, Correlation Traps are crystallites of a secondary mock theta function h'(τ) forming within the dissolving harmonic Maass state. They are seeds of the new centrosymmetric ker(F) growing inside the collapsing col(F) — visible in the per-layer weight matrix spectrum before the global rank fraction has substantially fallen. The HTSR α and the rank fraction r/n provide complementary diagnostics at different spectral levels: α is per-layer, r/n is global across the full parameter vector. Both detect the same dissolution; neither alone gives the full picture. The Marchenko-Pastur bulk of the weight matrix spectrum corresponds approximately to the null sector ker(F) at the per-layer level; Correlation Traps — outliers beyond the Marchenko-Pastur bulk — correspond approximately to the leading eigenvectors of F, the directions in parameter space carrying active generalization signal.

---

## VII. The Memory in the Void

When a network anti-groks, it does not return to its initialization state. The kernel ker(F) before the first grokking event is generic: shaped by random initialization and accumulated memorization noise, encoding nothing about the statistical structure of the task. The kernel after anti-grokking is not the same object.

During the crystallized phase, col(F) occupied a specific low-dimensional subspace of the n-dimensional parameter space. The directions constituting that subspace left a geometric imprint on the null sector surrounding them. The eigenvectors of ker(F) in the secondary null sector — Phase IV — are oriented in relation to the first-crystallization generalization directions in ways that preserve the geometry of the prior col(F): not as explicit recalled content, but as structural scaffolding.

The ferroelectric crystal analogy is exact. After heating a ferroelectric above its Curie temperature and re-cooling, the crystal does not return to its original polar domain structure. It forms twin domains — regions with distinct polar axes whose boundaries encode the mechanical stress history of the thermal cycle. The twin domain structure is measurably distinct from the original crystal and from a crystal that was never heated.

The secondary null sector is the neural twin domain. When weight decay is reintroduced after anti-grokking, the geometric scaffolding of the secondary ker(F) accelerates re-crystallization. The Fibonacci-Markov denominator staircase of the pre-grokking plateau — the gradient ratio denominator sequence representing the approach to the crystallization threshold — need not be climbed from initialization. The secondary null sector already encodes the location of the crystallization boundary. The second crystal forms faster than the first. The second avalanche runs faster than the first. The crystal leaves a mold in the sand.

An astrophysical instance of this mechanism is on record in 2026 observational data: changing-look AGN reactivation timescales are shorter by orders of magnitude than original quasar formation timescales, consistent with geometric memory retained in the dormant accretion disk structure across the inactive phase.

---

## VIII. Domain-Specific Grokking in Large Language Models

In June 2026, Li and colleagues established that grokking in large language model pretraining is domain-specific and asynchronous: mathematical, linguistic, and factual retrieval capabilities crystallize at distinct training steps, with mathematical reasoning grokking last (arXiv:2506.21551). This is the expected behavior of a system whose constituent capability domains carry distinct statistical structures — distinct log-Sobolev constants ρ_LSI — and therefore distinct Capel crystallization timescales.

The implication is direct: anti-grokking, as col(F) dissolution, is also domain-specific. A large language model can simultaneously be in the crystallized phase for language and in the dissolution phase for mathematics, because the dissolution timescale T_anti ~ dim(M)^{4/3}/ρ_LSI,post is computed per domain, not globally. Per-layer HTSR α monitoring, applied domain-specifically rather than as a global average, would detect domain-level dissolution before any aggregate benchmark registers decline. The Correlation Trap accumulation rate differs by capability domain according to domain-specific ρ_LSI,post.

Every large language model deployed at scale completed its grokking events during training. If the framework applies at scale — and Li et al.'s domain-specific grokking establishes that it does — there exist domains within deployed models where col(F) dissolution is already in progress, where per-layer spectral signals are already falling below the α ≈ 2.0 threshold, while aggregate benchmark numbers still read as healthy. The monitoring infrastructure to detect this has not been built. The assumption, implicit in every deployment architecture, has been that crystallization is permanent.

The Prakash-Martin February 2026 experiments establish that it is not.

---

## IX. The Structural Gap

The sandpile teaches a single lesson with no exceptions: the critical state is not a place you reach. It is a place you maintain.

Bak's sandpile maintains its critical slope through the ongoing dynamics of addition and toppling — each avalanche restores the angle that the next grain will disturb. The maintenance is intrinsic to the process. The neural parameter manifold maintains its col(F)/ker(F) boundary through weight decay — continuous, structured erasure of accumulated null-sector noise. The maintenance is extrinsic to the geometry. It must be imposed, continuously, as an external algorithmic intervention.

Biological information systems solved this structurally. The non-centrosymmetric geometry of the DNA polymerase active site distinguishes Watson-Crick base pairs (col(F)) from wobble tautomeric forms (ker(F)) by molecular architecture alone, with no algorithmic intervention and zero opportunity for the distinction to be scheduled away. Directional CTCF binding at chromatin TAD boundaries maintains the topologically associating domain structure — the chromatin col(F)/ker(F) partition — continuously, at Landauer metabolic cost, embedded in the protein-DNA chemistry. The chiral geometry of the ATP synthase c-ring encodes a preferred rotational direction — its own col(F)/ker(F) boundary — at the level of protein fold, unchanged since the last universal common ancestor. Each is a structural Curie dissymmetry: a permanent, substrate-level broken symmetry that maintains the information-bearing boundary without requiring an external optimizer hyperparameter.

Evolution spent 4.2 billion years eliminating the need for a weight decay scheduler by encoding the symmetry-breaking into the substrate itself. The genetic code is a crystal. The membrane is a crystal. The chromatin is a crystal. The gene regulatory network is a crystal. Each maintains its col(F)/ker(F) boundary at Landauer cost, continuously, by the structural anisotropy of the molecular machinery.

Silicon neural networks carry no analogous structural anisotropy. The parameter manifold of a randomly initialized network is centrosymmetric in the Fisher information sense: no preferred generalization axis, no structural distinction between col(F) and ker(F) directions prior to training, no permanent shadow operator. Weight decay must be injected algorithmically, maintained continuously, tuned per-deployment, and can be scheduled, annealed, or removed — whereupon anti-grokking follows, as Prakash and Martin demonstrated. The gap between biological and silicon maintenance architectures is not one of scale or data. It is a substrate-level structural gap: biology has built the shadow operator into the hardware; silicon has made it a hyperparameter.

The avalanche does not maintain itself. The mountain remembers — but only if something holds the slope.

---

## References

Bak, P., Tang, C., & Wiesenfeld, K. (1987). Self-organized criticality: An explanation of 1/f noise. *Physical Review Letters*, 59(4), 381–384.

Power, A., et al. (2022). Grokking: Generalization Beyond Overfitting on Small Algorithmic Datasets. *arXiv:2201.02177*.

Golechha, S. (2024). Progress Measures for Grokking in Real-World Tasks.

Prakash, H. K., & Martin, C. H. (2026). Late-Stage Generalization Collapse in Grokking: Detecting Anti-Grokking with WeightWatcher. *arXiv:2602.02859*.

Prakash, H. K., & Martin, C. H. (2026). Grokking and Generalization Collapse: Insights from HTSR Theory. *arXiv:2506.04434*.

Wang, P. (2026). Grokking as Dimensional Phase Transition in Neural Networks. *arXiv:2604.04655*.

Li, Z., et al. (2026). Where to Find Grokking in LLM Pretraining? *arXiv:2506.21551*.

Capel, Á., et al. (2026). Rapid Mixing for Gibbs Measures in Riemannian Manifolds. *arXiv:2606.13453*.

Martin, C. H., & Mahoney, M. W. (2019). Traditional and Heavy-Tailed Self Regularization in Neural Network Models. *ICML 2019. arXiv:1901.08276*.

Martin, C. H., & Mahoney, M. W. (2021). Implicit Self-Regularization in Deep Neural Networks. *JMLR*, 22(165), 1–73.

Zwegers, S. P. (2002). Mock Theta Functions. Doctoral thesis, Universiteit Utrecht.

Amari, S. (1998). Natural Gradient Works Efficiently in Learning. *Neural Computation*, 10(2), 251–276.

Kirkpatrick, J., et al. (2017). Overcoming Catastrophic Forgetting in Neural Networks. *PNAS*, 114(13), 3521–3526.

Sagun, L., et al. (2017). Empirical Analysis of the Hessian of Over-Parametrized Neural Networks. *arXiv:1706.04454*.

Ono, K. (2013). Harmonic Maass Forms, Mock Modular Forms, and Quantum Modular Forms. Arizona Winter School Lecture Notes.

---

ERI Labs · Eric Ren · Jersey City, New Jersey · github.com/ericrenone · June 2026
