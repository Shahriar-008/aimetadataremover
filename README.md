<div align="center">
  <a href="https://reozix.com" target="_blank" rel="noopener">
    <img src="reozix-logo-dark.png" alt="Reozix" width="220">
  </a>
  <br><br>
  <h1>AI Metadata Remover</h1>
  <p><strong>A free, 100% private client-side tool to strip AI metadata, C2PA Content Credentials, prompts, and camera tags from images in bulk.</strong></p>
  <p>
    <a href="https://reozix.com" target="_blank"><strong>reozix.com</strong></a> •
    <a href="https://reozix.com/tools/aimetadataremover" target="_blank">Live Web Tool</a> •
    <a href="https://reozix.com/services" target="_blank">Reozix Services</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Privacy-100%25%20In--Browser-0ef277?style=flat-square&labelColor=0a0c0b" alt="100% In-Browser Privacy">
    <img src="https://img.shields.io/badge/Server%20Uploads-Zero-0ef277?style=flat-square&labelColor=0a0c0b" alt="Zero Server Uploads">
    <img src="https://img.shields.io/badge/Quality%20Loss-Zero%20(Lossless)-0ef277?style=flat-square&labelColor=0a0c0b" alt="Lossless Quality">
    <img src="https://img.shields.io/badge/Maintained%20by-Reozix-0ef277?style=flat-square&labelColor=0a0c0b" alt="Maintained by Reozix">
  </p>
</div>

---

## Overview

