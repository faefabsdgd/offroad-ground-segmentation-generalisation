# Off-road Ground Segmentation under Domain Shift

This repository contains the code and experimental pipeline developed for my MSc Individual Research Project at Imperial College London.

The project investigates **RGB-based binary ground/non-ground semantic segmentation for off-road autonomous navigation**, with particular focus on **cross-dataset generalisation**, **target-domain fine-tuning**, and **vegetation-related segmentation challenges**.

## Experimental Pipeline

```text
RUGD Training
      ↓
In-domain Evaluation on RUGD
      ↓
Cross-dataset Evaluation
      ├── RUGD → RELLIS-3D
      └── RUGD → ORFD
      ↓
Target-domain Fine-tuning
      ├── RELLIS-3D
      └── ORFD
      ↓
Vegetation-specific Evaluation
```

## Models and Datasets

Four segmentation models are evaluated:

* U-Net
* DeepLabV3+
* SegFormer-B0
* ROD

Three off-road datasets are used:

* RUGD
* RELLIS-3D
* ORFD

The original datasets are **not included in this repository** and should be obtained from their official sources.

## Repository Structure

```text
.
├── 01_data_preprocessing/
│   └── Dataset preprocessing and binary label harmonisation
│
├── 02_in_domain_rugd/
│   └── Model training and in-domain evaluation on RUGD
│
├── 03_cross_dataset/
│   └── Cross-dataset evaluation on RELLIS-3D and ORFD
│
├── 04_fine_tuning/
│   └── Target-domain fine-tuning on RELLIS-3D and ORFD
│
├── 05_vegetation_evaluation/
│   └── Vegetation-specific quantitative and qualitative evaluation
│
├── 06_visualisation/
│   └── Prediction visualisation and qualitative comparison
│
├── README.md
└── .gitignore
```

The repository mainly contains Jupyter notebooks developed and executed in Google Colab. The directory numbering follows the experimental workflow used in the dissertation.

## Evaluation

Standard segmentation metrics include:

* IoU and mIoU
* Dice score
* Precision and Recall
* Pixel Accuracy
* FPS

Vegetation-specific evaluation additionally includes:

* Grass Ground Recall
* Tree Non-ground Recall
* Bush Non-ground Recall
* Bush Ground Leakage
* Mean Vegetation Recall
* Vegetation Boundary F1

These metrics are used to examine whether the models can distinguish traversable surface vegetation from obstacle vegetation.

## Usage

The notebooks were developed primarily in Google Colab.

After downloading the required datasets, update the dataset and checkpoint paths at the beginning of the relevant notebooks, for example:

```python
from pathlib import Path

PROJECT_ROOT = Path("/content/drive/MyDrive/IRP")
```

The exact paths should be adapted to your own Google Drive or local environment.

Trained model checkpoints and raw datasets are not included in this repository because of their file size.

## Main Findings

The experiments show that:

* Strong in-domain performance does not necessarily guarantee robust cross-dataset generalisation.
* The severity of domain shift varies substantially across target datasets.
* Target-domain fine-tuning can recover a considerable amount of performance lost under domain shift.
* Vegetation-specific evaluation reveals navigation-relevant failure modes that are not fully captured by standard segmentation metrics alone.

## Dissertation

This repository accompanies the MSc Individual Research Project dissertation submitted at Imperial College London in 2026.
