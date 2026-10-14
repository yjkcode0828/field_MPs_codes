# Third-party materials: what is and is not in this repository

This repository contains only material authored by the project team, licensed
under CC BY-NC 4.0 (see LICENSE). The reference libraries below are **not part
of the Work and are not redistributed**; each must be obtained from its
original source under that source's own terms. Versions are those used in the
archived end-to-end run of 13 October 2026 (release `v1.1.0-manuscript`); they
are the same versions as in the first release of 29 August 2026 except where a
fetch date is given. The notebooks state where each library is expected.

| Material | Version used | Used by | Status here | Obtain from |
|---|---|---|---|---|
| SLoPP and SLoPP-E Raman libraries (Munno et al., *Anal. Chem.*, 2020, 92, 2443–2451) | 2020 distribution, no version number: SLoPP 148 and SLoPP-E 113 spectra (`slopp-and-slopp-e.zip`, `copy-of-slopp-and-slopp-e-spectra-itemized_public.xlsx`) | Code 1 §12-4 (per-band corpus analysis), §15 (stream 2 and support level), §15-2 (specificity weights) | **Not included.** §12-4 fetches the two files from the URLs below and caches them; §15 and §15-2 reuse that cache. The settings under which the cache was built are recorded in `corpus_build_settings.json` beside it (§12-4) and the cache files are fingerprinted in §17-4 | [Rochman Lab spectral libraries page](https://rochmanlab.wordpress.com/spectral-libraries-for-microplastics-research/); files: [zip](https://rochmanlab.wordpress.com/wp-content/uploads/2020/02/slopp-and-slopp-e.zip), [xlsx](https://rochmanlab.wordpress.com/wp-content/uploads/2020/09/copy-of-slopp-and-slopp-e-spectra-itemized_public.xlsx). Free for research use; not intended for commercial purposes |
| siMPle "Single spectra IR" ATR reference library (Primpke et al., *Appl. Spectrosc.*, 2020, 74, 1127–1138) | v1.0.2 (`siMPle_ATR_single_file_library_Version1.0.2.txt`; 326 spectra listed by the distributor) | Code 3 (stream 7) | **Not included.** Expected in `simple_lib/`; without it Code 3 runs with five streams | [simple-plastics.eu](https://simple-plastics.eu) |
| Open Specy R package and reference libraries (Cowger et al., *Anal. Chem.*, 2021, 93, 7543–7548) | Package 1.5.3 (CRAN). Libraries `derivative` (43,171 spectra, of which the 21,542 FT-IR spectra were used) and `model_derivative` (FT-IR classifier, 26 classes), fetched by `get_lib()` on 13 October 2026 (`derivative` file 42,005,267 bytes); the libraries carry no version number, so the fetch date and file size identify them. The 29 August 2026 run fetched the same file and obtained the same counts | Code 3 (streams 5 and 6) | **Not included.** The package is installed and the libraries are downloaded at run time | Package: [CRAN](https://cran.r-project.org/package=OpenSpecy); libraries: [OSF](https://osf.io/x7dpz/) (DOI 10.17605/OSF.IO/X7DPZ). The libraries compile data from many groups; their individual sources are listed in the `get_lib()` documentation |
| RRUFF reference spectra (Lafuente et al., 2015) | Quartz R040031, R050125, R060604; hematite R040024, R050300, R060190, R110013; anatase R060277; rutile R050031, R060745 | Code 1 §2 (band library construction) | **Only this project's peak-pick values** appear, inside the band ledger with their source recorded; no RRUFF files | [rruff.info](https://rruff.info) |
| OMNIC commercial libraries (Thermo Fisher Scientific) | OMNIC 9.11.745 on the Nicolet iS50; correlation search over 748–3302 cm⁻¹; 23 libraries searched together, listed in the ESI of the article | Code 2 (stream 4) | **Only the hit names and HQI as returned** by the software appear in the catalogue; no library spectra, entries or metadata | Commercial; not redistributable |
| Raw FT-IR and Raman spectra of the field particles (project data) | — | Code 1 §3–11, Code 2 §0.3, Code 3 (streams 5–7) | **Not included** (basis of ongoing follow-up studies); available from the corresponding author on reasonable request. The 47 Raman spectra (raw, ALS baseline and baseline-corrected) and their peak lists are shown in the executed output of Code 1 §11 | — |

The diagnostic band ledgers (`data/band_provenance.csv`,
`data/SI_band_provenance.csv`, `data/SI_rule_provenance.csv`) are compilations
of wavenumber values and rule criteria transcribed from the published
literature; every entry records its source.
