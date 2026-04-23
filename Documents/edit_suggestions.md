# MFO Synopsis — Edit Suggestions

## Factual Errors

**1. Wrong comparison algorithms (appears twice: Algorithm section and Results section)**
- Synopsis claims MFO is compared against PSO, GA, and **DE (Differential Evolution)**
- DE is never a comparison baseline in the paper — actual comparators are: PSO, GSA, BA, FPA, SMS, FA, GA
- Fix: replace DE with GSA (or list the full set)

**2. Missing test category: composite benchmark functions**
- Synopsis only mentions "unimodal and multimodal benchmark functions"
- Paper tests three categories: unimodal (F1–F7), multimodal (F8–F13), **and composite (F14–F19)**
- Fix: add composite functions to the description

**3. Engineering design problems completely omitted**
- Paper includes 9 constrained engineering problems (welded beam, gear train, truss, pressure vessel, etc.) and a marine propeller design problem — none are mentioned
- Fix: add a sentence acknowledging real-world engineering benchmarks

**4. "Swarm Intelligence" misclassification**
- Source calls MFO a "novel nature-inspired optimization paradigm" and a "population-based algorithm" — it does not label it Swarm Intelligence
- MFO is inspired by individual moth navigation, not collective swarm behaviour

**5. GA "sensitivity to parameter tuning" claim**
- Not stated in the source paper — unsupported

## Style / AI-Generated Phrases to Rewrite

- *"Exorbitant exploration leads to inefficiency"* — "exorbitant" is misused here
- *"It takes help from spiral-based movements"* — awkward phrasing; use "uses" or "employs"
- *"Structural weaknesses in existing algorithms gave way to a novel approach"* — generic filler, remove or replace
- *"I am confident that the methods used are reproducible..."* — first-person has no place in academic writing, remove
- *"In my opinion, the authors justified their claim..."* — same issue, rewrite in third person
- *"in a concrete manner"* — padding, cut it
- *"stable and smooth convergence"* — vague, unsupported by specific results

## Other

- Results section has no specific numbers (no p-values, no "best on X of Y functions") — add at least one concrete result from Tables 4–9
- Wilcoxon rank-sum test (used throughout the paper) is not mentioned — worth a brief reference
- Bullet list uses raw dashes (`-`) instead of a LaTeX `\begin{itemize}` environment — fix for consistency with the rest of the document

---

# PSO Synopsis — Edit Suggestions

*Source verified against: Kennedy & Eberhart (1995), "Particle Swarm Optimization," ICNN'95, pp. 1942–1948.*

## Factual Errors

**1. Author order in citation is reversed**
- Citation (line 202) lists "R. C. Eberhart and J. Kennedy" — Eberhart first
- Source paper header lists **James Kennedy** as first author, Russell Eberhart as second
- The inline text already correctly says "Kennedy and Eberhart"; the citation block should match
- Fix: change citation to `J.~Kennedy and R.~C.~Eberhart`

**2. Rastrigin and Rosenbrock not in source**
- Synopsis (line 260) states PSO was "validated on Schaffer's F6, Rastrigin, and Rosenbrock"
- Source (Section 5) tests only **Schaffer's f6** plus neural network training (XOR, Fisher Iris Data Set) — Rastrigin and Rosenbrock do not appear anywhere
- Fix: remove Rastrigin and Rosenbrock; keep only Schaffer's f6 and the NN training results

**3. Simulated annealing not in source**
- Synopsis uses SA as a motivating contrast in two places (lines 221 and 246): "simulated annealing maintained only a single candidate solution"
- SA is **not mentioned anywhere** in the source paper — the paper's only comparator is GAs
- Fix: remove SA entirely from the motivation and algorithm sections, or cite a separate external source

**4. Gradient-based solver motivation not in source**
- Synopsis (lines 217–218) frames PSO's gap as addressing "gradient-based solvers (Newton's method, conjugate gradient)"
- The source paper never mentions gradient methods, Newton's method, or conjugate gradient — the motivation is framed entirely around social simulation and comparison with GAs
- Fix: rewrite the motivation to match the source: PSO was developed from a social behaviour simulation, with GAs as the primary algorithmic comparator

**5. Velocity equation attributed to 1995 paper includes the 1998 inertia weight**
- The equation block (lines 235–240) includes $w\,\mathbf{v}_i$ (inertia term) as part of what "Kennedy and Eberhart proposed"
- The source's final simplified equation (Section 3.6) is: `vx = vx + 2*rand()*(pbest - x) + 2*rand()*(gbest - x)` — **no $w$ term**; the existing velocity is kept by addition, not by an explicit weight
- $w$ was introduced by Shi & Eberhart (1998), which the synopsis correctly cites as [7], but presenting the combined form as the original 1995 equation is misleading
- Fix: show the 1995 equation without $w$, then introduce $w$ separately as a 1998 extension; also clarify that the source uses a single constant (2) for both cognitive and social terms, not separate $c_1$ and $c_2$

