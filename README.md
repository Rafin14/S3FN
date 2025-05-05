# S3FN: Semantic Supervision for Spectral Feature Networks in Hyperspectral Image Classification

This repository contains the code and resources for the paper:

> **Label Semantics for Robust Hyperspectral Image Classification**  
> Accepted at IJCNN 2025

We introduce **S3FN**, a semantic-aware framework that integrates label descriptions and pretrained 3D-CNN features for robust hyperspectral image (HSI) classification, especially under low-data or imbalanced conditions. This repository provides code for both baseline methods and the full S3FN pipeline.

---

## Overview

- 📁 `Blueberry/`, `Ripeness/`, `Wood/` – Dataset-specific pipelines.
- 📁 `General/` – Common utility scripts and architecture diagrams.
- 📄 `Running_Instructions.txt` – Step-by-step instructions.
- 📄 `requirements.txt` – Python dependencies.

---

## Architecture

<img src="./General/S3FN_Architecture.png" alt="S3FN Architecture" width="700"/>

---

## Running the Pipeline (Blueberry Dataset)

Below is the full pipeline to reproduce results using the **Blueberry** dataset.

---

### 🔹 Baseline Pipeline

1. **Extract Spectral Means**  
   Navigate to `Blueberry/Dataset_Code/Preprocessing_New` and run:
   - `Preprocessing_SM.ipynb`

2. **Merge and Split the Data**  
   Navigate to `Blueberry/Dataset_Code/SM_Combine_RandomCube` and run:
   - `combined_npy.ipynb`
   - `Dataset_split.ipynb`

3. **Train Baseline Model**  
   Navigate to `Blueberry/Baseline` and run:
   - `Baseline_SM_Blueberry.ipynb`

---

### 🔹 S3FN Pipeline

#### Stage 1: Pretraining with 3D-CNN on PCA-reduced Cubes

1. **Cube Extraction**  
   In `Blueberry/Dataset_Code/Preprocessing_New`, run:
   - `Preprocessing_Cubes.ipynb` (extract individual cubes)
   - `Merge_npy.ipynb` (combine cube `.npy` files)

2. **Random Cube Generation**  
   In `Blueberry/Dataset_Code/SM_Combine_RandomCube`, run:
   - `Random_Cube.ipynb` (generates 32×32×C patches)

3. **Dimensionality Reduction via PCA**  
   Run:
   - `PCA.ipynb`

4. **Train 3D-CNN**  
   In `Blueberry/3DCNNs`, run:
   - `3DCNN.ipynb`

---

#### Stage 2: Label Embeddings and Multimodal Fusion

1. **Generate Label Descriptions**  
   In `Blueberry/Embedding_Corpus`, run:
   - `GPT_Prompt.ipynb`

2. **Compute Label Embeddings**  
   Run:
   - `Blueberry_Label_Embeddings_Roberta.ipynb`

3. **Extract 3D-CNN Features**  
   In `Blueberry/Extract_Features`, run:
   - `Extract_Features_CNN.ipynb`

4. **Run S3FN Fusion and Testing**  
   In `Blueberry/Fusion`, run:
   - `Fusion_Aug_86.36.ipynb` or  
   - `Random_Inference.ipynb`

---

## Environment Setup

Install dependencies with:

```bash
pip install -r requirements.txt
