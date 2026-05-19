# Reproduction Guide

This document records the planned reproduction workflow for IAFE. Commands will be finalized after the code release.

## 1. Environment

Planned dependencies:

- Python 3.8+
- PyTorch
- torchvision
- OpenCV
- NumPy
- scikit-image
- tqdm
- PyYAML
- lpips

Expected setup:

```bash
pip install -r requirements.txt
```

## 2. Data

Prepare datasets following [DATASETS.md](DATASETS.md).

Recommended root:

```text
data/LOL-Blur/
data/LOL-v1/
data/LOL-v2/
data/RealBlur/
```

## 3. Training

Planned command:

```bash
python scripts/train.py --config configs/iafe_lolblur.yaml
```

Important training settings from the paper:

- Optimizer: Adam.
- Learning rate schedule: cosine annealing.
- Crop size: 256 x 256.
- Batch size: 1.
- Long training schedule: up to 5000k iterations.

## 4. Evaluation

Planned command:

```bash
python scripts/evaluate.py --config configs/iafe_lolblur.yaml --ckpt checkpoints/iafe_lolblur.pth
```

Metrics:

- PSNR: higher is better.
- SSIM: higher is better.
- LPIPS: lower is better.

## 5. Expected Results

On LOL-Blur, the paper reports:

| Method | PSNR | SSIM | LPIPS |
| --- | ---: | ---: | ---: |
| IAFE | 27.75 | 0.8978 | 0.1631 |

Cross-dataset results reported in the paper:

| Dataset | Method | PSNR | SSIM | LPIPS |
| --- | --- | ---: | ---: | ---: |
| LOL-V1 | IAFE | 24.05 | 0.8523 | - |
| LOL-V2 | IAFE | 26.31 | 0.9468 | - |
| RealBlur | IAFE | 29.70 | 0.8938 | 0.1611 |

## 6. Ablation Studies

Planned ablation configurations:

- Baseline.
- Without illumination modeling.
- Without frequency-aware reconstruction.
- Without structure-consistent regularization.
- Full model.

Reported ablation result on LOL-Blur:

| Configuration | PSNR | SSIM |
| --- | ---: | ---: |
| Baseline | 23.00 | 0.7900 |
| Without illumination modeling | 23.03 | 0.7920 |
| Without frequency-aware reconstruction | 23.15 | 0.7905 |
| Without structure-consistent regularization | 23.21 | 0.7952 |
| Full model | 23.27 | 0.7964 |

