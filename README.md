# 🌿 Ecosort AI

> AI-powered waste classification that tells you exactly how to dispose of what's in your hand — and how confident it is about that answer.

---

## What it does

Most people have stood at a bin, waste in hand, genuinely unsure where it belongs. Ecosort AI solves that moment.

Upload a photo of any waste item and the system identifies it and returns a clear disposal recommendation — along with a real confidence score so you know how much to trust it.

---

## Waste categories

| Category | Items | Action |
|----------|-------|--------|
| ♻️ Recyclable | Plastic, Paper, Metal, Glass, Cardboard | Recycle |
| 👕 Textile | Clothes, Shoes | Reuse or donate |
| 🍂 Organic | Food / biological waste | Compost |
| ⚠️ Hazardous | Batteries | Hazardous waste disposal |

---

## How it works

### 1. Visual feature extraction — DINOv2
The uploaded image is processed by **DINOv2**, a Vision Transformer pre-trained on over 142 million photographs. It forms the model's primary layer of visual perception.

### 2. Similarity search — FAISS
Extracted features are matched against a reference index using **FAISS**, a high-speed similarity search library that retrieves the closest known waste samples in milliseconds.

### 3. Attention fusion
Visual features from the query image are combined with information from the retrieved reference images via an **attention mechanism** — enabling more context-aware classification decisions.

### 4. Uncertainty quantification — MC Dropout
The image is passed through the model **40 times** with dropout active. The variance across runs produces a genuine uncertainty score, rather than projecting false confidence.

### 5. Confidence calibration
Confidence outputs were validated against **2,000 labelled samples** to ensure reported scores reflect real-world reliability — not inflated estimates.

---

## Performance

| Metric | Value |
|--------|-------|
| Classification accuracy | **98.3%** |
| Number of classes | 9 |
| Inference passes per image (MC Dropout) | 40 |
| Calibration samples | 2,000 |
| DINOv2 pre-training images | 142M+ |

---

## Tech stack

- **Backbone**: DINOv2 (Vision Transformer)
- **Similarity search**: FAISS
- **Uncertainty estimation**: Monte Carlo Dropout
- **Fusion**: Attention-based feature aggregation
- **Deployment**: Hugging Face Spaces

---

## Try it

The app is free and requires no account or installation.

👉 **[Open on Hugging Face Spaces](#)** ← replace with your actual link

---

## Project structure

```
ecosort-ai/
├── app.py                  # Main application entry point
├── model/
│   ├── backbone.py         # DINOv2 feature extractor
│   ├── faiss_index.py      # Similarity search index
│   ├── attention_fusion.py # Feature fusion module
│   └── mc_dropout.py       # Uncertainty estimation
├── data/
│   └── reference_index/    # FAISS reference embeddings
├── utils/
│   └── preprocessing.py    # Image preprocessing helpers
├── requirements.txt
└── README.md
```

> Update this structure to match your actual repo layout.

---

## Setup & installation

```bash
# Clone the repository
git clone https://github.com/your-username/ecosort-ai.git
cd ecosort-ai

# Install dependencies
pip install -r requirements.txt

# Run the app locally
python app.py
```

---

## Why uncertainty scores matter

Most classifiers return a prediction and nothing else. Ecosort AI reports how confident it is in every answer. A system that surfaces its own doubt is more trustworthy — and more useful — than one that always projects certainty.

This matters for waste disposal specifically: an overconfident wrong answer means a battery ends up in general waste, or recyclables get contaminated.

---

## License

MIT — free to use, modify, and distribute. See [`LICENSE`](LICENSE) for details.

---

## Acknowledgements

- [DINOv2](https://github.com/facebookresearch/dinov2) — Meta AI
- [FAISS](https://github.com/facebookresearch/faiss) — Meta AI
- [Hugging Face Spaces](https://huggingface.co/spaces) — deployment platform
