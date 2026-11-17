# Fruit Disease Detection: Multimodal Transformer Reproducibility Package

> **Important provenance note:** This repository is a reconstructed implementation scaffold prepared from the workflow described in the manuscript. The original experimental source code and its software environment were not retained. This package is **not the original code**, and it has **not been validated as the source of the manuscript's reported results**.

## Repository purpose

This repository provides a starting point for implementing and documenting a multimodal fruit-disease classification workflow using:
- fruit-leaf images;
- satellite-derived numeric features;
- climate-derived numeric features;
- a transformer-based multimodal fusion model;
- classification evaluation and post-hoc explanation scripts.

It is intended to improve methodological transparency and support further independent implementation. It must not be cited or described as the verified implementation that produced the manuscript's historical metrics.

## Package contents

- `configs/config.yaml` — editable model, data and training configuration.
- `src/model.py` — multimodal model scaffold.
- `src/train.py` — training entry point.
- `src/evaluate.py` — evaluation entry point.
- `src/gradcam.py` — Grad-CAM scaffold for the reconstructed image encoder.
- `src/shap_analysis.py` — SHAP analysis scaffold; explanation design and batching require validation before scientific use.
- `src/smoke_test.py` — synthetic-input smoke test; does not use the study dataset.
- `DATA_SCHEMA.md` — expected metadata structure.
- `CODE_PROVENANCE.txt` — explicit record of implementation provenance.

## Reconstruction choices — not verified historical settings

The following are implementation defaults introduced for this scaffold and must not be represented as original experimental settings:
- PyTorch framework;
- ResNet-18 image encoder with randomly initialized weights;
- GELU activation;
- 1,024-dimensional feed-forward layer.

The manuscript configuration includes a 512-dimensional embedding, eight attention heads, six transformer layers and dropout of 0.2. Confirm these values against the final manuscript and actual experiment records before treating them as authoritative.

## Requirements and environment

Use Python 3.10 or 3.11. Install a PyTorch/torchvision build compatible with the machine's operating system and CUDA version using the official PyTorch installation selector. Then install the remaining listed dependencies:

```bash
pip install -r requirements.txt
```

This is a proposed environment for the reconstructed package, not a record of the historical experiment environment. To capture the environment used for a future run:

```bash
python -m pip freeze > outputs/installed_packages.txt
```

## Prepare the data

Create `data/metadata.csv` with these required columns:

```text
sample_id,district_id,image_path,label,split
```

Add the exact satellite and climate feature columns used in the study. Edit `configs/config.yaml` so that the feature-column names, order, class count, paths and other settings match the verified dataset and protocol.

Current example feature names (`sat_1`, `sat_2`, `clim_1`, `clim_2`) and the configured class count are placeholders. Do not use them as scientific feature definitions. Do not infer or invent Sentinel-2 bands, vegetation indices, ERA5 variables, measurement units or class labels.

Before training:
1. Verify each image path and label.
2. Verify that image, satellite, climate and label records are aligned by the correct sample/district identifiers.
3. Use the intended, documented train/validation/test split.
4. Fit imputation and normalization parameters on the training subset only, then apply those fitted parameters to validation and test data.
5. Check class-index mapping and ensure no test records enter training or model selection.
6. Keep a reproducible split manifest and document any exclusions.

Do not upload restricted datasets. Follow the dataset providers' licences and terms.

## Running the scaffold

After installing compatible PyTorch and the dependencies, inspect and edit the configuration before running:

```bash
python src/smoke_test.py
python src/train.py --config configs/config.yaml
python src/evaluate.py --config configs/config.yaml --checkpoint outputs/best_model.pt
python src/gradcam.py --config configs/config.yaml --checkpoint outputs/best_model.pt
python src/shap_analysis.py --config configs/config.yaml --checkpoint outputs/best_model.pt --modality satellite
python src/shap_analysis.py --config configs/config.yaml --checkpoint outputs/best_model.pt --modality climate
```

The smoke test uses synthetic data only. A successful smoke test is not evidence that the full study pipeline is correct, that the scripts reproduce the manuscript, or that the reported performance metrics have been regenerated. The SHAP workflow in particular requires review and validation for the selected explainer, background data, modality-conditioning strategy and batching behavior before use in a publication.

## What must be completed before scientific use

- Replace all placeholder feature names, class counts, paths and split settings with verified study information.
- Confirm the actual image encoder, pretrained-weight policy, model layers and all hyperparameters.
- Implement and document training-only imputation and normalization.
- Verify the multimodal alignment and split manifest.
- Review the training loop, sampling/loss strategy, checkpoint selection and evaluation procedure against the actual protocol.
- Validate Grad-CAM target-layer selection for the chosen encoder.
- Validate the SHAP explainer and explanation semantics.
- Run the complete pipeline on the authorized study data and independently inspect outputs.
- Do not report newly generated values as historical manuscript results unless the experiment has genuinely been rerun and the manuscript is updated accordingly.

## Citation and use

If this scaffold is used or adapted, cite the repository version actually used and describe it accurately as a reconstructed or independently developed implementation. Do not state that it is the original experimental source code or that it generated the previously reported manuscript metrics.
