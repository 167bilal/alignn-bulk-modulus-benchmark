# Same Average, Larger Typical Error

Code and data for the paper **"Same Average, Larger Typical Error: Testing a Pretrained ALIGNN Bulk Modulus Model on Materials Outside Its Training Data"** by Muhammad Bilal (Department of Physics, University of Peshawar).

## What this study does

Pretrained graph neural networks such as ALIGNN are usually judged by their mean error on a randomly chosen test set. This project tests the pretrained ALIGNN bulk modulus model on 12,753 JARVIS-DFT materials that are absent from all of its published training, validation and test splits, and compares its errors with those on its official test set.

## Main results

| | Official test set | Unseen materials |
|---|---|---|
| Materials (after removing non-positive labels) | 1,227 | 12,571 |
| Mean absolute error | 9.94 GPa | 10.06 GPa |
| Median absolute error | 3.06 GPa | 5.22 GPa |

- The pipeline reproduces the model's published benchmark (9.94 GPa against a reported 9.89 GPa).
- Mean error on unseen materials matches the benchmark, but median error is 1.7 times higher (one-sided Mann–Whitney U test, p < 10⁻²⁶).
- About 2% of bulk modulus values in JARVIS-DFT are zero or negative, which is physically impossible for a stable crystal.

## Repository contents

```
notebooks/
  01_build_dataset.ipynb   download JARVIS-DFT, classify splits, label-quality audit
  02_run_alignn.ipynb      run the pretrained model (Google Colab, GPU)
  03_analysis.ipynb        all statistics, tables and Figure 1 (runs on a laptop)
data/
  alignn_bulk_modulus_full_results.csv   one row per material: DFT value, prediction, split
figures/
  figure1_error_cdf.png / .pdf
```

## How to reproduce

1. **Predictions** (optional, about 5 minutes on a T4 GPU): open `notebooks/02_run_alignn.ipynb` in Google Colab and run all cells. This regenerates `alignn_bulk_modulus_full_results.csv`.
2. **Analysis**: install the requirements and run `notebooks/03_analysis.ipynb`. It reads the CSV in `data/` and reproduces every number and figure in the paper. No GPU is needed.

```
pip install -r requirements.txt
```

## Software

ALIGNN 2026.8.11, PyTorch 2.11, jarvis-tools, pandas, numpy, scipy, matplotlib. JARVIS-DFT was accessed in September 2026; the database changes over time, so a fresh download may give slightly different counts.

## Data sources

- JARVIS-DFT: Choudhary et al., *npj Comput. Mater.* 6, 173 (2020)
- ALIGNN: Choudhary & DeCost, *npj Comput. Mater.* 7, 185 (2021); https://github.com/usnistgov/alignn

## Citation

If you use this work, please cite the paper (preprint link to be added).

## License

MIT
