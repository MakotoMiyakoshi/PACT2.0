# Nadalin et al. (2019) — Critical reading notes for PACT2.0

**Source**: Nadalin JK, Martinet LE, Blackwood EB, Lo MC, Widge AS, Cash SS, Eden UT, Kramer MA (2019). A statistical framework to assess cross-frequency coupling while accounting for confounding analysis effects. *eLife* 8:e44287. https://doi.org/10.7554/eLife.44287. Uploaded 29-page PDF reviewed on 2026-11-19.

## Methods (source-derived)

- Response: high-frequency envelope `A_high`. Predictors: **low-frequency** phase `phi_low`, **low-frequency** amplitude `A_low`, and amplitude-by-phase interactions.
- Three Gamma GLMs: (i) `A_high | phi_low` (phase spline basis); (ii) `A_high | A_low` (intercept + linear amplitude); (iii) `A_high | phi_low,A_low` (phase splines + linear A_low + A_low*sin(phi_low) + A_low*cos(phi_low)). See pp. 3–5, Eqs 1–3.
- Preferred phase spline order fixed at ten control points, informed by AIC simulations comparing 4–30 nodes (pp. 3–5, Fig. 2).
- The full model and reduced model are evaluated as predicted mean-response surfaces over 100 phase values and 640 values of `A_low` spanning its **5th–95th percentiles** (p. 6). This truncates only the range used to assess a *predictor* for the R statistics; it is not a highest-HFO-amplitude sampling procedure.
- `R_PAC = max_{A_low,phi_low} abs(1 - S_A_low / S_A_low,phi_low)` (p. 7 Eq. 4); the analogous `R_AAC` is maximum relative difference between phase-only and combined surfaces (Eq. 5). These scores represent global maximum predicted surface differences, not rank statistics or GLM goodness of fit.
- Parametric coefficient-resampling bootstrap (10,000 draws) for confidence intervals; AAFT resampling of `V_high` (1,000 surrogates) for p-values, with same procedure used for Tort MI comparison (pp. 7–8). AAFT is a model-conditional surrogate and not automatically valid under nonstationarity, condition changes, or sharp transients.
- 4–7 Hz `V_low`, 100–140 Hz `V_high`; linear-phase FIR plus Hilbert phase and envelopes (p. 3).
- MATLAB `fitglm`; public code https://github.com/Eden-Kramer-Lab/GLM-CFC (p. 10). Do not import into the PACT2.0 code/external directory without selecting an exact pinned version and ensuring compatibility with project rules.

## Results (source-derived)

| Simulation setting | R_PAC | Tort MI | Source |
|---|---:|---:|---|
| No PAC or AAC; 1000 null 20-s pink-noise simulations | 0.6% nominal-positive PAC | no matched numeric MI null in that paragraph | p. 10, Fig. 5 |
| Ordinary induced PAC, IPAC=1; 1000 20-s trials | 96.5% PAC detected | not directly paired in that case | p. 10 |
| Very weak ordinary PAC, IPAC <=0.3 | less sensitive | more sensitive | p. 12, Fig. 6 |
| No PAC, severe low-frequency amplitude step + AAC; 1000 200-s simulations | 0.4% nominal-positive PAC | 34.3% nominal-positive PAC | pp. 13–14, Fig. 7 discussion |
| Sparse coupling only for the **top 5% of low-frequency wave peaks** | 72% detected | 37% detected | p. 15, Fig. 8 |
| Phase-locked high-frequency amplitude *enhanced* during high A_low and *suppressed* during lower A_low | 96% detected | 58% detected | p. 15–16, Fig. 9 |

The original paper reports that ordinary `chi2` nested GLM comparisons yielded apparent PAC in **59.7%** of null simulations, and AIC selected the fuller model in **98.6%**; this must not be confused with failure of all GLMs or all likelihood-ratio inference. The failure is demonstrated **in the authors' autocorrelated time-series simulation and their testing strategy**. p. 10, Fig. 5.

## Scientific interpretation and corrections

**Critical distinction:** Nadalin's sparse simulation gates coupling on **low-frequency oscillation peak amplitude** `A_low`; PACT's HAS selects observations by **high-frequency/HFO amplitude** `A_high`. These are not equivalent and the reported 72% vs 37% result does not demonstrate superiority for HAS-style HFO-tail coupling.

Nadalin evaluates whether phase adds predictive information after conditioning on `A_low`. Their formulation is an important *confound-adjustment comparator* but **does not characterize an upper-tail profile of `A_high` versus phase**, does not scan a HAS sampling proportion, and does not define a Pareto frontier.

**Especially relevant:** Maximum difference across fitted model surfaces is a proper feature of Nadalin's statistic. PACT2.0's proposed *maximum over a HAS-rate/frequency field* is a distinct search domain. The resulting adaptive selection must enter the null calibration regardless of how appealing its sensitivity-first aim is.

**Important limitation:** A conditional *mean* Gamma GLM with a single modeled Gamma shape need not detect tail-only changes that leave means similar. The published paper has not shown that a proposed conditional upper-quantile/upper-tail PAC would outperform its method.

## Limitations acknowledged by the authors (p. 23)

1. Phase spline basis may fit rapidly varying coupling poorly.
2. R scores depend on the analyzed `A_low` range, mitigated by restricting surface evaluation to 5–95th percentiles.
3. Frequency bands must be chosen ahead of computing R or an expensive scan performed.
4. Assumes approximately sinusoidal isolated components; nonsinusoidal confounds are not removed. Additional sharp-change predictors are suggested.
5. Synthetic generative models may lack the complexity and latent confounders of in-vivo neural signals.

They also note standard nested-model tests can be more powerful but yield many false positives *in their setting*.

## PACT2.0 research consequences (proposal, not findings in Nadalin)

- Keep **HAS identity**: high sensitivity to true rare **high-frequency amplitude** PAC bursts.
- Use Nadalin's `R_PAC` as a methodological comparator when feasible, especially under LFO amplitude changes and AAC, not as a synonym for HAS.
- Potential adaptation: scan *conditional upper-quantile effects* of `A_high` on LFO phase while controlling `A_low`. Quantile regression, censored/tail likelihood, and upper-exceedance approaches are **unvalidated hypotheses**, not methods endorsed by Nadalin.
- DO NOT use `rank(A_high)` as an ordinary predictor of its own response `A_high` in a GLM; that would be a deterministic response leakage. Rank/tail-index can instead define a candidate estimand, score, or response distribution.
- At nominally calibrated statistical Type I error, compare genuine sparse PAC sensitivity against physiological/artifact false-positive resistance on **scenario-conditional Pareto frontiers**. Report uncertainty on both axes. This paper illustrates scenario reversals, not a pre-established PACT2.0 frontier.
- Validate the **entire HAS-percentage/frequency-field adaptive search** under the appropriate null; randomization preserving only spectrum/amplitude marginal is not always sufficient for highly nonstationary EEG.

**Status:** literature note only. No algorithm built, no simulations run, and no validation claimed.
