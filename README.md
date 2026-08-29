# [repo name]: Code 1-3 for "[Article title]"

Companion code and data products for
[Authors] (2026). *[Article title]*. *[Journal]*. DOI: [article DOI]

**Archived version:** release `v1.0-manuscript` · Zenodo DOI **10.5281/zenodo.22145775**
This is the version cited in section 2.7 of the article. The three notebooks are archived
**as executed**: every cell retains the output of the final end-to-end run, so the numbers
in the article can be checked against cell outputs without re-running anything.

**Licence.** CC BY-NC 4.0: free to download, study and reuse for research and other
non-commercial purposes, with citation of the article and this archive (see `LICENSE`
and `CITATION.cff`). Commercial use requires permission from the corresponding author.

## Pipeline

Three notebooks with strictly one-way data flow. No label, score or flag produced
downstream re-enters an upstream notebook.

| Notebook | Version | Reads | Writes |
|---|---|---|---|
| `Code1_raman_reference.ipynb` | v1.0 | field Raman spectra*, SLoPP/SLoPP-E (external) | `ground_truth_for_code2.csv`, `handoff_manifest.json`, `sens_C_delta.csv` |
| `Code2_spec_class_omnic.ipynb` | framework v1.0, parameter set p1 | Code 1 hand-off, field FT-IR spectra*, OMNIC hit names | `code3_input_catalogue_v01.csv`, `params_snapshot_p1.json` |
| `Code3_naming_divergence.ipynb` | v1.0 | Code 2 catalogue, Open Specy + siMPLe libraries (external) | `code3_master_n47.csv`, `SI_stream_dictionary.csv`, all comparisons and figures |

\* Raw spectra are not in this repository (NOTICE.md); the archived outputs make every
downstream step checkable without them.

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
outputs/
  ground_truth_for_code2.csv         # Code 1 -> Code 2 (the Raman Code1 Reference)
  sens_C_delta.csv                   # Code 1 -> Code 2 (wavenumber-offset sensitivity)
  code3_input_catalogue_v01.csv      # Code 2 -> Code 3 (particle x stream catalogue)
  code3_master_n47.csv               # Code 3 master table = ESI Data S1 (verbatim labels)
  SI_stream_dictionary.csv           # table label <-> CSV column bridge (ESI)
LICENSE · CITATION.cff · NOTICE.md · README.md
```

## Where the items named in section 2.7 live

| Item (section 2.7) | Location |
|---|---|
| Three notebooks, archived as executed | `notebooks/` |
| Diagnostic band library and its source ledger | band positions defined in Code 1 §2; per-band sources in `data/band_provenance.csv` |
| Threshold-provenance records | `RULE_C_PROVENANCE` in `data/handoff_manifest.json` (Raman rule); `THRESHOLD_PROVENANCE` in `data/params_snapshot_p1.json` (FT-IR rules) |
| Frozen parameter snapshot | `data/params_snapshot_p1.json` |
| Full catalogue of verbatim labels (ESI Data S1) | `outputs/code3_master_n47.csv` |
| Stream dictionary | `outputs/SI_stream_dictionary.csv` |
| Preprocessed Raman spectra of the 47 comparison particles, with diagnostic-band evidence | worksheet output of Code 1, section 11 (in the notebook) |
| Particle photographs | ESI of the article (not in this repository) |
| Raw FT-IR and Raman spectra | corresponding author, on reasonable request |

Sensitivity grids, null-model tables and per-band performance tables are in the ESI of
the article; the same numbers appear in the cell outputs of Code 1 sections 12-15 and
Code 2 sections 0.5-0.10.

## Labelling streams (as in the article tables)

| Label | Modality | Library / method | CSV column |
|---|---|---|---|
| 1. Raman ref | Raman | in-house rule + evidence floor (reference axis; not a verified ground truth) | `raman_gt` |
| 2. SLoPP | Raman | SLoPP **and** SLoPP-E libraries, Code 1 preprocessing (Open Specy software not used) | `B_label` |
| 3. spec_class | FT-IR | in-house rule | `spec_class` |
| 4. omnic_name | FT-IR | OMNIC commercial libraries, hit name verbatim | `omnic_name` |
| 5. OS_cor | FT-IR | Open Specy `derivative` library, `match_spec` | `openspecy_name` |
| 6. OS_ml | FT-IR | Open Specy `model_derivative`, `ai_classify` | `ml_name` |
| 7. siMPLe | FT-IR | siMPLe ATR single-spectra reference library (siMPLe software not run) | `simple_name` |

Two analysis layers: reference-free (N = 47) and reference-anchored (N = 33; 14 of the 47
were withheld by the evidence floor). The two denominators are never mixed.

## Re-running

The archived notebooks already contain their outputs; re-execution is optional and the raw
field spectra (not distributed) are required only for Code 1 sections 3-11 and Code 2
section 0.3. Everything downstream of the committed hand-off files can be re-run:
Code 3 needs only `outputs/code3_input_catalogue_v01.csv`, `data/params_snapshot_p1.json`
and the external libraries in `NOTICE.md`. Environment: Google Colab, Python 3.13
(NumPy 2.1, SciPy 1.16, pandas 2.2, Matplotlib 3.10; exact versions in
`data/environment.json`) and, for Code 3, R with the `OpenSpecy` package.

## How to cite

Please cite **both** the article and this archive (the licence makes attribution a
condition of use):

> [Authors] (2026). [Article title]. *[Journal]*. DOI [article DOI]
> [Authors] (2026). [repo name] (v1.0-manuscript). Zenodo. DOI 10.5281/zenodo.22145775

`CITATION.cff` is provided; GitHub renders it under "Cite this repository".

## Licence

Code, notebooks and project-authored data products: **CC BY-NC 4.0** (non-commercial use
with attribution; see `LICENSE`). Third-party libraries are excluded and remain under
their own terms (`NOTICE.md`). The article itself is subject to the publisher's terms and
is separate from this repository.
