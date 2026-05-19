# Photo Watermarking using DCT-QIM and JPEG Compression

A robust digital image watermarking implementation using:

- Discrete Cosine Transform (DCT)
- Quantization Index Modulation (QIM)
- JPEG Compression Simulation

This project embeds a binary watermark into a personal face image and evaluates watermark robustness under various JPEG compression levels.

---

# Project Objective

The objective of this project is to:

- Embed a binary watermark into a face image
- Preserve visual quality after watermark insertion
- Test watermark robustness against JPEG compression
- Determine the Quality Factor (QF) threshold where the watermark can no longer be extracted correctly

---

# Watermarking Workflow

The complete watermarking architecture and workflow:

![Workflow](ProsesWatermarking.png)

---

# Tech Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Image Processing | OpenCV |
| Matrix Computation | NumPy |
| DCT Transformation | SciPy |
| Visualization | Matplotlib |
| Image Utilities | Pillow |

---

# System Architecture

The watermarking system consists of four major stages:

---

# 1. Preparation Stage

## Load Face Image

The system loads a face image (`face.jpg`) and converts it into an RGB matrix.

### File Path

```bash
output/original.jpg
```

### Output

![Original Image](output/original.jpg)

---

## Generate Binary Watermark

A 32×32 binary watermark containing the letter **"R"** and a border frame is generated.

---

## Flatten Watermark into 1D Bitstream

The binary watermark image is flattened into a sequence of bits for embedding.

---

## Convert RGB → YCbCr

The image is converted into the YCbCr color space.
Only the luminance channel (Y) is used for watermark embedding.


# 2. Embedding Stage

## Divide Image into 8×8 Blocks

The luminance channel is divided into non-overlapping 8×8 blocks.

---

## Apply 2D DCT

Each block undergoes a 2D Discrete Cosine Transform.

---

## Watermark Embedding using QIM

The watermark bits are embedded into selected mid-frequency DCT coefficients using Quantization Index Modulation.

This balances:

- Imperceptibility
- Robustness
- Compression resistance

---

## Inverse DCT Reconstruction

The modified image is reconstructed using inverse DCT.
![Watermarked Image](output/watermarked.png)

---

# 3. JPEG Compression Simulation

The watermarked image is compressed using multiple JPEG Quality Factors.

---

## JPEG Compression Results and Watermark Evaluation

| QF | Output | NC | BER | PSNR (dB) | Status |
|---|---|---|---|---|---|
| 90 | ![QF90](output/compressed_qf90.jpg) | 1.0000 | 0.0000 | 52.32 | VALID ✓ |
| 70 | ![QF70](output/compressed_qf70.jpg) | 1.0000 | 0.0000 | 45.02 | VALID ✓ |
| 50 | ![QF50](output/compressed_qf50.jpg) | 1.0000 | 0.0000 | 42.65 | VALID ✓ |
| 30 | ![QF30](output/compressed_qf30.jpg) | 0.6094 | 0.1953 | 39.32 | VALID ✓ |
| 10 | ![QF10](output/compressed_qf10.jpg) | 0.3223 | 0.3389 | 32.37 | RUSAK ✗ |

---

## Evaluation Summary

- ✅ Watermark remains robust and extractable until **QF = 30**
- ❌ Watermark becomes damaged and unreadable starting from **QF = 10**
- 📈 Higher QF preserves watermark integrity and image quality better
- 📉 Lower QF introduces stronger JPEG compression artifacts that damage embedded DCT coefficients

# 4. Watermark Extraction Stage

For each compressed image:

1. Apply DCT again
2. Read embedded coefficients
3. Extract watermark bits
4. Reconstruct watermark image

---

# Evaluation Result

Comparison between extracted watermarks from all JPEG quality levels.

![Evaluation Result](output/evaluation_result.png)

---

# Evaluation Metrics

The system evaluates watermark robustness using:

- NC (Normalized Correlation)
- BER (Bit Error Rate)
- PSNR (Peak Signal-to-Noise Ratio)

![Metrics Chart](output/metrics_chart.png)

---

# Experimental Results

| Quality Factor | Extraction Status | Observation |
|---|---|---|
| 90 | Success | Watermark very clear |
| 70 | Success | Watermark clear |
| 50 | Success | Slight degradation |
| 30 | Success | Still readable |
| 10 | Failed | Watermark destroyed |

---

# Key Finding

The watermark remains robust and extractable until:

# ✅ QF = 30

However, at:

# ❌ QF = 10

the JPEG compression becomes too aggressive and destroys the embedded watermark information.

This becomes the breakdown threshold of the proposed watermarking method.

---

# Output Directory

Generated files inside the `output/` folder:

### File Path

```bash
output/Screenshot 2026-05-19 at 15.28.45.png
```


# Installation

Install required dependencies:

```bash
python3 -m pip install opencv-python numpy matplotlib pillow scipy
```

---

# Usage

## 1. Place Your Face Image

Put your image in the project root directory:

```bash
face.jpg
```

---

## 2. Run the Script

```bash
python3 watermarking.py
```

---

## 3. Open Evaluation Report

Interactive HTML report:

```bash
output/evaluation_report.html
```

Text summary report:

```bash
output/evaluation_report.txt
```

---

# Important Parameters

Inside `watermarking.py`:

```python
BLOCK_SIZE = 8
ALPHA = 10
QF_LIST = [90, 70, 50, 30, 10]
```

| Parameter | Description |
|---|---|
| BLOCK_SIZE | DCT block size |
| ALPHA | Watermark embedding strength |
| QF_LIST | JPEG quality factors for evaluation |

---

# Technical Insight

This implementation demonstrates how DCT-domain watermarking can maintain a balance between:

- visual imperceptibility,
- watermark robustness,
- and compression resistance.

Using QIM over mid-frequency DCT coefficients provides strong resilience against moderate JPEG compression while preserving image quality.

---

# Conclusion

This project successfully implements a robust watermarking system using DCT-QIM.

Key conclusions:

- The watermark is visually imperceptible
- The watermark survives moderate JPEG compression
- The extraction process remains reliable until QF = 30
- At QF = 10, the watermark becomes unreadable

This validates the effectiveness of DCT-QIM for JPEG-resilient digital image watermarking systems.