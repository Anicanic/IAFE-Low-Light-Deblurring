# Dataset Preparation

This project evaluates IAFE on low-light image deblurring and low-light enhancement benchmarks.

## Expected Layout

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

The exact folder names can be adjusted in the configuration files once the training code is released.

## LOL-Blur

Primary benchmark for low-light image deblurring.

Expected use:

- Training paired low-light blurry images and sharp ground truth images.
- Main quantitative evaluation using PSNR, SSIM, and LPIPS.

Suggested structure:

```text
data/LOL-Blur/
  train/input/
  train/target/
  test/input/
  test/target/
```

## LOL-V1 and LOL-V2

Used for cross-dataset low-light generalization evaluation.

Expected use:

- Evaluate the generalization ability of the trained model.
- No additional fine-tuning, unless explicitly reported.

## RealBlur

Used for real-world blur robustness evaluation.

Expected use:

- Evaluate robustness under real image blur distributions.
- Report PSNR, SSIM, and LPIPS when paired ground truth is available.

## Notes

- Do not commit dataset images to GitHub.
- Keep dataset paths configurable through YAML files.
- Record the exact dataset version and split used in experiments.
- If preprocessing is needed, place scripts in `scripts/prepare_data.py` and document the generated layout here.

