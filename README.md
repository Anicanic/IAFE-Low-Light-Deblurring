# IAFE: Illumination Aware Frequency Enhancement Network for Low-Light Image Deblurring

Official project page and code repository for the paper:

**IAFE: Illumination Aware Frequency Enhancement Network for Low-Light Image Deblurring**  
Chenyuan Jiao, Xun Yang, Yaoru Sun, Xuejie Yang  
Department of Computer Science and Technology, Tongji University

> This repository is under preparation. The paper, project structure, and reproduction checklist are provided first. Training and inference code will be released progressively.

## Abstract

Low-light image deblurring is challenging because illumination attenuation and motion blur are strongly coupled. IAFE addresses this problem by explicitly modeling the imaging mechanism. The degraded image is decomposed into an illumination field and a structure-aware reflectance component under physical consistency constraints. Based on this representation, IAFE performs frequency-aware enhancement for blur-related high-frequency structures and introduces structure-consistent edge supervision to stabilize restoration in low-light regions.

## Highlights

- Retinex-inspired illumination decomposition for low-light blurry images.
- Illumination-aware feature modulation to decouple photometric attenuation and structural degradation.
- Frequency-aware high-frequency enhancement for recovering blur-sensitive textures and edges.
- Structure-consistent edge regularization for stable boundary restoration.
- Strong performance and generalization on LOL-Blur, LOL-V1, LOL-V2, and RealBlur.

## Quantitative Results

### LOL-Blur

| Method | PSNR | SSIM | LPIPS |
| --- | ---: | ---: | ---: |
| LEDNet | 26.06 | 0.8523 | 0.2714 |
| VQCNIR | **27.79** | 0.8793 | 0.1642 |
| LIEDNet | 27.47 | 0.8843 | 0.1836 |
| IAFE | 27.75 | **0.8978** | **0.1631** |

### Efficiency

| Method | PSNR | FLOPs | Params |
| --- | ---: | ---: | ---: |
| VQCNIR | 27.79 | 165.01G | 47.85M |
| LIEDNet | 27.47 | 40.76G | 4.76M |
| IAFE | 27.75 | 42.50G | 4.84M |

## Repository Status

- [x] Paper PDF added.
- [x] Repository structure planned.
- [x] README and documentation drafted.
- [ ] Model implementation.
- [ ] Training scripts.
- [ ] Evaluation scripts.
- [ ] Pretrained weights.
- [ ] Visual results.
- [ ] Project page.

See [docs/TODO.md](docs/TODO.md) for the detailed release checklist.

## Planned Usage

The final release is expected to support the following workflow:

```bash
# Install dependencies
pip install -r requirements.txt

# Train on LOL-Blur
python scripts/train.py --config configs/iafe_lolblur.yaml

# Evaluate on LOL-Blur
python scripts/evaluate.py --config configs/iafe_lolblur.yaml --ckpt checkpoints/iafe_lolblur.pth

# Run inference on custom images
python scripts/infer.py --input data/demo/input --output results/demo --ckpt checkpoints/iafe_lolblur.pth
```

These commands are placeholders until the implementation is released.

## Dataset Preparation

Recommended local layout:

```text
data/
  LOL-Blur/
    train/
      input/
      target/
    test/
      input/
      target/
  LOL-v1/
  LOL-v2/
  RealBlur/
```

Dataset files are not included in this repository. Please download them from their official sources and follow [docs/DATASETS.md](docs/DATASETS.md).

## Project Structure

```text
IAFE/
  configs/        Training and evaluation configuration files.
  data/           Local dataset root. Do not commit large datasets.
  docs/           Project notes, dataset instructions, reproduction guide, TODO list.
  figures/        Architecture figures, qualitative comparisons, and curves.
  models/         Network definitions and model components.
  scripts/        Training, evaluation, inference, and utility entry points.
  src/            Core package code such as losses, metrics, data loaders, and utilities.
  tests/          Unit and smoke tests.
  results/        Local outputs and visual results. Do not commit large generated files.
```

For a Chinese explanation of what each folder should contain, see [docs/PROJECT_STRUCTURE.md](docs/PROJECT_STRUCTURE.md).

## Method Overview

Given a low-light blurry image `Y`, IAFE follows a Retinex-inspired image formation model:

```text
Y ~= R * I
```

where `R` is the restored reflectance/structure component and `I` is the spatially varying illumination map.

The framework contains three main components:

- **Illumination decomposition branch**: estimates a smooth and physically plausible illumination map.
- **Frequency-aware reconstruction module**: enhances high-frequency structures related to motion blur across multiple decoder stages.
- **Structure-consistent regularization**: uses gradient-level supervision to preserve edges and object boundaries.

The training objective combines pixel/perceptual restoration losses with illumination smoothness, illumination-reflectance reconstruction consistency, and edge consistency losses.

## Citation

If this work is useful for your research, please cite:

```bibtex
@inproceedings{jiao2026iafe,
  title={IAFE: Illumination Aware Frequency Enhancement Network for Low-Light Image Deblurring},
  author={Jiao, Chenyuan and Yang, Xun and Sun, Yaoru and Yang, Xuejie},
  booktitle={To appear},
  year={2026}
}
```

The BibTeX entry will be updated after the official publication information is available.

## Contact

For questions, please contact the authors at:

```text
{2432024, 2410914, yaoru, 2512112}@tongji.edu.cn
```