**6. lbest topology is not in the ICNN'95 source paper**
- Synopsis (lines 250–253) describes the lbest neighbourhood topology as one of "two notable extensions developed from this base"
- The ICNN'95 source only describes the **GBEST model** — lbest with explicit neighbourhood sizes is from the companion paper (Eberhart & Kennedy, MHS'95, "A New Optimizer Using Particle Swarm Theory")
- Fix: cite the companion paper for lbest, or clearly attribute it to a separate source rather than implying it comes from the ICNN'95 paper

**7. "provides pseudocode" — source has no pseudocode**
- Synopsis (line 262) states "The paper provides pseudocode and explicit parameter settings"
- The source has **no pseudocode block** — it describes the algorithm in prose and provides the velocity update formula (Section 3.6); there is no step-by-step pseudocode listing
- Fix: change to "the paper provides the velocity update equation and parameter settings"

**8. "faster convergence" overstates the source result**
- Synopsis (line 261) claims PSO showed "faster convergence on several test cases" against GA
- Source (Section 5) says: *"appears to approximate the results reported for elementary genetic algorithms... in terms of the number of evaluations required"* — a deliberately modest claim of parity, not faster convergence
- Fix: replace "showing faster convergence" with "achieving comparable results to GA with similar evaluation budgets"

## LaTeX / Structural Issues

**9. Raw bracket citations `[2]`, `[4]`, `[7]` etc. instead of `\cite{}`**
- The entire PSO section uses literal text like `~[2]`, `~[4]`, `~[7]` instead of `\cite{kennedy1995}` etc.
- These render as plain text and do not link to the bibliography; bibliography entries won't be marked as cited
- Fix: replace all `[n]` inline citations in the PSO section with proper `\cite{key}` commands

**10. Duplicate `\bibitem` entries in bibliography**
- The following entries appear **twice** (once under "PSO references", again under "PSO refrences [sic]"): `kennedy1995`, `reynolds1987`, `shi1998`, `price2019`, `bayzidi2021`, `tzanetos2020`
- LaTeX will throw multiply-defined label errors
- Fix: remove the duplicate block (approximately lines 511–541)

**11. Duplicate Kennedy & Eberhart entry across sections**
- `\bibitem{kennedy1995pso}` (DA section) and `\bibitem{kennedy1995}` (PSO section) reference the same paper
- Fix: unify under one key (e.g. `kennedy1995pso`) used consistently across all sections

---

# GA Synopsis — Edit Suggestions

*No dedicated source file available. Verified against established GA literature: Holland (1975) and Goldberg (1989) as cited; factual claims checked against well-known properties of the algorithm.*

## Factual Errors

*No outright factual errors found.* All major claims — Holland as GA's originator, Goldberg's popularisation for engineering, selection/crossover/mutation as the three operators, the Schema Theorem and Building Block Hypothesis, De Jong's empirical analysis, and the standard weakness profile — are accurate and consistent with the cited sources.

## Logical / Coherence Issues

**1. `α_3` index in chromosome example is inconsistent**
- The chromosome on line 337 is written as `x = [w_1, w_2, w_3, d_1, d_2, d_3, α_3, …]`
- The weights `w_i` and window sizes `d_i` both start their index at 1; the EMA decay parameters jump straight to `α_3` with no `α_1` or `α_2`
- Fix: change to `α_1` (or write `α_1, α_2, α_3, …` to match the pattern of the other parameters)

**2. "LMA" is undefined and non-standard (line 378)**
- The text refers to "a good relative weighting between SMA, LMA, and EMA components"
- "LMA" is not a standard moving-average abbreviation (standard terms are SMA, EMA, WMA); a reader cannot infer what it means
- Fix: replace with a defined term or add a brief inline definition (e.g. "long-window MA (LMA)")

**3. No Free Lunch paragraph creates a false logical bridge (lines 315–319)**
- The paragraph moves from: NFL ("no optimiser is best on every problem") → "GA's answer is to keep diverse partial solutions alive long enough that useful building blocks can be recombined"
- NFL does not lead to the Building Block approach — NFL makes a general statement about all algorithms; Holland's building-block strategy predates NFL by 22 years and was motivated by biological evolution, not by NFL
- The current phrasing makes it seem like GA is a direct response to the NFL limitation, which is historically and logically backwards
- Fix: split into two separate points: (i) use NFL to justify why new algorithms are still worth exploring (as the DA and MFO sections do), then (ii) introduce the building-block motivation independently

## Style Issues

**4. First-person "My assessment" (line 407)**
- "My assessment is that GA is a strong baseline for the later implementation..."
- First-person assessment language is inconsistent with academic literature review style
- The same issue appears in the MFO synopsis ("In my opinion...") — both should be rewritten in third person

## Structural Note

**5. Dual primary source reduces specificity**
- The section cites two books as co-primary sources (Holland 1975 and Goldberg 1989) rather than a single paper, making it harder to tie specific claims to a specific source
- The Holland book covers GA theoretically; Goldberg covers practical optimisation — the synopsis could be clearer about which claims derive from which source (e.g., the Schema Theorem is Holland; the engineering benchmarking is Goldberg/De Jong)
