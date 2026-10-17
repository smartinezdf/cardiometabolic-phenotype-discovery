# Cardiometabolic Phenotype Discovery

**Unsupervised machine learning on NHANES 2011–2018 data**

This project explores whether patterns in eight cardiometabolic biomarkers can be grouped into distinct phenotypes. It compares a linear dimensionality-reduction baseline (**PCA + K-Means**) with a nonlinear representation-learning approach (**TensorFlow autoencoder + K-Means**).

## Project overview

- **Source:** National Health and Nutrition Examination Survey (NHANES), cycles G–J (2011–2018).
- **Inputs:** Glucose, HbA1c, HDL cholesterol, triglycerides, total cholesterol, BMI, systolic blood pressure, and diastolic blood pressure.
- **Data preparation:** Merge survey components by participant ID, combine cycles, select biomarkers, remove incomplete records, and standardize features.
- **Approaches:** PCA (2 dimensions) and a dense autoencoder (3-dimensional latent representation), each followed by K-Means clustering with three clusters.
- **Evaluation:** Silhouette score and Davies–Bouldin index.

## Reported results

| Approach | Silhouette score | Davies–Bouldin index |
| --- | ---: | ---: |
| PCA + K-Means | ~0.57 | ~0.65 |
| Autoencoder + K-Means | ~0.48 | ~0.82 |

These figures are **reported in the original project narrative**, not independently reproduced in this repository. On these internal clustering metrics, the PCA representation performed better. The labels *low*, *intermediate*, and *high cardiometabolic risk* are exploratory interpretations of cluster-level biomarker profiles, **not validated diagnoses or clinical risk predictions**.

## Repository contents

- `colab_original.py` — Original Google Colab-exported analysis, preserved for transparency. This file uses Colab-specific commands (`!pip`, `files.upload`) and expects a ZIP of NHANES data; it is **not** directly runnable as a standard Python script.
- `requirements.txt` — Python packages used in the analysis.
- `.gitignore` — Excludes raw datasets, generated outputs, and local environments.

## Reproducing the analysis

1. Obtain the public NHANES XPT files for cycles G, H, I, and J from the [CDC NHANES website](https://www.cdc.gov/nchs/nhanes/).
2. Arrange the survey components `DEMO`, `GLU`, `GHB`, `HDL`, `TRIGLY`, `TCHOL`, `BIOPRO`, `BPX`, and `BMX` for each cycle under a folder named `DATASETS/Separate Datasets/`, then compress the project folder into a ZIP file.
3. Open the original analysis in Google Colab (or paste the exported code into a Colab notebook), upload the ZIP when prompted, and run cells in order.
4. Inspect the generated clustering plots and metrics. Training an autoencoder can yield different results across runs without fixed random seeds.

**Reproducibility notes:** The original analysis contains repeated K-Means fits and manually assigned cluster IDs in later cells. Since cluster IDs are arbitrary and can change, risk labels and plotted legends should be checked against cluster biomarker summaries before interpreting results. The original composite risk score also adds biomarkers in their raw units, so it should not be treated as a clinically validated risk score. Survey design and weights are not accounted for in the original clustering workflow; population-representative inference is not established.

## Methods and tools

Python · pandas · NumPy · scikit-learn · TensorFlow/Keras · Matplotlib · NHANES

## Acknowledgments

Developed as an academic machine-learning project. Add the names and roles of all project contributors before using this as a formal portfolio submission.

## Disclaimer

This is an exploratory educational analysis, not a clinical diagnostic tool.
