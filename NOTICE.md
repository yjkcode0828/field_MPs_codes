# Third-party materials: what is and is not in this repository

This repository contains only material authored by the project team, licensed
under CC BY-NC 4.0 (see LICENSE). The reference libraries below are **not part
of the Work and are not redistributed**; each must be obtained from its
original source under that source's own terms. The notebooks state where each
is expected.

| Material | Used by | Status here | Obtain from |
|---|---|---|---|
| SLoPP and SLoPP-E Raman libraries (Munno et al., *Anal. Chem.* 2020, 92, 2443) | Code 1 (stream 2, corpus analysis) | **Not included.** Code 1 section 12-4 downloads and caches them at run time | Rochman lab distribution page |
| siMPLe "Single spectra IR" ATR reference library | Code 3 (stream 7) | **Not included.** Expected in `simple_lib/` | simple-plastics.eu |
| Open Specy `derivative` library and `model_derivative` classifier | Code 3 (streams 5, 6) | **Not included.** Downloaded at run time by the `OpenSpecy` R package | CRAN / Open Specy |
| RRUFF reference spectra (Lafuente et al. 2015) | Code 1 (band library construction) | **Only this project's peak-pick values** appear, inside the band ledger with their source recorded; no RRUFF files | rruff.info |
| OMNIC commercial libraries (Thermo Fisher) | Code 2 (stream 4) | **Only the hit names and HQI as returned** by the software appear in the catalogue; no library spectra, entries or metadata | commercial; not redistributable |
| Raw FT-IR and Raman spectra of the field particles | Code 1, Code 2 | **Not included** (basis of ongoing follow-up studies); available from the corresponding author on reasonable request | - |

The diagnostic band ledgers (`data/band_provenance.csv`,
`data/SI_band_provenance.csv`, `data/SI_rule_provenance.csv`) are compilations
of wavenumber values and rule criteria transcribed from the published
literature; every entry records its source.
