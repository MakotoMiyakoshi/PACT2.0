# PACT2.0 — Pre-development literature synthesis (2026-11-19)

**Scope:** 24-paper reading list in [LITERATURE_READING_LIST.md](LITERATURE_READING_LIST.md). Twenty-two PDFs were present in the project's uploaded Sources. The two unmounted titles (Theiler et al. 1992; Kriegeskorte et al. 2009) were checked from publicly accessible full-text copies / author versions online. Huber 1964 is an image-only scan, so assessment emphasizes its foundational formulation rather than machine-searchable detail. This synthesis distinguishes **published findings**, **methodological implications**, and **new PACT2.0 hypotheses**. No new numerical experiments have yet been run.

## Working scientific judgement

**Owner's design charter (2026-11-19): HAS is the identity of PACT. PACT2.0 is a sensitivity-first evolutionary generalization of HAS, not a generic highly conservative robust PAC estimator.** The goal is to preserve preferential sensitivity to rare, high-amplitude phase-locked bursts while making the selection/inference statistically legitimate and integrating HAS into established PAC estimators. A non-dominated **high-sensitivity region** of a rigorously measured, scenario-conditional sensitivity versus physiological-artifact-robustness Pareto frontier is the success target; superior robustness on every case is not required. Statistical Type I calibration is non-negotiable and distinct from artifact-induced physiological misinterpretation.

The nontrivial aim is **not** simply to remove the upper-tail threshold, use ranks, use a median, or calculate a KL divergence: versions of all these ingredients are already available. The worthwhile question is whether the central HAS idea of prioritizing rare high-amplitude events can be incorporated into an interpretable rank-resolved model that retains genuine sparse-burst sensitivity while reporting its tradeoff against plausible artifact nulls, without imposing an arbitrary universal physiological cutoff.

Rank is a deterministic transform of amplitude. An estimator cannot simultaneously be invariant under *every* strictly increasing transformation of amplitude and recover information about the size of amplitude gaps: such transformations preserve rank and can arbitrarily change gaps. Choose precisely what invariance (e.g., positive scaling) and magnitude sensitivity are desirable.

The distinction between **statistical phase–amplitude dependence** and **interactions of two independently generated physiological oscillations** is non-negotiable. Any statistic of the same observed (A, phase) joint distribution is incapable of distinguishing generative mechanisms that produce that same distribution.

## 1. Historical development

| Era | Reference IDs | Main advance; limitation exposed |
|---|---|---|
| 1964–1992 | P12 Huber 1964; P13 Hampel 1974; P11 Koenker & Bassett 1978; P14 Theiler 1992 | Robust M-estimation and its efficiency–outlier tradeoff; influence curves and conditional quantiles; generative-null surrogate testing. These tools predate PAC. |
| 2006–2010 | P01 Canolty 2006; P20 Kramer et al. 2008; P02 Tort 2010; P24 Maris & Oostenveld 2007; P15 Kriegeskorte et al. 2009 | Phase-weighted complex-vector PAC, recognition that sharp edges generate spurious coupling, phase-bin KL score, permutation and max/cluster inference, warnings about post-selection testing. |
| 2013–2016 | P03 Miyakoshi et al. 2013; P16 Dvorak & Fenton 2014; P21 Aru et al. 2015; P05 van Driel et al. 2015; P22 Lozano-Soldevilla et al. 2016; P19 Minsker 2015 | Historical HAS acknowledges fixed-percentile selection irrespective of genuine HFO presence; oscillation-triggered event analysis; amplitude-filter bandwidth and window requirements; phase-clustering debias; one non-sinusoidal oscillator creates harmonic PAC; geometric-median robust aggregation. |
| 2017–2021 | P06 Ince et al. 2017; P17 Hülsemann et al. 2019; P07 Combrisson et al. 2020; P04 Miyakoshi et al. 2021 | Gaussian-copula rank MI and gcPAC; systematic method simulation; a real scalp EEG case showing artifact cleaning changes classification; still no universally superior estimator or universally valid surrogate. |
| 2023–2026 | P23 Wodeyar et al. 2023; P08 Perley & Coleman 2024; P09 Perley & Coleman 2026; P10 Rivest 2026 | Phase uncertainty/model dependence; Gamma GLM for amplitude given phase with GOF and MDL; dynamic state-space MI with approximate uncertainty; rigorous circular–linear rank correlation/circula statistics. |

