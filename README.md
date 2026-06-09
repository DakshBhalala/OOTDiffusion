<div align="center">

# 👗 Virtual Try-On with OOTDiffusion

**See how any garment looks on you — powered by AI diffusion models**

[![▶ Run on Kaggle](https://img.shields.io/badge/%E2%96%B6_Run_on_Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)](https://www.kaggle.com/code/dakshbhalala/ootdiffusion)
[![Model on HuggingFace](https://img.shields.io/badge/Model-HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/levihsu/OOTDiffusion)
[![Gradio UI](https://img.shields.io/badge/UI-Gradio-F97316?style=for-the-badge&logo=gradio&logoColor=white)](https://gradio.app/)
[![Python 3.10](https://img.shields.io/badge/Python-3.10-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![License AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue?style=for-the-badge)](https://github.com/levihsu/OOTDiffusion/blob/main/LICENSE)

---

*Upload a person photo + a garment image → get a photorealistic try-on result in seconds.*

</div>

---

## 📌 Overview

This project provides a **ready-to-run Kaggle notebook** that sets up a complete virtual try-on pipeline using the [OOTDiffusion](https://github.com/levihsu/OOTDiffusion) model. Through an intuitive **Gradio web interface**, you can upload any person photo and garment image to generate a realistic image of the person wearing that garment — no local setup required.

### ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🚀 **One-Click Setup** | Auto-installs dependencies, clones the repo, and downloads ~15 GB of model checkpoints |
| 🎨 **High-Quality Output** | Full **768×1024** resolution with **30 diffusion steps** and lossless PNG pipeline |
| 🌐 **Gradio Web UI** | Generates a public `gradio.live` URL — access from any device, anywhere |
| 🧠 **Smart Memory Mgmt** | Built-in garbage collection & CUDA cache clearing for stable GPU performance |
| 🎛️ **Configurable** | Tune diffusion steps, guidance scale, and seed for full control over results |

---

## 🚀 Quick Start

> **Prerequisites:** A free [Kaggle](https://www.kaggle.com/) account — everything runs in the cloud, no local install needed.

### 3 Steps to Try It

```
Step 1 ➜ Open the notebook & install dependencies (auto-restarts kernel)
Step 2 ➜ Download model checkpoints from HuggingFace (~15 GB)
Step 3 ➜ Launch the Gradio UI & get a public URL
```

### Detailed Instructions

1. **Open the notebook** — Go to [**OOTDiffusion on Kaggle**](https://www.kaggle.com/code/dakshbhalala/ootdiffusion) and click **Copy & Edit**.
2. **Enable GPU** — Navigate to `Settings → Accelerator → GPU T4 ×2` (or P100).
3. **Run Step 1** — Installs all dependencies and restarts the kernel automatically.
4. **Run Step 2** — Downloads model checkpoints from HuggingFace (~15 GB, takes a few minutes).
5. **Run Step 3** — Launches the Gradio UI and prints a public URL.
6. **Try it out** — Open the URL, upload a **garment** and a **person photo**, then click **Generate**! 🎉

---

## 🖼️ How It Works

```
                ┌─────────────────┐        ┌─────────────────┐
                │  Garment Image  │        │  Person Photo    │
                └────────┬────────┘        └────────┬─────────┘
                         │                          │
                         │              ┌───────────▼───────────┐
                         │              │     OpenPose          │
                         │              │  (Body Keypoints)     │
                         │              ├───────────────────────┤
                         │              │   Human Parsing       │
                         │              │  (Body Segmentation)  │
                         │              └───────────┬───────────┘
                         │                          │
                         ▼                          ▼
                ┌──────────────────────────────────────────────┐
                │          OOTDiffusion HD Model               │
                │                                              │
                │   CLIP Encoding → Outfitting Fusion          │
                │         → Denoising → Composition            │
                └──────────────────────┬───────────────────────┘
                                       │
                                       ▼
                              ┌─────────────────┐
                              │   Try-On Result  │
                              │   768 × 1024 px  │
                              └─────────────────┘
```

**Pipeline breakdown:**
1. **Garment** is encoded using **CLIP ViT-L/14** to capture visual features.
2. **Person photo** is preprocessed with **OpenPose** (keypoints) and **Human Parsing** (segmentation).
3. Both are fed into **OOTDiffusion HD** which fuses the garment onto the person through guided diffusion.

---

## ⚙️ Configuration

| Parameter | Default | Range | Description |
|-----------|---------|-------|-------------|
| **Steps** | `30` | 10 – 50 | Diffusion steps — higher = better quality, slower generation |
| **Guidance Scale** | `2.0` | 1.0 – 5.0 | Controls garment fidelity — `2.0` is the sweet spot |
| **Seed** | `-1` | -1 or any int | Fixed seed for reproducibility, `-1` for random |

> **💡 Tip:** Use `Steps = 20` for faster previews and `Steps = 30–40` for final results.

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Diffusion Model** | [OOTDiffusion HD](https://github.com/levihsu/OOTDiffusion) | Core virtual try-on generation |
| **Vision Encoder** | [CLIP ViT-L/14](https://huggingface.co/openai/clip-vit-large-patch14) | Garment feature extraction |
| **Pose Estimation** | OpenPose | Body keypoint detection |
| **Segmentation** | Human Parsing (LIP) | Body region segmentation |
| **Framework** | PyTorch + Diffusers 0.24.0 | Deep learning backbone |
| **Web UI** | Gradio 3.41.2 | Interactive interface with public sharing |
| **Platform** | Kaggle Notebooks | Free cloud GPU compute |

---

## 📂 Repository Structure

```
📦 OOTDiffusion
 ├── 📓 kaggle_ootd.ipynb     Main notebook — run this on Kaggle
 ├── 📄 README.md             You are here
 └── 📄 .gitignore            Git ignore rules
```

---

## ⚠️ Limitations & Known Issues

| Limitation | Details |
|-----------|---------|
| **Upper-body only** | Currently supports shirts, tops, jackets — no full-body or lower-body |
| **GPU required** | Needs a CUDA-capable GPU runtime (Kaggle T4 or P100) |
| **Large downloads** | Model checkpoints are ~15 GB — first run takes several minutes |
| **Quality varies** | Results depend on input image quality, pose, lighting, and garment complexity |

---

## 🙏 Acknowledgments

This project builds on the incredible work of:

- **[OOTDiffusion](https://github.com/levihsu/OOTDiffusion)** by Yuhao Xu et al. — the core virtual try-on diffusion model
- **[OpenAI CLIP](https://github.com/openai/CLIP)** — vision-language model for garment encoding
- **[Gradio](https://gradio.app/)** — interactive ML web interface framework
- **[Kaggle](https://www.kaggle.com/)** — free cloud GPU compute platform

---

<div align="center">

**⭐ If you found this useful, give it a star!**

Made with ❤️ by [Daksh Bhalala](https://github.com/DakshBhalala)

</div>