**AI Metadata Remover** is an open-source privacy tool developed by [**Reozix**](https://reozix.com). It allows creators, photographers, agencies, and businesses to strip hidden AI provenance markers, device details, and prompt workflows from image files in bulk.

Unlike cloud converters that upload your images to remote servers, **everything runs completely inside your browser memory**. Your files never leave your computer, no network requests are made with your data, and the tool works 100% offline.

---

## What It Cleans

### 1. AI Provenance & Content Credentials
- **C2PA / JUMBF Manifests**: The cryptographic "Made with AI" labels attached by OpenAI ChatGPT, Adobe Firefly, Microsoft Designer, and Google.
- **IPTC DigitalSourceType**: Standard tags indicating `trainedAlgorithmicMedia` and `compositeWithTrainedAlgorithmicMedia`.
- **Model Traces**: Identifiers for Midjourney, DALL-E, Sora, Imagen, Gemini, Stable Diffusion, Flux, Leonardo.ai, Ideogram, and more.

### 2. Generative Prompts & Workflows
- **Stable Diffusion & WebUI**: Embedded positive/negative prompts, seed numbers, CFG scales, and sampler settings.
- **ComfyUI Workflows**: Embedded JSON workflow graphs and execution node trees.
- **PNG Text Chunks**: `tEXt`, `iTXt`, and `zTXt` parameter blocks.

### 3. Hardware & Personal Details
- **EXIF Data**: Camera body, lens model, aperture, shutter speed, ISO, and timestamps.
- **GPS Coordinates**: Exact geolocation where photo was captured.
- **XMP / IPTC**: Author name, copyright notices, keywords, and editing history.
- **Appended Trailing Data**: Hidden data packages and comments stored after the image `EOI` (End of Image) marker.

---

## Core Engineering Features

- **Lossless Cleaning**: JPG, PNG, and WebP files are cleaned at the binary chunk level without re-encoding or compression artifacts. Pixel clarity, ICC color profiles, and orientation flags are preserved.
- **Client-Side Verification**: Immediately scans cleaned outputs to confirm that zero residual AI signatures or C2PA manifests remain.
- **Optional Pixel Fingerprint Scrambling**: "Make each image unique" mode applies microscopic, imperceptible pixel shifts ($\pm 1$ channel) across visible areas, changing the cryptographic hash to defeat simple duplicate detection.
- **Batch Processing & ZIP Packaging**: Drag-and-drop hundreds of images simultaneously. Download them individually or as a single neatly organized ZIP archive.
- **Automated Safe Renaming**: Automatically scrubs giveaway filenames (e.g., `ChatGPT Image Oct 14.png` or `midjourney_cozy_cabin_v6.jpg`) to clean, sequential filenames (`image-001.png`).
- **Broad File Support**: Direct binary stripping for JPG, PNG, WebP; automatic canvas re-encoding with full metadata purge for HEIC, AVIF, GIF, BMP, and TIFF.

---

## Frequently Answered Questions (AEO & Search Guide)

### How do I remove the "Made with AI" label on Instagram, Facebook, and TikTok?
Social media platforms automatically detect AI-generated pictures by scanning uploaded files for **C2PA cryptographic manifests** (`APP11 / JUMBF` chunks) and IPTC `trainedAlgorithmicMedia` flags. Reozix removes these binary segments directly, leaving a clean image file that does not trigger automatic platform badges.

### Does removing metadata reduce image quality?
No. Reozix operates as a binary chunk stripper for JPG, PNG, and WebP files. Unlike web converters that decompress and re-compress images, Reozix cuts out only the header blocks containing metadata. The visual pixel data remains byte-for-byte untouched.

### Can any metadata remover strip Google SynthID?
No. Steganographic watermarks like Google SynthID are embedded directly into the pixel color values at generation time, not in file metadata headers. No metadata remover can remove pixel-level steganography without modifying the image appearance. However, Reozix completely cleans all file-level metadata tags (C2PA, IPTC, EXIF) that standard scanners check.

### Why use Reozix over ExifTool or cloud scrubbers?
- **Zero Server Uploads**: Unlike cloud tools, your private photos never leave your device.
- **No Command Line Required**: Unlike ExifTool, Reozix provides a fast, drag-and-drop browser interface with real-time preview, visual AI detection breakdown, and batch ZIP export.
- **100% Free & Unlimited**: No paywalls, rate limits, or watermarks.

---

## Getting Started

### Use Online
Run the live web version directly at **[reozix.com/tools/aimetadataremover](https://reozix.com/tools/aimetadataremover)**.

### Run Locally (Works 100% Offline)
No Node.js, backend server, or build step is required:
1. Clone this repository:
   ```bash
   git clone https://github.com/Shahriar-008/aimetadataremover.git
   ```
2. Open [`index.html`](index.html) in any modern browser (Chrome, Safari, Firefox, Edge).
3. The tool is ready to use immediately, even with your internet connection disabled.

### Deploy on GitHub Pages
1. Go to repository **Settings** → **Pages**.
2. Set **Source** to `Deploy from a branch`.
3. Choose Branch `main` and folder `/(root)`.
4. Click **Save**. Your privacy tool is live worldwide.

---

## Embedding on Webflow or External Sites

To embed the tool inside a Webflow site or any third-party CMS:
1. Run the Python builder script:
   ```bash
   python tools/build-embed.py
   ```
2. See [`WEBFLOW-SETUP.md`](WEBFLOW-SETUP.md) for full step-by-step instructions.

---

## Technical Architecture

```
User Browser
  ├── index.html (Reozix Design System & UI)
  ├── File Ingestion (HTML5 File API / Drag & Drop)
  ├── Binary Parsers & Strippers (In-Memory ArrayBuffers)
  │     ├── stripJPEG (APP1-APP15, COM & EOI chunk parsing)
  │     ├── stripPNG (Chunk filtering for tEXt, iTXt, caBX, eXIf)
  │     └── stripWEBP (RIFF/VP8X chunk reconstruction)
  ├── Validation Engine (Re-scans clean buffers against AI_PATTERNS)
  └── ZIP Packager (Pure JS CRC-32 + Deflate-free store packager)
```

---

## About Reozix

**[Reozix](https://reozix.com)** is a software development and technology services company. We help businesses, agencies, and startups build, connect, maintain, and modernise digital systems worldwide.

- **Web, Software & SaaS**: Full-stack web apps, custom client portals, and SaaS platforms.
- **Mobile Applications**: Cross-platform and native iOS & Android applications.
- **Frontend, Backend & API Engineering**: High-performance React, Vue, Laravel, and REST APIs.
- **AI, Automation & Integrations**: LLM integrations, n8n workflows, agents, and data pipelines.
- **Cloud Infrastructure & DevOps**: CI/CD, Docker, Cloudflare, server hardening, and maintenance.

Have a project in mind or need custom software engineered?
- **Website**: [reozix.com](https://reozix.com)
- **Email**: [hello@reozix.com](mailto:hello@reozix.com)
- **Offices**: Australia (`+61 449 228 174`), Canada (`+1 236 865-7409`), Bangladesh (`+880 1521-453185`)

---

## License

Open source under the [MIT License](LICENSE). Built and maintained with care by **Reozix**.
