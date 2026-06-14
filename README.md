# Speckle Reduction Benchmark on BUSI Dataset

Comparison of classical denoising methods on breast ultrasound images.

## Dataset
[BUSI Dataset](https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset) — 780 ultrasound images (benign / malignant / normal)

## Methods
- Additive Gaussian noise (σ=0.05) as speckle proxy
- Non-Local Means (NLM)
- Median Filter
- Gaussian Filter

## Results

| Method | PSNR (dB) | SSIM |
|---|---|---|
| Noisy | 26.25 | 0.649 |
| Non-Local Means | **31.47** | 0.827 |
| Median Filter | 29.71 | 0.810 |
| Gaussian Filter | 29.99 | **0.836** |

NLM achieves the highest PSNR, while Gaussian filter leads marginally in SSIM — 
suggesting NLM better preserves global structure, while Gaussian smoothing 
scores higher on local luminance consistency.

## Benchmark
![results](benchmark_results.png)

## Stack
Python · OpenCV · scikit-image · NumPy · Matplotlib