### Historical PACT-specific insight (P03)
The 2013 PACT paper's *Limitations* explicitly states that the selected highest-amplitude percentage does not depend on whether genuine HFO events are present. It separately states that significant MI need not imply pathological tissue, and that better inferential statistics for phase-sorted amplitude may exist. The 2021 scalp EEG application (P04) used the highest 2% gamma amplitude samples; sleep classification AUC was >0.98 in all cleaning conditions, but waking AUC reached approximately 0.845 only after stringent ICA/ASR cleaning. This is evidence that artifact handling matters; it is not evidence that 2% is a universally optimal tail threshold.

## 2. Problems addressed or technically solvable

**(a) PAC can be defined through explicit estimands.** Canolty's complex resultant measures a first circular harmonic weighted by amplitude (P01); Tort's phase-bin KL compares normalized phase-specific mean-amplitude profiles to uniform (P02). Both are validly defined *descriptive statistics*, not universal measures of physiological interaction. The first can cancel under biphasic coupling. Tort MI is a KL of normalized mean amplitudes and is **not** identical to the full mutual information I(A;phi).

**(b) Phase marginal clustering has a known partial correction.** van Driel et al. (P05) gave dPAC by subtracting the mean phase phasor before forming amplitude-weighted coupling. The paper's Fig. 3 and simulated/empirical comparisons show phase clustering distorting uncorrected PAC; debiasing reduces this. This does not remove sharp transients, harmonic PAC, or shared event-locking.

**(c) Important filter-design constraints are characterized.** Dvorak & Fenton (P16) showed that an amplitude-filter passband must accommodate modulation sidebands (in their standard setting, at least twice the modulating frequency); the phase band should isolate a meaningful rhythm. Their roughly 10 s guideline was specific to their simulated/recorded scenarios, not a universal law. Aru et al. (P21) explain the necessity of peaks, suitable sidebands, edge guards, and checks on instantaneous phase progression.

**(d) Nonparametric correction of a defined search family is available in principle.** Maris & Oostenveld (P24) established rigorous randomization and max/cluster-statistic logic under relevant exchangeability. Kriegeskorte et al. (P15) showed that selecting parameter combinations on the same data can invalidate inference even when the downstream statistical procedure appears correct. A valid null must reproduce the full adaptive search.

**(e) Rank-based and full conditional-distribution approaches exist.** Ince et al. (P06) derive efficient Gaussian-copula MI estimation on rank-normalized margins; Combrisson et al. (P07) implement gcPAC with amplitude ranks and (sin(phi),cos(phi)). Perley & Coleman (P08) fit Gamma GLMs for f(A|phi), evaluate GOF and model order, and estimate MI; P09 extends to a time-varying latent state with Laplace-based uncertainty. Rivest (P10) provides circular–linear rank-dependence measures and asymptotic results. None obviates validation of neural-phase estimation or mechanistic confounds.

**(f) A framework for quantifying robustness exists.** Huber (P12) provides the M-estimation tradeoff; Hampel (P13) formalizes infinitesimal contamination response through the influence function; Koenker & Bassett (P11) generalize the median to conditional quantiles; Minsker (P19) derives performance properties of geometric medians of sufficiently independent weakly concentrated estimators. The theory does not automatically transfer to temporally dependent, burst-dominated EEG blocks.

**(g) Distinct estimator response patterns are measured.** Hülsemann et al. (P17) report that MVL is sensitive to monophasic coupling strength/width whereas Tort MI and GLM-CFC detect biphasic coupling, with MI comparatively less influenced by tested nuisance factors. These conclusions are *conditional on their synthetic models*, not a universal ranking.

## 3. Unresolved problems

