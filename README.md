# field_MPs_codes: Code 1-3 for "A library-independent Raman band rule calibrated by permutation for comparing Raman and FTIR identification of field microplastics"

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22145774.svg)](https://doi.org/10.5281/zenodo.22145774)

Companion code and data products for
Kim, Y. (2026). *A library-independent Raman band rule calibrated by permutation for comparing Raman and FTIR identification of field microplastics*. Submitted for publication.

**Archived version:** release `v1.2.0-manuscript` (notebooks re-executed end to end on 13 October 2026; raw spectra of the comparison set added 21 October 2026) · Zenodo DOI **10.5281/zenodo.22145774** (concept DOI, cited in the manuscript; it resolves to the latest archived version, currently `v1.2.0-manuscript`).
The three notebooks are archived **as executed**: every cell retains the output of the final end-to-end run, so the numbers in the article can be checked against cell outputs without re-running anything.

**Relation to `v1.0.1-manuscript` (29 August 2026).** The decision logic is unchanged. The Code 1 hand-off read by Code 2 (`outputs/ground_truth_for_code2.csv`) is byte-identical to the first release (SHA-256 checked in Code 1 §17-6). `v1.1.0-manuscript` differs only in output wording, annotations, figure numbering aligned with the manuscript, the cache-settings record in Code 1 §12-4 and the supplementary analysis Code 3 E.3; `v1.2.0-manuscript` adds the raw spectra of the comparison set under `data/raw/` and changes nothing else (see *Changes* below).

**Licence.** CC BY-NC 4.0: free to download, study and reuse for research and other non-commercial purposes, with citation of the article and this archive (see `LICENSE` and `CITATION.cff`). Commercial use requires permission from the corresponding author.

## Pipeline

Three notebooks with strictly one-way data flow. No label, score or flag produced downstream re-enters an upstream notebook.

| Notebook | Version | Reads | Writes |
|---|---|---|---|
| `Code1_raman_reference.ipynb` | v1.0 | field Raman spectra*, SLoPP/SLoPP-E (external) | `ground_truth_for_code2.csv`, `handoff_manifest.json`, `sens_C_delta.csv`, `band_provenance.csv`, `environment.json`, `validation/` |
| `Code2_spec_class_omnic.ipynb` | framework v1.0, parameter set p1 | Code 1 hand-off, field FT-IR spectra*, OMNIC hit names | `code3_input_catalogue_v01.csv`, `params_snapshot_p1.json`, `SI_band_provenance.csv`, `SI_rule_provenance.csv` |
| `Code3_naming_divergence.ipynb` | v1.0 | Code 2 catalogue, Open Specy + siMPle libraries (external) | `code3_master_n47.csv`, `SI_stream_dictionary.csv`, `SI_*.csv` supplementary tables, `code3_manifest.json`, all comparisons and figures |

\* Raw spectra of the 47 comparison particles and of the standards are in `data/raw/`; the remaining 181 FT-IR spectra of the 228-particle catalogue are retained for follow-up studies (see `NOTICE.md`). The archived outputs make every downstream step checkable without them.

## Repository layout

```
notebooks/
  Code1_raman_reference.ipynb        # executed; outputs preserved in every cell
  Code2_spec_class_omnic.ipynb
  Code3_naming_divergence.ipynb
data/
  band_provenance.csv                # Raman diagnostic band ledger: every band with its literature source
  SI_band_provenance.csv             # FT-IR band ledger (Code 2)
  SI_rule_provenance.csv             # FT-IR decision-rule ledger (Code 2)
  params_snapshot_p1.json            # frozen parameter snapshot, incl. THRESHOLD_PROVENANCE (Code 2)
  handoff_manifest.json              # Code 1 -> Code 2 contract, incl. RULE_C_PROVENANCE
  environment.json                   # software versions of the archived run
  validation/                        # Code 1 §17: accuracy on spectra of known identity (SLoPP / SLoPP-E)
    validation_truth_v1.csv          #   scope of every depositor name, fingerprinted before any decision (§17-0a)
    validation_protocol_v1.json      #   every analysis choice, fingerprinted before any decision (§17-0b)
    validation_equivalence_field47.csv  # §17-2: the frozen rule reproduces all 47 field assignments
    validation_metrics.csv           #   §17-4: precision, coverage, false-positive rate (Table 3b)
    validation_confusion_SLoPP.csv   #   §17-4: confusion matrix, SLoPP (Fig. 2a)
    validation_confusion_SLoPP-E.csv #   §17-4: confusion matrix, SLoPP-E (Fig. 2b)
    validation_offset_diagnostic.csv #   §17-4: key-band offsets from the nearest peak
    validation_manifest.json         #   §17-6: fingerprints of the validation outputs
  raw/                               # raw spectra of the comparison set and the standards (see data/raw/README.md)
    raman_47/                        #   47 Raman spectra (.txt, instrument export)
    ftir_47/                         #   47 ATR-FTIR spectra of the same particles (.CSV, OMNIC export)
    standards_raman/                 #   Si, polystyrene (ASTM E1840, two sessions), LDPE and iPP pellets (.txt)
    standards_ftir/                  #   LDPE and iPP pellets (.CSV)
    raw_manifest.csv                 #   file list with size and SHA-256
outputs/
  ground_truth_for_code2.csv         # Code 1 -> Code 2 (the Raman Code 1 Reference)
  sens_C_delta.csv                   # Code 1 -> Code 2 (wavenumber-offset sensitivity)
  code3_input_catalogue_v01.csv      # Code 2 -> Code 3 (particle x stream catalogue)
  code3_master_n47.csv               # Code 3 master table (verbatim labels of all 47 particles)
  SI_stream_dictionary.csv           # table label <-> CSV column bridge (ESI)
  SI_pairwise_mcnemar_bh.csv         # Code 3 E.1: pairwise McNemar tests, Benjamini-Hochberg corrected
  SI_ari_by_stratum.csv              # Code 3 E.1: adjusted Rand index by stratum (emitted / withheld)
  SI_granularity_stream5.csv         # Code 3 E.2: stream 5 at entry level vs class level
  SI_granularity_ari.csv             # Code 3 E.2: ARI of stream 5 pairs at both levels
  SI_pepp_by_agreement.csv           # Code 3 E.3: PE/PP completeness where both Raman methods agree
  code3_manifest.json                # Code 3 run record
LICENSE · CITATION.cff · NOTICE.md · README.md · .zenodo.json
```

## Where the items named in the article's data-availability statement live

| Item | Location |
|---|---|
| Three notebooks, archived as executed | `notebooks/` |
| Diagnostic band library and its source ledger | band positions defined in Code 1 §2; per-band sources in `data/band_provenance.csv` |
| Threshold-provenance records | `RULE_C_PROVENANCE` in `data/handoff_manifest.json` (Raman rule); `THRESHOLD_PROVENANCE` in `data/params_snapshot_p1.json` (FT-IR rules) |
| Frozen parameter snapshot | `data/params_snapshot_p1.json` |
| Validation truth table and protocol, with fingerprints | `data/validation/` |
| Full catalogue of verbatim labels | `outputs/code3_master_n47.csv` |
| Stream dictionary | `outputs/SI_stream_dictionary.csv` |
| Preprocessed Raman spectra of the 47 comparison particles, with diagnostic-band evidence | worksheet output of Code 1, section 11 (in the notebook) |
| Particle photographs | ESI of the article (not in this repository) |
| Raw FT-IR and Raman spectra | `data/raw/` (47 comparison particles and the standards); the remaining 181 FT-IR spectra on reasonable request |

Sensitivity grids, null-model tables, per-band performance tables and the validation on spectra of known identity are in the cell outputs of Code 1 sections 12-17 and Code 2 sections 0.5-0.10; the ESI of the article reproduces the subset it cites.

## Where the article's figures and tables come from

| Article | Notebook cell |
|---|---|
| Fig. 1 (a, b) | Code 1 §11-1 (copies of the §11 worksheet figures for 0517S1-1 and 0614S1-1) |
| Fig. 2 | Code 1 §17-5 (`Fig2_validation_confusion`) |
| Fig. 3 | Code 3 F1b (`Fig3_alluvial_verbatim`) |
| Fig. 5 | Code 3 F1 (`Fig5_ari_matrix`) |
| Fig. 6 | Code 3 F1a (`Fig6_completeness_ci_pepp`) |
| Fig. 7 | Code 3 F1c (`Fig7_score_vs_agreement`) |
| Fig. S5 | Code 1 §12-2 and §12-3 (`null_A1_*.png`) |
| Table 2 | Code 1 §16 |
| Table 3a | Code 1 §13, §14, §12, §12-2, §12-3 |
| Table 3b | Code 1 §17-4 and §17-6 |
| Table 4 | Code 3 D.1 |
| Table 5 | Code 3 C1 (rows of `code3_master_n47.csv`) |

Fig. 4 (FT-IR spectra of the Table 5 particles) was drawn from the archived spectra with the band windows of Code 2 §0.2 and is not produced by the three notebooks.

## Labelling streams (as in the article tables)

| Label | Modality | Library / method | CSV column |
|---|---|---|---|
| 1. Raman ref | Raman | in-house rule + evidence floor (reference axis; not a verified ground truth) | `raman_gt` |
| 2. SLoPP | Raman | SLoPP **and** SLoPP-E libraries, Code 1 preprocessing (Open Specy software not used) | `B_label` |
| 3. spec_class | FT-IR | in-house rule | `spec_class` |
| 4. omnic_name | FT-IR | OMNIC commercial libraries, hit name verbatim | `omnic_name` |
| 5. OS_cor | FT-IR | Open Specy `derivative` library, `match_spec` | `openspecy_name` |
| 6. OS_ml | FT-IR | Open Specy `model_derivative`, `ai_classify` | `ml_name` |
| 7. siMPle | FT-IR | siMPle ATR single-spectra reference library (siMPle software not run) | `simple_name` |

Two analysis layers: reference-free (N = 47) and reference-anchored (N = 33; 14 of the 47 were withheld by the evidence floor). The two denominators are never mixed.

## Re-running

The archived notebooks already contain their outputs; re-execution is optional. `data/raw/` holds the Raman and FT-IR spectra of the 47 comparison particles and of the standards (placement of the folders is described in `data/raw/README.md`). With these files Code 1 re-runs end to end (the hand-off must reproduce the SHA-256 checked in §17-6), Code 3 re-runs end to end from the archived catalogue (`outputs/code3_input_catalogue_v01.csv`) and the external libraries listed in `NOTICE.md`, and Code 2 re-runs its standard verification (0.5) and the comparison against the Code 1 reference (Part 4). Code 2 Parts 1-3 and the threshold sweeps of 0.6-0.10 use the full 228-spectrum catalogue, of which the remaining 181 FT-IR spectra are retained for follow-up studies; those sections are documented by their preserved outputs. Environment: Google Colab, Python 3.13 (NumPy 2.1, SciPy 1.16, pandas 2.2, Matplotlib 3.10; exact versions in `data/environment.json`) and, for Code 3, R 4.6 with `OpenSpecy` 1.5.3 via `rpy2`.

## Changes

- **v1.2.0-manuscript (2026-10-21).** Adds `data/raw/`: raw Raman and ATR-FTIR spectra of the 47 comparison particles and of the standards, with a file manifest (size and SHA-256). Notebooks, data products and decision logic are unchanged from v1.1.0-manuscript.
- **v1.1.0-manuscript (2026-10-20).** All three notebooks re-executed end to end on 13 October 2026. No change to any decision rule, threshold or vocabulary; the Code 1 hand-off is byte-identical to v1.0.1 (Code 1 §17-6). Code 1 §12-4 now records the settings under which the SLoPP corpus cache was built and 0-Z carries that record back to the project folder. Code 3 gained section E.3 (PE/PP completeness restricted to particles on which both Raman methods agree) and writes its supplementary tables to `outputs/`. Output wording, figure file names and section references were aligned with the manuscript; `data/validation/` added.
- **v1.0.1-manuscript (2026-08-29; GitHub tag `v1.0-manuscript`).** First archived release.

## How to cite

The associated article has been submitted for publication. Until it is published, please cite this archive by its Zenodo record; the article reference below will be completed with the journal citation and DOI on acceptance.

**This archive (software and data products)**

> Kim, Y. (2026). Code 1-3 for 'A library-independent Raman band rule calibrated by permutation for comparing Raman and FTIR identification of field microplastics' (v1.2.0-manuscript) [Software]. Zenodo. https://doi.org/10.5281/zenodo.23529343

All versions: https://doi.org/10.5281/zenodo.22145774 (concept DOI, resolves to the latest version).

**The associated article**

> Kim, Y. (2026). _A library-independent Raman band rule calibrated by permutation for comparing Raman and FTIR identification of field microplastics_. Submitted for publication.

The licence (CC BY-NC 4.0) makes attribution a condition of use; once the article is published, please cite both the article and this archive. `CITATION.cff` is provided and GitHub renders it under "Cite this repository".

## Licence

Code, notebooks and project-authored data products: **CC BY-NC 4.0** (non-commercial use with attribution; see `LICENSE`). Third-party libraries are excluded and remain under their own terms (`NOTICE.md`). The article itself is subject to the publisher's terms and is separate from this repository.
