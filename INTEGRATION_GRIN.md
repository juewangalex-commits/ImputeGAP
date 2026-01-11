# GRIN Integration into ImputeGAP

Author: Wang Jue  
Date: 2026-01-12

## Purpose
This document describes how the GRIN imputation method was executed and integrated
within the ImputeGAP framework for the course project.

The goal was not to re-implement GRIN from scratch, but to:
- Run GRIN inside the ImputeGAP pipeline
- Ensure compatibility on macOS / Python 3.10
- Provide reproducible scripts for evaluation and comparison

---

## What was done

1. Successfully executed GRIN using the ImputeGAP wrapper:
   - Entry point: `imputegap/algorithms/grin.py`
   - Backend: `imputegap/wrapper/AlgoPython/GRIN/`

2. Fixed compatibility issues encountered during execution:
   - Window indexing out-of-bound error in temporal dataset handling
   - DataLoader multiprocessing issues on macOS (solved by using workers=0)

3. Added runnable scripts:
   - `export_grin.py`: runs GRIN and exports imputed results to CSV
   - `compare_methods.py`: compares GRIN with baseline methods

4. Generated experimental results:
   - `grin_imputed_eeg_alcohol.csv`
   - `results.csv` (MAE, RMSE, runtime comparison)

---

## How to reproduce

### 1. Setup environment
```bash
conda create -n imputegap python=3.10
conda activate imputegap
pip install -r requirements.txt

python export_grin.py

python compare_methods.py

Notes

GRIN is already included in the ImputeGAP framework.
This project focuses on:

Making the method runnable in the local environment

Ensuring full execution on real datasets

Providing empirical evaluation and reproducibility