1. **Identifiability of genuine cross-frequency mechanism.** Sharp edges (Kramer, P20), nonsinusoidal rhythmic harmonics (Lozano-Soldevilla, P22) and common nonstationary input (Aru, P21) can generate genuine statistical dependence without interaction between two independent rhythms. A purely bivariate A–phi estimator cannot generally decide physiology from its value.
2. **Tail structure versus robust estimation.** Unbounded amplitude weights are sensitive to a single extreme observation. All-rank statistics are insensitive to monotone amplitude transformations, but can lose magnitude information. Aggressive capping or medians can eliminate the *true* rare bursts PACT originally targeted. Robustness and power must be examined jointly at matched Type I error.
3. **Information discarded by Gaussian-copula approximation.** Ince et al. (P06) explicitly show that nonlinear/non-Gaussian dependencies may be underrepresented by GCMI (even report zero where true MI is positive); tail dependence is one possible failure. Whether a new robust rank–magnitude estimator improves this is *unproved*.
4. **Phase is model-dependent, not a perfectly observed variable.** Wodeyar et al. (P23) compare FIR-Hilbert, state-space and Poincaré phase. High confidence is not a guarantee of correct phase for a sharp transient. Data-censoring by uncertainty also creates an analysis selection problem.
5. **Correct null for autocorrelated and nonstationary signals.** Theiler (P14) defines surrogate validity relative to the exact null. Aru (P21) warns that real PAC alternatives are often generated with correlated nonstationarity. Simple single-sample phase permutation destroys serial structure; generic time shifts, rotations and sign-flips each require their own model assumptions.
6. **Statistical testing versus event confounds.** Event-locked phase and HFO amplitude may change together without ongoing oscillatory modulation. Single-trial, between-trial, and event-locked nulls are not interchangeable.
7. **Finite-sample effects and effective N.** Low HAS rate, strong temporal autocorrelation, long bursts, few independent cycles or blocks, binning and large frequency grids can make estimates unstable. Nominal sample count cannot be substituted for independent events.
8. **Hyperparameter/search multiplicity.** Percentile q, rank kernel bandwidth, gap saturation scale, phase-bin count, harmonics, frequency bands, time windows, channels, and comparison conditions all contribute selection; channel-only correction is inadequate for exploratory rank–frequency tuning.
9. **Effect-size comparability.** Raw vector-length PAC changes with amplitude scale and phase marginal; normalized, MI-based, and copula-based scores target different functionals. A standardized null score may help calibration but does not make distinct estimands interchangeable.
10. **Dynamic uncertainty and model assumptions.** Perley & Coleman (P09) achieve dynamic inference but acknowledge acausal smoothing, approximate latent-state posterior uncertainty, fixed harmonic order and unresolved hyperparameter uncertainty. The static Gamma GLM (P08) can still detect spurious non-sinusoidal effects.
11. **Artifact resistance in scalp EEG.** Artifacts can co-vary across bands through the same physical transient. P04 shows aggressive cleaning was decisive for awake scalp EEG classification; a robust statistic alone is no replacement for source/quality controls.
12. **Methodological novelty.** Rank dependence (P06, P07, P10), amplitude conditional distributions (P08, P09), phase debias (P05), event-level analysis (P16), and robust medians/quantiles (P11–P13, P19) are already published. A new combination must be shown to solve an identified failure mode that they do not.

## 4. Methods or practices to retire as *standalone evidence* (not blanket abandonment)

| Practice | Decision for PACT2.0 | Reason / source |
|---|---|---|
| Uncorrected raw Canolty vector magnitude as standalone evidence | **Demote to baseline descriptive outcome** | Scales with amplitude, phase-clustering bias, misses some multimodal effects (P01, P05, P17). |
| Fixed 1%, 2%, or 5% highest-amplitude cutoff asserted to identify genuine HFOs | **Discard as universal assumption; retain a benchmark** | Historical HAS limitation explicitly documented (P03); q is a modeling choice, not a physiological boundary. |
| Arbitrary sample-by-sample phase reshuffling for PAC significance | **Reject without a matching independent/exchangeable null** | Eliminates autocorrelation and burst structure; surrogate tests are model-conditional (P14, P21, P24). |
| A very narrow high-frequency filter that drops amplitude sidebands | **Reject if transfer function does not cover modulation** | P16 and P21 demonstrate the signal-processing problem. |
| First-harmonic resultant as the only PAC descriptor | **Discard as universal test, retain under monophasic alternative** | Biphasic phase dependence can cancel (P02, P17). |
| Hard-coding equal phase-bin occupancy or a uniform phase null without checking | **Reject** | Phase clustering and event locking invalidate naive assumptions (P05, P21). |
| Treating a significant cluster/bin as spatially or rank-localized proof | **Reject as an inferential overinterpretation** | Max/cluster tests control global false positives, not every claim about exact effect boundaries (P24). |
| Claiming Gaussian-copula MI is the true MI for any nonlinear/tail-dependent copula | **Reject**, but **retain gcPAC as essential baseline** | It is generally a lower bound and can miss a non-Gaussian dependence pattern (P06). |
| Treating a statistically significant PAC as proof of distinct physiological oscillators or causal communication | **Reject** | Sharp edges, harmonics, common input, and nonstationary evoked structure (P20–P22). |
| Optimizing estimator or phase method on the observed coupling and testing the winner as predeclared | **Reject unless nested in null or held out** | Selection dependence and double dipping (P15, P23). |

