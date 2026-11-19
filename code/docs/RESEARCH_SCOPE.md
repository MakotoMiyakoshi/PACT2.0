# PACT2.0 — research scope and repository rules

Status: exploratory research design, 2026-11-19. No estimator has yet been validated.

## Research identity and objective — fixed by project owner, 2026-11-19

**Highest-Amplitude Sampling (HAS) is PACT's identity, not a disposable historical artifact.** PACT2.0 must *develop HAS beyond its prototype cutoff implementation*, preserving **sensitivity-first design** for rare, high-amplitude, phase-coupled neural activity. Its purpose is to embed the insight of HAS more defensibly into established PAC and statistical estimators, not to replace it with a generic conservative rank/robustness estimator.

**Target:** be a statistically calibrated, **high-sensitivity, non-dominated point on a conditional PAC-method Pareto frontier**, not necessarily the most artifact-resistant estimator. Trading sensitivity for physiological-artifact resistance is legitimate and should be disclosed. Inflated nominal Type I error due to an invalid statistical null **is not** a legitimate performance tradeoff.

Investigate HAS-descended rank–amplitude approaches to PAC that:
- allocate high sensitivity to rare, large-amplitude observations without claiming that a hard percentage cutoff is a physiological boundary;
- use all-rank / smooth-tail / multi-scale selection *only if* the behavior of original HAS is recoverable as an interpretable special or limiting case;
- use relative rank and amplitude magnitude together where useful, without erasing real sparse bursts through overzealous clipping or median aggregation;
- fit HAS principles into established PAC estimators (Canolty, debiased PAC, Tort/KL, conditional-distribution or MI approaches);
- report the sensitivity–artifact-resistance tradeoff and identify **conditional non-dominated methods**, rather than optimizing a single indiscriminate robustness score;
- compare against conventional HAS-Canolty PAC, phase-only HAS resultant length, Tort KL, dPAC, gcPAC, and conditionally the more complex GLM-MI methods.

The repository is an independent *research investigation*, not a replacement for sccn/PACT. No clinical validity, Pareto dominance, or statistical superiority is assumed until established by simulations and independent validation.

### Important distinctions for the Pareto objective

1. **Statistical false positive:** Under an explicitly specified statistical independence null, the reported test must attain the declared false-positive rate. The entire adaptive search belongs inside the null calibration (or an independent test set). Uncalibrated Type I inflation is **not** an acceptable way to buy sensitivity.
2. **Physiological/artifactual false positive:** A sharp transient, nonsinusoidal generator, or muscle artifact can induce statistical amplitude–phase dependence without the physiological interaction of interest. Resilience to such patterns may trade off against sensitivity to true rare bursts. This is the primary scientific robustness axis.
3. Fix a family of true-signal scenarios and competing physiologic-null/artifact scenarios before drawing a frontier. Different scenarios can have different frontier sets; one universal two-dimensional curve is not assumed.
4. Sensitivity-prioritized method selection is not the same as hand-selecting the method with the smallest p-value. State the sensitivity objective and calibrate the search independently.

**Research success criterion:** show at least one prespecified scenario in which a HAS-descended estimator provides high power to detect genuine sparse PAC at the declared statistical alpha while occupying a non-dominated sensitivity–physiological-false-positive-resistance position against meaningful published baselines. Document conditions where it fails.

## Mathematical starting point

For N valid paired observations with high-frequency amplitude A_t >= 0 and low-frequency phase phi_t, sort amplitude in descending order and carry the corresponding phases. Write z_(r) = exp(1i*phi_(r)), zbar = mean(z), and

D_r = (1/N) * sum_{i=1}^r (z_(i) - zbar).

Then the identity

mean(A.*z) - mean(A)*mean(z) =
    sum_{r=1}^{N-1} (A_(r) - A_(r+1)) * D_r

holds exactly. This algebraic decomposition motivates examination of rank-by-amplitude-gap weighting. It is **not** a demonstration of estimator validity or robustness.

Candidate families to investigate (not yet accepted algorithms):
1. Rank-resolved cumulative phase deviation D_r.
2. Integrated/rank-local phase-dependence statistics with a prespecified null.
3. Robustly weighted rank-amplitude spacings, with parameter sensitivity measured.
4. Rank-aware amplitude reconstruction and phase-bin KL divergence, with phase-occupancy reference.

Note: A rank-only statistic is invariant to strictly monotone amplitude transforms but loses magnitude information. A robustified amplitude statistic may damp genuine rare high-amplitude bursts. The tradeoff is central, not an implementation detail.

## Required validation

- Exact algebraic identity tests and edge cases (ties, constant amplitude, extreme outliers, nonuniform phase marginals).
- Null calibration under independent amplitude/phase with autocorrelation, long bursts, nonsinusoidal phase, and event-locked nonstationarity.
- Power under persistent coupling, rare burst coupling, amplitude-band-specific coupling, and bimodal phase preference.
- Comparison against preselected benchmark methods using consistent null-calibration and corrected multiplicity.
- Runtime and memory scaling versus number of samples, channels, frequencies, and surrogate draws.

Do not interpret small nominal p-values as evidence of physiological PAC without validation under an appropriate data-generating null. If estimator or hyperparameter selection uses phase information, repeat that search inside each null draw or evaluate on independent data.

## Pipeline invariants (TRACE-style, project-specific)

- Root contains only `code/` and p-numbered data/output directories.
- `p0000_...` is reserved for starting raw data, not a generated analysis output. No placeholder raw files are manufactured.
- Pipeline scripts begin with **p0010** and progress in ascending p-numbers.
- Pipeline MATLAB scripts are directly under `code/`, with filenames such as `pNNNN_stage_name.m`. No nonpipeline files directly under `code/`.
- Every pipeline script writes **only** into the root directory exactly matching its basename.
- Generated output directories are never manually altered; to change an output, change its script and rerun.
- Scripts execute independently from a clean MATLAB session, with fixed seeds and no interactive inputs. Scripts load intermediate files only from strictly lower-numbered output directories.
- Unit-test-worthy research functions live in `code/lib/` and associated tests in `code/tests/`; published pinned third-party code belongs in `code/external/`. Supporting documentation belongs in `code/docs/`.
- No nested functions. Local helper functions after the final `end` are only for boilerplate, not scientific methods.
- Explicitly authorized exception (2026-11-19): root-level `.github/workflows/` is permitted **only** for GitHub Actions workflow configuration. No other root-level files or directories are authorized; no workflow is created until literature review and methods design.

## Open decisions

- Confirm the precise p0010 stage name and role before creating a pipeline script.
- GitHub Actions location resolved: **option B approved**, `.github/workflows/` exception only. Workflow contents and execution remain pending literature review.
- Determine if simulations should use only synthetic data generated by p0010 or also later ingest raw data from p0000.
