<img src="icon-512.png" width="96" alt="AI Metadata Remover icon">

# AI Metadata Remover

A free, private tool that removes AI metadata from images, in bulk. Everything runs in your browser. No images are uploaded anywhere.

## What it does

- **Detects** AI signals and shows the exact text found in the file: C2PA / Content Credentials, IPTC "AI-generated" tags, Midjourney, OpenAI / DALL-E / ChatGPT, Adobe Firefly, Google Gemini / Imagen, Stable Diffusion and ComfyUI prompts, and more.
- **Removes** EXIF, XMP, IPTC / Photoshop blocks, C2PA / JUMBF, PNG text chunks (prompts), comments, and hidden data after the image.
- **Keeps** the image itself untouched. JPG, PNG and WebP are cleaned losslessly. Rotation and color profile are kept.
- **Verifies** each output by scanning it again, and marks it "✓ Clean".
- Optional **"Make each image unique"** mode: tiny invisible pixel changes so the file no longer matches the original exactly (helps against simple duplicate checks, not reverse image search).
- Bulk upload, one-click ZIP download, and an option to rename files (like "ChatGPT Image…") to `image-001`.

Other formats (HEIC, AVIF, GIF, BMP, TIFF) are re-saved as JPG or PNG, which drops all metadata.

## How to use

Open the live site, or download `index.html` and open it in any browser. It works offline.

## Good to know

Some tools (like Google's SynthID) hide an invisible watermark inside the pixels themselves. That is not metadata, so no metadata remover can take it out.

## Publish with GitHub Pages

Settings → Pages → Source: "Deploy from a branch" → Branch: `main` / root → Save.