No paper establishes that all event-thresholding, all MVL, all Tort MI, or all conventional surrogate methods should be abandoned. Use appropriate baseline methods under their stated assumptions.

## 5. Publication-critical requirements (PACT2.0 scientific gate)

### P0: necessary before claiming calibrated inference

1. **Explicit estimand(s) and hypotheses.** Write separately what the proposed estimator measures: first-harmonic amplitude-weighted dependence, all-shape rank–phase dependence, or rank- and magnitude-sensitive tail structure. State if magnitude normalization should be invariant under global scaling and why. Document all tuning constants before examining target data.
2. **Exact algebra, symmetry and corner cases.** Verify the rank–amplitude Abel/summation-by-parts identity
   `mean(A.*z)-mean(A)*mean(z)=sum_r (A_(r)-A_(r+1))*D_r`,
   `D_r=(1/N)*sum_{i<=r}(z_(i)-mean(z))`, `z=e^(i*phi)`.
   State how ties, constant amplitude, phase-bin occupancy, zero weights, rare bursts and nonuniform phase are handled. This identity is algebraically correct but neither novel as a general identity nor proof that any chosen weight is robust.
3. **Two different null questions.** (i) statistical independence of A and phi, possibly conditional on data structure; (ii) absence of interaction of *separate oscillatory generators*. They are different scientific hypotheses; successful control of (i) does not imply mechanistic specificity under (ii).
4. **Valid empirical Type I calibration.** Simulate independent but autocorrelated LFO/HFO, nonuniform phase, 1/f noise, long burst envelopes, discontinuities and boundaries, event-locked inputs, nonsinusoidal single oscillators and broadband sharp edges. For each, report rejection rate with binomial CI versus nominal alpha and note if the case is a statistical or physiological null.
5. **Surrogate justified by invariances.** Preserve null-relevant time structure, segment boundaries and event design; regenerate the entire tested statistic, including rank, adaptive weights and phase/frequency selection when needed. No simple permutation/sign-flip/rotation automatically satisfies this.
6. **Full selection correction.** Correct across rank windows, phase frequencies, amplitude frequencies, channels, window times, harmonics and hyperparameter choices *actually searched*. Use global max-statistics or prespecified nested holdout. If an optimization objective uses phase information, it must be repeated inside each surrogate.
7. **Signal-processing audit.** Explicit FIR/Wavelet responses and amplitude sidebands; LFO peak evidence; phase monotonicity/uncertainty, filter edges and boundaries; test against phase estimation alternatives, and event-related confounds.
8. **Compare fairly at equal alpha.** Essential baselines: conventional HAS-Canolty, unconditional Canolty, van Driel dPAC, Tort KL, gcPAC and a simple rank-only circular-linear statistic; Gamma-GLM MI as a stronger distributional baseline if feasible. Validate the baselines' null procedures as carefully as those of the new method.
9. **Reproducibility.** Fixed random seeds, independent script execution, finite-sample controls, test vectors, documented parameter values and environment; match PACT2.0 TRACE-style p-numbered directory constraints.

### P1: essential to sustain a claim of improvement

1. **Power–robustness frontier:** matched-alpha detection power versus contamination fraction (e.g., 0–5%), artifact amplitude, burst occupancy and true-burst strength; display both gross errors and genuine extreme events. Quantify influence or empirically bounded sensitivity, not merely a lower observed maximum.
2. **Different coupling motifs:** sustained sinusoidal, highly sparse bursts, nonmonotonic mid-rank-only, phase-bimodal, time-varying preferred phase, amplitude shift/gain changes, different carrier amplitudes.
3. **Uncertainty and effective sample size:** cycle/block/trial-level CI or supported resampling; document how dependence affects effective N, especially in upper tails.
4. **Interpretability of rank geometry:** a rank-resolved PAC image/curve must have a physically interpretable region; a global p-value does not establish the exact rank interval is significant without local correction.
5. **Evidence of added value beyond rank-only or magnitude-only:** identify data-generating models where the hybrid captures a difference either comparator misses, while demonstrating it does not destroy true rare events.
6. **External robustness:** independent dataset / subject-wise held-out validation, preprocessing sensitivity, EMG/blink sensitivity, montage/source analysis when biological claims are made.
7. **Practical scalability:** sort `O(N log N)` once per channel/HFO band; efficient rank accumulations; realistic frequency-grid and surrogate costs; runtime and memory benchmarks.

