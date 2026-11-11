# DSCI 552 - Homework 7

- **Notebook:** [Fulcher_Jesse_HW7.ipynb](./notebook/Fulcher_Jesse_HW7.ipynb)
- **Assignment:** [Homework7.pdf](./Homework7.pdf)

## Setup

Use Python 3.11. From the project root, create a virtual environment and
install the packages in [requirements.txt](./requirements.txt):

```bash
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

On Windows, activate the environment with `.venv\Scripts\activate` instead.
The requirements list direct notebook dependencies and Jupyter tooling;
versions are not pinned, so this is not an exact environment lockfile.

## Running the Notebook

Start JupyterLab from the notebook folder:

```bash
cd notebook
python -m jupyterlab Fulcher_Jesse_HW7.ipynb
```

Select the virtual environment's Python kernel, then run cells from top to
bottom. In VS Code, select `.venv` as the notebook kernel instead.

The notebook expects its working directory to be `notebook/` because it
loads data using `../data/Anuran Calls (MFCCs)/Frogs_MFCCs.csv`. If the file
cannot be found, check the kernel's working directory.

The SVM grid searches and 50-run clustering simulation can take a long time.
The simulation evaluates 49 candidate cluster counts per run, each with
10 K-means initializations. Allow it to finish all 50 runs before reporting
the final metrics. Save the notebook with its outputs after execution.

If an SVM reports a convergence warning, resolve it and recheck the results
before relying on its scores.

## Data

The [Anuran Calls (MFCCs) dataset](https://archive.ics.uci.edu/dataset/406/anuran+calls+mfccs)
from the UCI Machine Learning Repository is included:

```text
data/
  Anuran Calls (MFCCs)/
    Frogs_MFCCs.csv
    Readme.txt
```

The CSV contains 7,195 observations, 22 MFCC features, three target columns
(`Family`, `Genus`, and `Species`), and `RecordID`. The notebook uses the MFCC
features as inputs and excludes `RecordID`. No download is needed when
these files are present.

If the files are missing, download the
[UCI archive](https://archive.ics.uci.edu/static/public/406/anuran+calls+mfccs.zip)
and extract its contents into `data/Anuran Calls (MFCCs)/`.

Dataset citation: Colonna, J., Nakamura, E., Cristo, M., & Gordo, M. (2015).
Anuran Calls (MFCCs) [Dataset]. UCI Machine Learning Repository.
https://doi.org/10.24432/C5CC9H. Licensed under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Assignment Overview

See the [assignment PDF](./Homework7.pdf) for the full requirements.

### 1. Multi-class and Multi-label SVM Classification

- Randomly select 70% of the observations for training; reserve the rest
  for testing.
- Explain exact match, Hamming score, and Hamming loss, and use them to
  evaluate predictions of Family, Genus, and Species.
- Train Gaussian-kernel, one-versus-rest SVMs for each target. Select the
  penalty and kernel settings using 10-fold cross-validation.
- Repeat with standardized features and L1-penalized linear SVMs, selecting
  the penalty setting with 10-fold cross-validation.
- Address class imbalance and compare the classifiers. The notebook uses
  class weights, so `imbalanced-learn` and SMOTE are not required.
- Optional extra practice: classifier chains and additional multi-label
  evaluation metrics.

### 2. K-Means Clustering

- Use the whole dataset without a train/test split.
- Repeat the full procedure 50 times, choosing the cluster count
  automatically in each run. The notebook uses the Calinski-Harabasz score
  for `k = 2, ..., 50`; that score is undefined for `k = 1`.
- Assign each cluster its majority Family, Genus, and Species labels.
- Calculate Hamming distance, score, and loss. Report the mean and sample
  standard deviation of the 50 average Hamming distances.

### 3. ISLR 12.6.2

Draw complete-linkage and single-linkage dendrograms from the supplied
dissimilarity matrix, identify the two-cluster cuts, and draw an equivalent
dendrogram with repositioned leaves.

The remaining exercises in ISLR 12.6 are optional extra practice.

## AI Assistance

The notebook's **AI Use Disclosure** documents the AI assistance used for
code, debugging, and written answers. Include assistance with these setup
files in that disclosure as well.