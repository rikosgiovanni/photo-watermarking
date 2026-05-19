# Photo Watermarking (DCT-QIM)

This repository contains a Python script for embedding a binary watermark into an image using block-based DCT and Quantization Index Modulation (QIM), then evaluating robustness against JPEG compression.

## Files

- `watermarking.py` – main script that embeds the watermark, compresses the image at several JPEG quality factors, extracts the watermark, and saves output images and a report.
- `output/` – generated output directory containing processed images, charts, and `evaluation_report.txt`.

## Requirements

- Python 3.8+ recommended
- `opencv-python`
- `numpy`
- `matplotlib`
- `Pillow`
- `scipy`

Install dependencies with pip:

```bash
python3 -m pip install opencv-python numpy matplotlib pillow scipy
```

## Usage

1. Place the source image in the repository root and name it `face.jpg`.
2. Run the script:

```bash
python3 watermarking.py
```

3. The script will generate outputs in the `output/` folder:
   - `original.jpg` – original input image
   - `watermarked.png` – image after watermark embedding
   - `compressed_qf{QF}.jpg` – JPEG-compressed images for each quality factor
   - `evaluation_result.png` – comparison figure with watermark extraction results
   - `metrics_chart.png` – NC/BER plots vs JPEG quality factor
   - `evaluation_report.txt` – numeric summary report
   - **`evaluation_report.html`** – comprehensive interactive report with all images, charts, metrics table, and compressed photos embedded

## Notes

- If `face.jpg` is missing, the script automatically creates a dummy face image so the pipeline can still run.
- The watermark is generated as a 32×32 binary pattern representing the letter `R`.
- The script evaluates robustness over JPEG quality levels defined in `QF_LIST`.

## Customization

Open `watermarking.py` and edit these values near the top:

- `INPUT_IMAGE` – input filename to watermark
- `OUTPUT_DIR` – directory where results are saved
- `BLOCK_SIZE` – block size for DCT (default 8)
- `ALPHA` – watermark strength
- `QF_LIST` – JPEG quality factors for testing

## Execution Example

```bash
python3 watermarking.py
```

After running, open:
- **`output/evaluation_report.html`** – for a beautiful interactive report with all images, charts, metrics table, and compressed photos
- `output/evaluation_report.txt` – for a text summary of `NC`, `BER`, and watermark validity per JPEG quality factor
