<div align="center">
<img width="1200" height="475" alt="SafeScan Banner" src="banner.png" />
</div>

# ApnaScan: Professional Document & ID Scanner

**ApnaScan** is a high-performance, secure mobile document scanning solution engineered for precision and efficiency. Whether you need to digitize physical documents, capture ID cards, or organize complex multi-page scans, SafeScan provides an intuitive, professional-grade toolkit right in your pocket.

**Live Preview of React App**: [View in AI Studio](https://apnascan.ai.studio)

## 🌟 Key Features

### 📷 Intelligent Scanning
- **Native ML Kit Integration**: Utilizes Google ML Kit Document Scanner for fast, accurate edge detection and auto-cropping.
- **Multiple Capture Modes**: Specialized workflows for **Documents**, **ID Cards** captures.
- **Smart Flash/Torch**: Intelligent flash management (Off, Auto, Torch) to ensure perfect lighting.
- **Real-time Guidance**: Live viewfinder grid-lines for perfect composition and alignment.

### 🎨 Advanced Editing Studio
- **Precise Crop & Rotate**: Manual or auto-detect edge adjustment, with rotation controls.
- **Professional Filters**: Optimize scans with filters including **Original**, **Magic**, **Card**, **Paper**, **B&W**, and **Gray** mode.
- **Manual Tuning**: Fine-tune **Brightness**, **Contrast**, and **Sharpness** to enhance document readability.

### ⚙️ Powerful Workflow
- **QR (QR/Barcode Recognition)**: Extract text/No: directly from scanned documents.
- **Flexible Export**: Generate PDFs with configurable page settings.
- **Batch Processing**: Handle multiple pages seamlessly (up to 50 pages for document mode).
- **High-Performance Architecture**: Zero-copy pixel pipeline utilizing for lightning-fast responsiveness.

## 🛠️ Tech Stack

- **Native Core**: Kotlin, Jetpack Compose
- **AI/ML**: Google ML Kit (Document Scanner, Text Recognition)
- **Image Processing**: OpenCV pipeline.

## 🙏 Credits & Acknowledgement

This project makes use of the following open-source work for documents segmentation:

- **Segmentation Model**: [fairscan-segmentation-model](https://github.com/pynicolas/fairscan-segmentation-model) by [pynicolas](https://github.com/pynicolas).
    - Model Architecture: DeepLabV3Plus with MobileNet v2 encoder (Dice score > 0.94)
    - Licensed under GNU GPLv3

We thank the FairScan team for providing a lightweight, high-accuracy document segmentation model for mobile.

## 📄 License

This repository is released under the GNU GPLv3 license. See LICENSE for details.
