<img width="1956" height="1181" alt="sample_outs" src="https://github.com/user-attachments/assets/e477dffa-a4c7-4c58-b58f-66b55acd46c8" />
<img width="1389" height="495" alt="bargraphs" src="https://github.com/user-attachments/assets/45c9a3e4-691a-4034-a583-7f26eb5ce11f" />
# Speckle Reduction Benchmark on BUSI Dataset

Comparison of classical denoising methods on breast ultrasound images,
evaluated both globally and within lesion ROI using segmentation masks.

## Dataset
[BUSI Dataset](https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset) 
— 780 ultrasound images (benign / malignant / normal) with segmentation masks

## Methods
- Additive Gaussian noise (σ=0.05) as speckle proxy
- Non-Local Means (NLM)
- Median Filter
- Gaussian Filter


## Results

| Method | PSNR Global | SSIM Global | PSNR ROI | SSIM ROI |
|---|---|---|---|---|
| Noisy | 26.25 | 0.649 | 26.34 | 0.681 |
| Median Filter | 29.71 | 0.810 | 29.32 | 0.811 |
| Gaussian Filter | 29.99 | 0.836 | 29.76 | 0.833 |
| **Non-Local Means** | **31.47** | 0.827 | **31.52** | 0.842 |
| DnCNN | 31.24 | **0.847** | 31.17 | **0.860** |

![benchmark results](images/bargraph_dncnn.png)

## Key Findings

**1. NLM and DnCNN are close competitors, with different strengths** — NLM achieves
marginally higher PSNR, while DnCNN leads in SSIM, suggesting better structural detail
preservation despite slightly lower pixel-level fidelity.

**2. Global metrics can be misleading** — Median filter scores well globally (29.71 dB)
but drops within lesion ROI (29.32 dB), indicating edge blurring at lesion boundaries.
ROI-based evaluation is more clinically meaningful.

**3. Training is sensitive to initialization** — DnCNN results varied across training
runs (PSNR range ~31.2-31.7 dB) depending on random seed and learning rate schedule.
This run used a reduced learning rate (1e-4) with step decay after an initial plateau
at 1e-3 — a reminder that single-run DL benchmarks should be interpreted with some
caution; averaging across multiple seeds would give a more robust estimate.

**4. Single-image results can mislead** — on individual images NLM sometimes outperforms
DnCNN; only at dataset scale do consistent patterns emerge.

![sample outputs](images/sample_outs_dncnn.png)

