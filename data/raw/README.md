# Raw spectra of the comparison set

Spectra as written by the instruments, unmodified. Licence: CC BY-NC 4.0 (see `../../LICENSE`).

| Folder | Files | Content |
|---|---|---|
| `raman_47/` | 47 `.txt` | Raman spectra of the 47 comparison particles (RAMANtouch export; the header records laser power, exposure and the instrument-internal wavenumber shift listed in ESI Table S2a) |
| `ftir_47/` | 47 `.CSV` | ATR-FTIR spectra of the same 47 particles (OMNIC export, wavenumber-absorbance) |
| `standards_raman/` | 6 `.txt` | Silicon and polystyrene (ASTM E1840) axis standards, two sessions (Code 1 §13); LDPE and isotactic PP pellets (Code 1 §14); ESI Table S2b |
| `standards_ftir/` | 2 `.CSV` | LDPE and isotactic PP pellets, ATR-FTIR (Code 2 §0.5) |
| `raw_manifest.csv` | | every file with its folder, size in bytes and SHA-256 |

File names are the particle identifiers used throughout the archive: the `file` column of
`outputs/ground_truth_for_code2.csv` (Raman) and of `outputs/code3_master_n47.csv` (FT-IR).
Two spellings occur in the FT-IR names (`0517S1_1.CSV`, `0607S1-12.CSV`); both are read by the parsers.

The remaining 181 FT-IR spectra of the 228-particle catalogue are retained for follow-up studies and
are available from the corresponding author on reasonable request.

## Placing the files to re-run the notebooks

The notebooks copy their inputs from a project folder on Google Drive (`PROJECT` in the first cell of each):

| Archive folder | Project folder | Read by |
|---|---|---|
| `raman_47/` | `raman_spectra/` | Code 1 (0-0, §3-11) |
| `standards_raman/` (Si, PS files) | `standards/` | Code 1 §13 |
| `standards_raman/` (PE, PP files) | `standards_polymer/` | Code 1 §14 |
| `ftir_47/` | `spectra/` | Code 2 §0.3, Code 3 A2-A4 |
| `standards_ftir/` | `standards_ftir/` | Code 2 §0.5 |

With these files Code 1 re-runs end to end, Code 3 re-runs end to end from the archived catalogue, and
Code 2 re-runs sections 0.5 and Part 4; Code 2 Parts 1-3 and 0.6-0.10 need the full 228-spectrum set.