### P2: later or application-dependent

- Dynamic state-space extension and real-time implementation are not mandatory for a paper focused on static rank geometry.
- Biophysical intervention and causal models are needed for strong mechanistic claims; they are **not** required if the paper explicitly positions the result as a statistical biomarker/estimator and validates its statistical scope.
- A new composite score is not scientifically compelling solely because its AUC is larger on one dataset; show calibration, estimand meaning and repeatability.

## Proposed *pre-coding* adjudication

Three estimands to compare on paper first:
- **Rank-only dependence** `I(rank(A); phi)` or a circular-integrated rank statistic: invariant to strictly increasing amplitude transforms; no magnitude information.
- **Magnitude-dependent conditional distribution** `I(A;phi)` / `f(A|phi)`: can represent tails, but vulnerable to parametric misspecification and finite-sample issues.
- **Hybrid rank–magnitude functional** of cumulative phase deviation and amplitude spacings: may preserve information about local amplitude gaps while bounding influence. Its benefits and influence function have **not been established**.

Do not prematurely accept the previously discussed local-median-of-rank-spacings + tanh saturation as the primary algorithm. Rank spacing is sample-size and density dependent; small spacings, ties and vanishing local scales create special cases. A bounded modification of gaps does not automatically confer a bounded influence function for the *full* estimator after sorting, adaptivity and normalization. Its ability to preserve sparse pathological HFO events is untested.

A useful analytic target is to derive **population-level functionals** indexed by amplitude quantile and circular phase, rather than define an ad hoc statistic directly on finite-sample gaps. Then prove/measure scale equivariance, point-contamination sensitivity, sensitivity to rare alternatives, and statistical calibration. Retain the rank-resolved curve as a diagnostic object even if a different global test is selected.

## Sources and accuracy

See [LITERATURE_READING_LIST.md](LITERATURE_READING_LIST.md) for the complete 24 bibliography items and DOIs. Specially decisive anchors:
- [Miyakoshi et al. 2013](https://doi.org/10.1109/EMBC.2013.6610242), Limitations: percentile selection regardless of HFO presence.
- [Dvorak & Fenton 2014](https://doi.org/10.1016/j.jneumeth.2014.01.002), Figs 2/4/5: filter sidebands, window length, event-level OTC.
- [Aru et al. 2015](https://doi.org/10.1016/j.conb.2014.08.002), pp. 58–60: physiological interpretation hierarchy and nine practical controls.
- [van Driel et al. 2015](https://doi.org/10.1016/j.jneumeth.2015.07.014), Fig 3 and eqs 9–10: phase clustering and dPAC.
- [Ince et al. 2017](https://doi.org/10.1002/hbm.23471), discussion on non-Gaussian copula and tail dependence: GCMI may underestimate.
- [Hülsemann et al. 2019](https://doi.org/10.3389/fnins.2019.00573), simulation-based monophasic/biphasic comparisons.
- [Combrisson et al. 2020](https://doi.org/10.1371/journal.pcbi.1008302), p. 7: rank-normalized amplitude and sine/cosine phase gcPAC.
- [Wodeyar et al. 2023](https://doi.org/10.1523/ENEURO.0507-22.2023), Discussion: uncertainty can be high even for wrong phase, beware selection by confidence.
- [Perley & Coleman 2024](https://doi.org/10.3389/fncom.2024.1392655), Gamma GLM with GOF and model selection; spurious PAC remains.
- [Perley & Coleman 2026](https://doi.org/10.1109/TBME.2026.3705664), limitations: acausal smoothing and incomplete hyperparameter uncertainty.
- [Rivest 2026](https://doi.org/10.1016/j.csda.2026.108449), circular–linear rank correlations and finite-sample conservativeness.
- [Theiler et al. 1992](https://doi.org/10.1016/0167-2789(92)90102-S), full text checked online rather than mounted PDF.
- [Kriegeskorte et al. 2009](https://doi.org/10.1038/nn.2303), full author text / PMC checked online rather than mounted PDF.

**State:** Literature review completed at the methodological synthesis level; no new estimator is validated. This document is a design gate, not an evidence claim that PACT2.0 surpasses prior work.
