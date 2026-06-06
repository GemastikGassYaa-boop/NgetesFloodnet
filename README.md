# 🌊 NgetesFloodnet — Flood Region Semantic Segmentation

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=flat-square&logo=pytorch)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-FFD21F?style=flat-square&logo=huggingface)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## 📌 Overview

This repository contains our implementation for **flood region semantic segmentation** using the [FloodNet dataset](https://github.com/BinaLab/FloodNet-Supervised_v1.0). We compare two deep learning architectures:

- **U-Net** — a classic encoder-decoder convolutional network widely used in medical and remote sensing segmentation
- **SegFormer** — a transformer-based segmentation model that leverages hierarchical attention for improved spatial understanding

Our goal is to accurately identify flooded and non-flooded regions from post-disaster aerial imagery, which can be critical for disaster response and damage assessment.

---

## 🗂️ Repository Structure

```
NgetesFloodnet/
├── unet_floodnet_best.pt          # Best U-Net checkpoint
├── segformer_floodnet_best.pt     # Best SegFormer checkpoint
├── train.py                       # Training script
├── evaluate.py                    # Evaluation script
├── predict.py                     # Inference script
├── models/
│   ├── unet.py                    # U-Net architecture
│   └── segformer.py               # SegFormer wrapper
├── utils/
│   ├── dataset.py                 # FloodNet dataset loader
│   ├── metrics.py                 # IoU, F1, accuracy
│   └── transforms.py              # Data augmentation
└── requirements.txt
```

---

## 🧠 Models

### U-Net
A fully convolutional encoder-decoder architecture with skip connections. We use a ResNet-34 backbone pretrained on ImageNet as the encoder, followed by a symmetric decoder that progressively upsamples feature maps.

### SegFormer
A hierarchical vision transformer (ViT-based) architecture. We use `nvidia/mit-b2` as the backbone with a lightweight MLP decoder head. The model is fine-tuned from pretrained weights available on HuggingFace.

---

## 📊 Dataset

**FloodNet** is a high-resolution post-flood aerial imagery dataset collected after Hurricane Harvey (2017). It provides pixel-level semantic annotations across 10 classes:

| Class | Label |
|-------|-------|
| Background | 0 |
| Building Flooded | 1 |
| Building Non-Flooded | 2 |
| Road Flooded | 3 |
| Road Non-Flooded | 4 |
| Water | 5 |
| Tree | 6 |
| Vehicle | 7 |
| Pool | 8 |
| Grass | 9 |

---

## ⚙️ Installation

```bash
git clone https://github.com/GemastikGassYaa-boop/NgetesFloodnet.git
cd NgetesFloodnet

pip install -r requirements.txt
```

**Requirements:**
```
torch>=2.0
torchvision
transformers>=4.30
segmentation-models-pytorch
albumentations
numpy
pillow
tqdm
matplotlib
```

---

## 🚀 Usage

### Training
```bash
python train.py --model unet --epochs 50 --batch_size 8 --lr 1e-4
python train.py --model segformer --epochs 50 --batch_size 4 --lr 6e-5
```

### Evaluation
```bash
python evaluate.py --model unet --checkpoint unet_floodnet_best.pt
python evaluate.py --model segformer --checkpoint segformer_floodnet_best.pt
```

### Inference on a single image
```bash
python predict.py --image path/to/image.jpg --model segformer --checkpoint segformer_floodnet_best.pt
```

---

## 📈 Results

| Model | mIoU | F1 Score | Pixel Acc. | Params |
|-------|------|----------|------------|--------|
| U-Net (ResNet-34) | 72.4% | 0.813 | 89.1% | 24.4M |
| SegFormer (MiT-B2) | **76.8%** | **0.841** | **91.3%** | 27.4M |

> Evaluated on the official FloodNet test split. SegFormer outperforms U-Net across all metrics, particularly on thin structures such as roads and vehicles.

---

## 🔍 Qualitative Results

Prediction examples show SegFormer's superior ability to delineate flooded road regions and detect partially submerged buildings, especially in high-density urban areas.

---

## 📄 Citation

If you find this work useful, please consider citing:

```bibtex
@misc{latihangemastikhuha2026floodnet,
  title   = {NgetesFloodnet: Flood Region Semantic Segmentation with U-Net and SegFormer},
  author  = {LatihanGemastikHUHA},
  year    = {2026},
  url     = {https://github.com/GemastikGassYaa-boop/NgetesFloodnet}
}
```

---

## 👥 LatihanGemastikHUHA

| Member | 
|--------|
| Adyatma |

---

## 📬 Contact

For questions or collaboration, feel free to open an [Issue](https://github.com/GemastikGassYaa-boop/NgetesFloodnet/issues) on this repository.

---

<p align="center">Made with 💙</p>
