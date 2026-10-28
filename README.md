# Overlapping Windows Are Not a Test

Code, data and results for the paper

> A. Mehfooz, "Overlapping Windows Are Not a Test: Measuring and Removing Split Leakage in Remaining-Useful-Life Evaluation," submitted to *IEEE Transactions on Reliability*, 2026.

Data-driven remaining-useful-life (RUL) models are trained on sliding windows cut from run-to-failure records. When windows of one unit are split at random between training and validation or test sets, neighbouring windows share raw cycles and the score stops describing performance on a new unit. This repository measures that bias on six fleets (C-MAPSS FD001–FD004, PHM08, and 124 measured lithium-ion cells), tests a purge of overlapping training windows, and shows the cost for model selection and early stopping.

## Contents

| Folder | What it holds |
|---|---|
| `paper/` | Manuscript (`main.tex`, `main.pdf`), supplementary material, figures |
| `code/` | All experiment scripts (see below) |
| `results/` | JSON result files behind every table and figure; literature-survey table |
| `data/` | C-MAPSS training and official test files, PHM08 training set, Severson et al. battery per-cycle summary |

## Reproduce

Python 3.10+ with `numpy scipy scikit-learn h5py matplotlib torch`.

```bash
python code/run_rev8.py              # FD001-FD004 paired design, unpaired splits, simulator, overlap sweep
python code/run_rev9_deep_purged.py  # CNN/LSTM purged column (FD001)
python code/run_rev10.py             # dense windows, RMSE, model selection, simulator sweep
sh code/run_all_rev11.sh             # six fleets, bootstrap, deep early stopping, official tests
                                     # (Windows: code\run_all_rev11.bat)
python code/make_figs_rev9.py        # figures
python code/make_supp.py             # supplementary tables
cd paper && pdflatex main.tex && pdflatex main.tex
```

The full run takes several hours on a laptop CPU.

## Data sources

- **C-MAPSS and PHM08**: A. Saxena, K. Goebel, D. Simon and N. Eklund, "Damage propagation modeling for aircraft engine run-to-failure simulation," PHM 2008. NASA Prognostics Data Repository.
- **Battery cells**: K. A. Severson *et al.*, "Data-driven prediction of battery cycle life before capacity degradation," *Nature Energy*, 4, 383–391, 2019. Original release: https://data.matr.io/1. The per-cycle summary used here was taken from https://github.com/JasonLi-Arrebol345561/Battery-Cycle-Life-Prediction (124 cells, cycle lives 148–2237, matching the publication).

Please cite the original data sources when using the data.

## Licence

Code: MIT (see `LICENSE`). Data files remain under the terms of their original providers.

## Citation

See `CITATION.cff`.
