# CIRBP evolution: did long-lived mammals evolve a "better" DNA-repair protein?

**Part 2** of [sleep-cirbp](https://github.com/riddhikad9b-ux/sleep-cirbp). Part 1 showed that sleep loss lowers *Cirbp* in the mouse brain (3 datasets, pooled p = 0.00016). This repository asks whether **evolution tuned CIRBP's gene sequence in long-lived or cool-bodied mammals**.

## Answer in one line
**No.** Once mammal family history is taken into account, CIRBP's codon usage does not track longevity or body temperature. The bowhead whale's enhanced CIRBP looks like a **whale-specific adaptation**, not a mammal-wide rule.

## Background
The bowhead whale (200+ years) has high levels of CIRBP. CIRBP is a cold-inducible protein that boosts DNA double-strand-break repair, and the bowhead version of the gene uses more efficient codons (Firsanov et al., *Nature* 2025). We asked whether the same pattern appears across mammals.

## Two analyses

| | Analysis 1 (Ensembl) | Analysis 2 (NCBI, main) |
|---|---|---|
| Notebook | `cirbp_evolution_ensembl_v3.ipynb` | `cirbp_temperature_ncbi.ipynb` |
| CIRBP sequences | 56 mammals | 251 mammals |
| With lifespan + codon data | 22 | 84 (79 in joint model) |
| Mammal orders | 7 | 19 |
| Control genes | 20 | 44 |

## Results

### Analysis 1: first look (22 species)
| Measure | vs longevity | Within orders | Note |
|---|---|---|---|
| CIRBP CAI (GC-corrected) | rho = −0.48, p = 0.022 | p = 0.28 | Opposite direction to the hypothesis; disappears within orders |
| CIRBP GC3 vs body temperature | rho = +0.58, p = 0.004 | — | Suggested a temperature effect, tested in Analysis 2 |
| Arg CGN codons, RBM3, protein sites | all p > 0.1 | — | No signal |

### Analysis 2: proper test (up to 84 species)
Model: measure ~ body temperature + longevity residual + mammalian order (fixed effect), errors clustered by family. GC3 and CAI are also measured **relative to each species' genome background** (median across 66 other genes).

| CIRBP measure | Temperature effect | Beats controls | Longevity effect (given temperature) |
|---|---|---|---|
| GC3 (relative) | t = +0.70, p = 0.49 | 45% | t = +1.03, p = 0.31 |
| GC3 | t = +0.65, p = 0.52 | 39% | t = +0.84, p = 0.41 |
| CAI (relative) | t = +0.43, p = 0.67 | 27% | t = −0.38, p = 0.70 |
| CAI | t = +1.55, p = 0.13 | 73% | t = −1.23, p = 0.23 |
| Arg CG share | t = +0.64, p = 0.52 | 50% | t = +0.80, p = 0.43 |

**Robustness:** mixed model (order + family random effects): temperature p = 0.65 (GC3_rel), 0.14 (CAI_rel). Leaving out any one order: all |t| < 1.1.

**Why the raw correlation misled:** CIRBP GC3 correlates with temperature in raw data (rho = +0.45), but the coolest mammals (echidna, bats, naked mole-rat, opossum, tenrec) come from a few lineages. The difference is between lineages, not caused by temperature.

### Exploratory hint (not pre-registered)
**RBM3**, CIRBP's sister cold-shock gene: relative CAI rises with longevity (t = +3.36, p = 0.002, beats 95% of controls). This is 1 of about 20 tests and was not predicted; after multiple-testing correction it is borderline (≈ 0.04). It needs an independent check before any claim.

## Conclusion
Across up to 84 mammals, CIRBP codon usage showed no association with longevity or body temperature after controlling for phylogeny (order fixed effects, family-clustered errors, mixed models) and genome background. The bowhead whale's CIRBP enhancement therefore appears **lineage-specific**.

## Limitations
- Order fixed effects and family clustering are a stand-in for a full phylogenetic model (PGLS with a dated tree).
- Only 84 of 251 species had lifespan and temperature data in AnAge.
- The bowhead whale is not in Ensembl and was not matched in this NCBI run.
- Codon measures reflect sequence, not protein amount; the bowhead finding was about protein levels too.

## Data
- **Sequences:** NCBI Datasets ortholog sets (taxon Mammalia, 40674); Ensembl REST for Analysis 1.
- **Lifespan, body mass, body temperature:** AnAge (Human Ageing Genomic Resources).
- **Structure (Analysis 1):** AlphaFold DB model of human CIRBP (UniProt Q14011); ESM-2 protein language model.

## How to run
Open a notebook in `notebooks/` in Google Colab and choose **Runtime > Run all**. Analysis 2 takes about 10–20 minutes. Executed copies with real outputs are in `results/`.

## Author
Riddhika D, B.Tech Biotechnology, Sathyabama Institute of Science and Technology, Chennai, India.

Code: MIT licence.
