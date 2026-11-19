# PACT2.0 literature reading queue

Created: 2026-11-19. Bibliography verified against publisher, PubMed, PMC, or journal records. **Full texts have not yet been read in this project.**
No simulation, pipeline script, or GitHub Actions workflow may be developed until the full reading list supplied by the user has been reviewed and the statistical hypotheses and null models documented (unless the user explicitly narrows this list).

**Repository policy:** GitHub Actions option B approved; only `.github/workflows/` is an explicit root-level exception. The first processing script starts at p0010, and p0000 is reserved for raw data.

## First-priority reading (15 papers)

| ID | Paper | DOI | Why it matters |
|---|---|---|---|
| P01 | Canolty et al. (2006), *High gamma power is phase-locked to theta oscillations in human neocortex*, Science | [10.1126/science.1128115](https://doi.org/10.1126/science.1128115) | Foundational phase-weighted high-gamma coupling measure |
| P02 | Tort et al. (2010), *Measuring phase-amplitude coupling between neuronal oscillations of different frequencies*, J Neurophysiol | [10.1152/jn.00106.2010](https://doi.org/10.1152/jn.00106.2010) | KL-based amplitude-over-phase profile; comparable baseline |
| P03 | Miyakoshi et al. (2013), *Automated detection of cross-frequency coupling in the electrocorticogram for clinical inspection*, EMBC | [10.1109/EMBC.2013.6610242](https://doi.org/10.1109/EMBC.2013.6610242) | Original PACT / HAS motivation |
| P04 | Miyakoshi et al. (2021), *Automated preprocessing and phase-amplitude coupling analysis of scalp EEG discriminates infantile spasms from controls during wakefulness*, Epilepsy Res | [10.1016/j.eplepsyres.2021.106809](https://doi.org/10.1016/j.eplepsyres.2021.106809) | HAS application and interpretation; 2% high-amplitude selection |
| P05 | van Driel, Cox & Cohen (2015), *Phase-clustering bias in phase-amplitude cross-frequency coupling and its removal*, J Neurosci Methods | [10.1016/j.jneumeth.2015.07.014](https://doi.org/10.1016/j.jneumeth.2015.07.014) | Correct for non-uniform phase distribution and distinguish phase bias from coupling |
| P06 | Ince et al. (2017), *A statistical framework for neuroimaging data analysis based on mutual information estimated via a gaussian copula*, Hum Brain Mapp | [10.1002/hbm.23471](https://doi.org/10.1002/hbm.23471) | Rank-normalized copula MI baseline and assumptions |
| P07 | Combrisson et al. (2020), *Tensorpac*, PLoS Comput Biol | [10.1371/journal.pcbi.1008302](https://doi.org/10.1371/journal.pcbi.1008302) | gcPAC uses ranks of amplitude; must understand overlap with proposed estimator |
| P08 | Perley & Coleman (2024), *A mutual information measure of phase-amplitude coupling using gamma generalized linear models*, Front Comput Neurosci | [10.3389/fncom.2024.1392655](https://doi.org/10.3389/fncom.2024.1392655) | Explicit conditional amplitude given phase; joint-distribution model |
| P09 | Perley & Coleman (2026), *A Dynamic Mutual Information Measure of Phase-Amplitude Coupling With Uncertainty Quantification*, IEEE Trans Biomed Eng | [10.1109/TBME.2026.3705664](https://doi.org/10.1109/TBME.2026.3705664) | New dynamic gamma-GLM information estimator with uncertainty |
| P10 | Rivest (2026), *Rank correlations for bivariate circular-circular and circular-linear data*, Comput Stat Data Anal, online before Dec. 2026 issue | [10.1016/j.csda.2026.108449](https://doi.org/10.1016/j.csda.2026.108449) | Direct circular-linear rank-dependence novelty check |
| P11 | Koenker & Bassett (1978), *Regression quantiles*, Econometrica | [10.2307/1913643](https://doi.org/10.2307/1913643) | Conditional quantile functions, median as a special quantile |
| P12 | Huber (1964), *Robust Estimation of a Location Parameter*, Ann Math Stat | [10.1214/aoms/1177703732](https://doi.org/10.1214/aoms/1177703732) | Robust estimators between mean and median; contamination model |
| P13 | Hampel (1974), *The Influence Curve and its Role in Robust Estimation*, JASA | [10.1080/01621459.1974.10482962](https://doi.org/10.1080/01621459.1974.10482962) | Influence functions, local robustness and breakdown-related questions |
| P14 | Theiler et al. (1992), *Testing for nonlinearity in time series: the method of surrogate data*, Physica D | [10.1016/0167-2789(92)90102-S](https://doi.org/10.1016/0167-2789(92)90102-S) | Surrogate null must preserve null-relevant structure |
| P15 | Kriegeskorte et al. (2009), *Circular analysis in systems neuroscience: the dangers of double dipping*, Nat Neurosci | [10.1038/nn.2303](https://doi.org/10.1038/nn.2303) | Selection-dependent inference and max over tuned rank/phase parameters |

## Second-priority reading (9 papers; recommended before implementation)

| ID | Paper | DOI | Why it matters |
|---|---|---|---|
| P16 | Dvorak & Fenton (2014), *Toward a proper estimation of phase-amplitude coupling in neural oscillations*, J Neurosci Methods | [10.1016/j.jneumeth.2014.01.002](https://doi.org/10.1016/j.jneumeth.2014.01.002) | Oscillation-triggered coupling alternative and filter bandwidth rules |
| P17 | Hülsemann, Naumann & Rasch (2019), *Quantification of Phase-Amplitude Coupling...*, Front Neurosci | [10.3389/fnins.2019.00573](https://doi.org/10.3389/fnins.2019.00573) | Multiple PAC estimator performance benchmarks and generative models |
| P18 | Berens (2009), *CircStat: A MATLAB Toolbox for Circular Statistics*, J Stat Softw | [10.18637/jss.v031.i10](https://doi.org/10.18637/jss.v031.i10) | Circular mean, median, directional tests; MATLAB reference |
| P19 | Minsker (2015), *Geometric median and robust estimation in Banach spaces*, Bernoulli | [10.3150/14-BEJ645](https://doi.org/10.3150/14-BEJ645) | Blockwise robust complex-valued estimation if needed |
| P20 | Kramer, Tort & Kopell (2008), *Sharp edge artifacts and spurious coupling in EEG frequency comodulation measures*, J Neurosci Methods | [10.1016/j.jneumeth.2008.01.020](https://doi.org/10.1016/j.jneumeth.2008.01.020) | Artifactual PAC generated by sharp transients |
| P21 | Aru et al. (2015), *Untangling cross-frequency coupling in neuroscience*, Curr Opin Neurobiol | [10.1016/j.conb.2014.08.002](https://doi.org/10.1016/j.conb.2014.08.002) | Stationarity and physiological interpretation |
| P22 | Lozano-Soldevilla, ter Huurne & Oostenveld (2016), *Neuronal Oscillations with Non-sinusoidal Morphology Produce Spurious Phase-to-Amplitude Coupling and Directionality*, Front Comput Neurosci | [10.3389/fncom.2016.00087](https://doi.org/10.3389/fncom.2016.00087) | Non-sinusoidal waveforms and harmonics as PAC confounds |
| P23 | Wodeyar et al. (2023), *Different Methods to Estimate the Phase of Neural Rhythms Agree But Only During Times of Low Uncertainty*, eNeuro | [10.1523/ENEURO.0507-22.2023](https://doi.org/10.1523/ENEURO.0507-22.2023) | Low-frequency phase estimates can be ambiguous; confidence vs sample selection |
| P24 | Maris & Oostenveld (2007), *Nonparametric statistical testing of EEG- and MEG-data*, J Neurosci Methods | [10.1016/j.jneumeth.2007.03.024](https://doi.org/10.1016/j.jneumeth.2007.03.024) | Max-statistic permutation logic and multiple comparisons |

## Reading audit deliverables before coding

1. Define the estimand precisely: mean amplitude by phase, upper-tail occurrence, rank-by-phase dependence, or amplitude–rank joint functional.
2. Determine which part of the proposed idea is already covered by gcPAC, conditional-Gamma GLM, and recent circular-linear rank statistics.
3. Validate whether rank–amplitude spacing weighting has bounded gross-error sensitivity without removing genuine rare bursts. The claim is **not established**.
4. Identify null models for autocorrelated LFO and HFO, non-uniform phase, event-locking, and nonstationarity.
5. Explicitly distinguish a descriptive rank–phase curve from its global hypothesis test; model selection or scanning must be repeated in null draws or tested independently.
6. Only then decide the p0010 name, stage responsibility, exact MATLAB scripts, baseline methods, and repository workflow.

## Access / copyright

PDFs should be supplied as conversation attachments (or private material available through an authorized connector) rather than pushed into the public PACT2.0 repository unless their distribution licenses explicitly permit redistribution. Reading queue and original notes may be committed under `code/docs/`.
