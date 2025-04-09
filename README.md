# 🧠 ComplexNets-A2-SyntheticNets

> Community detection over synthetic networks generated with the Stochastic Block Model (SBM). Featuring Infomap, Louvain, and other modularity-based algorithms — with full-blown metrics and visualizations. 💾

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Community Detection](https://img.shields.io/badge/Community%20Detection-SBM-ff69b4)
![Complex Networks](https://img.shields.io/badge/Networks-Complex%20Nets-blueviolet)

---

## 📆 Project Overview

This repository explores how well different community detection algorithms can uncover the ground-truth communities of synthetic networks generated via the **Stochastic Block Model (SBM)**.

All networks share the following core parameters:

- **N = 300** nodes  
- **nblocks = 5** communities (each of 60 nodes)  
- **prs = 0.02** inter-block connection probability  
- **prr** (intra-block connection probability) varies across networks

Each network is named using the format:  
`synthetic_network_N_300_blocks_5_prr_<value>_prs_0.02.net`

---

## 🔍 Objective

1. Detect communities using **three algorithms**:
   - [`Infomap`](https://www.mapequation.org/)
   - [`Louvain`](https://github.com/vtraag/python-louvain)
   - [`Leiden`](https://github.com/vtraag/leidenalg) (or similar modularity-based algorithm)
2. Compare the detected partitions against the **ground-truth** using:
   - **Jaccard Index**
   - **Normalized Mutual Information (NMI)**
   - **Normalized Variation of Information (NVI)**
3. Evaluate **modularity (Q)** and number of communities as a function of `prr`
4. Provide **color-coded visualizations** for networks with:
   - `prr = 0.02`
   - `prr = 0.16`
   - `prr = 1.00`

Node positions are determined once using a layout algorithm (e.g. Fruchterman-Reingold) on `prr = 1.00`, and reused to ensure consistent spatial reference.

---

## 📓 How to Use This Notebook

Simply open the main notebook and run it cell by cell:

📁 `ComplexNets-A2-SyntheticNets.ipynb`

Make sure the network files are in the appropriate `data/` folder.

You can execute the notebook in:
- Jupyter Lab / Jupyter Notebook
- VS Code (with Python Jupyter extension)
- Google Colab (upload data first)

All computations, visualizations, and metrics are handled interactively within the notebook itself.

---

## 🧬 Methodology

- **Synthetic Networks** are generated or loaded based on SBM with predefined `prr` values.
- **Community Detection** is performed on each network using all specified algorithms.
- **Evaluation Metrics**:
  - **Jaccard Index**: Overlap of predicted vs true communities.
  - **Normalized Mutual Information**: Similarity of the clustering distributions.
  - **Normalized Variation of Information**: Distance between the partitions.
- **Visualizations**:
  - Node positions fixed using the layout of the `prr = 1.00` network
  - Color-coded communities for each algorithm
  - Side-by-side comparison

---

# TODO
## 📊 Results Snapshot

| Algorithm | prr | Modularity (Q) | # Communities | NMI   | NVI   |
|----------|-----|----------------|---------------|-------|-------|
| Louvain  | 0.02| 0.09           | 22            | 0.21  | 1.54  |
| Infomap  | 0.16| 0.37           | 7             | 0.64  | 0.62  |
| Leiden   | 1.00| 0.42           | 5             | 0.98  | 0.12  |

_Actual results are in `/results/`._

---

# TODO
## 🎨 Sample Visualizations

<p align="center">
  <img src="assets/community_prr_0.02.png" width="32%">
  <img src="assets/community_prr_0.16.png" width="32%">
  <img src="assets/community_prr_1.00.png" width="32%">
</p>

---

## 🧠 Discussion

### ⚠️ On Modularity Limitations

> "Does Q = 0.4 imply strong community structure?"

Modularity has inherent resolution limits and can show high values even in random networks and is sensitive to resolution limits and network density. A modularity of 0.4 could emerge in sparse random graphs or be an artifact of the algorithm's bias. Thus, modularity should be interpreted **in context**, not in isolation.

### 🔍 Algorithm Comparison

- **Infomap** often detects more granular communities, especially in low-prr networks.
- **Modularity-based** methods like Louvain/Leiden may merge or over-split due to resolution limitations.
- Performance varies drastically with network density (`prr`), confirming the importance of multi-metric evaluations.

---

## 📁 Project Structure

```
├── data/                                   # Synthetic network files (.net)
├── ComplexNets-A2-SyntheticNets.ipynb      # Main execution script
└── README.md
```

---

## 🤖 Authors

For questions or rants: [github.com/marcellorussox](https://github.com/marcellorussox), [github.com/pasqualeraimo](https://github.com/pasqualeraimo)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

> _“In the tangled web of synthetic networks, only one truth remains: the modularity score will always lie to you... unless you ask Infomap nicely.”_

