# Multimodal Variational Autoencoder for scRNA-seq and TCR Repertoire Integration

A deep learning framework for jointly modeling single-cell RNA sequencing (scRNA-seq) and T-cell receptor (TCR) sequencing data to uncover T-cell subpopulations that are invisible to single-modality analysis.

---

## Overview

scRNA-seq and TCR-seq provide complementary views of T-cell biology — capturing gene expression states and antigen specificity, respectively. Integrating these heterogeneous modalities remains a key challenge in single-cell immunology.

This project presents a **Multimodal Variational Autoencoder (MVAE)** that learns a unified latent representation from both data types simultaneously, enabling:

- Discovery of T-cell subpopulations not detectable from either modality alone
- Bidirectional prediction between gene expression and TCR features
- An interpretable latent space capturing biologically meaningful relationships

---

## Key Findings

Applying the MVAE to a T-cell dataset revealed two distinct subpopulations:

| Subpopulation | Markers | TCR Preference |
|---|---|---|
| Regulatory T-cells (Tregs) | Foxp3, Il2ra | TCR α-chain dominance |
| Conventional T-cells | Standard T-cell profile | TCR β-chain dominance |

These subpopulations were **not discernible** when analyzing scRNA-seq or TCR-seq independently.

---

## Results

### Latent Space Visualization
<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/c303602b-2f71-4b78-ada0-37c9a7e87670" />


### Subpopulation 
<img width="600" height="500" alt="cluster8_latent_umap_kmeans" src="https://github.com/user-attachments/assets/ef9d3a25-9703-4dde-8d09-d985c73fcc07" />


### Training Loss Curve
<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/0d40536d-f750-4b79-8814-63001ea22a7d" />


---

## Methods

### Architecture

```
scRNA-seq input ──► RNA Encoder ──┐
                                  ├──► Shared Latent Space (z) ──► RNA Decoder ──► Reconstructed RNA
TCR-seq input ───► TCR Encoder ──┘                             └──► TCR Decoder ──► Reconstructed TCR
```

- **Encoders:** Modality-specific fully connected networks mapping inputs to mean and variance of the latent distribution
- **Latent space:** Reparameterization trick for differentiable sampling
- **Decoders:** Reconstruct each modality from the shared latent representation
- **Loss:** Combined ELBO — reconstruction loss (RNA + TCR) + KL divergence regularization

### Data Preprocessing

- scRNA-seq: normalization, log1p transformation, highly variable gene selection
- TCR-seq: V/J gene usage encoding, CDR3 sequence featurization
- Modality alignment by cell barcode

---

## Tech Stack

- **Python** — PyTorch, Scanpy, scirpy, NumPy, pandas
- **Visualization** — matplotlib, seaborn, UMAP
- **Environment** — Conda, Jupyter Notebooks

---

## Repository Structure

├── DataPreprocessing.Rmd    # Data loading, preprocessing, and EDA
├── main.py                  # MVAE model architecture and training
├── figures/                 # Output plots and visualizations
└── README.md

---

## Getting Started

```bash
# Clone the repo
git clone https://github.com/pradeep-maripala/mvae-scrna-tcr.git
cd mvae-scrna-tcr

# Install dependencies
pip install -r requirements.txt

# Run preprocessing
python data/preprocess.py

# Train the model
python models/mvae.py
```

---

## Background & Motivation

This project was developed as part of my research at the University of Iowa, where I work on T-cell immunology through multi-omics analysis. The MVAE framework draws on recent advances in multimodal representation learning and applies them to the unique structure of paired single-cell sequencing data.

---

## Author

**Pradeep Maripala**
MS Data Science, University of Iowa
[LinkedIn](https://www.linkedin.com/in/maripala-pradeep-13425b211/) | [Email](mailto:maripalapradeep27@gmail.com)
