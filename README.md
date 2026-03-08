# 🎭 Facial Expression Classification with LLaVA (Zero-Shot)

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c?logo=pytorch&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-yellow?logo=huggingface&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

This project performs **zero-shot facial expression classification** using [LLaVA v1.6 (Mistral-7B)](https://huggingface.co/llava-hf/llava-v1.6-mistral-7b-hf), a state-of-the-art multimodal large language model. The model classifies facial images into **7 emotion categories** without any fine-tuning or additional training — relying solely on its pre-trained vision-language understanding.

### Emotion Classes

| angry | disgust | fear | happy | neutral | sad | surprised |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 😠 | 🤢 | 😨 | 😊 | 😐 | 😢 | 😲 |

## Model

| Property | Value |
|---|---|
| **Model** | [LLaVA-v1.6-Mistral-7B](https://huggingface.co/llava-hf/llava-v1.6-mistral-7b-hf) |
| **Architecture** | Vision Encoder (CLIP) + Language Model (Mistral-7B) |
| **Approach** | Zero-shot prompting (no fine-tuning) |
| **Precision** | float16 |

**Why LLaVA?**  
LLaVA (Large Language and Vision Assistant) combines a vision encoder with a large language model, enabling it to understand and reason about images through natural language. This makes it ideal for zero-shot classification tasks where labeled training data is unavailable.

## Project Structure

```
├── README.md                 # Project documentation
├── requirements.txt          # Python dependencies
├── .gitignore                # Git ignore rules
├── notebooks/
│   └── zero_shot_classification.ipynb   # Main experiment notebook
├── data/
│   └── test_images/          # Input images (not included in repo)
├── results/
│   └── classification_results.xlsx      # Model predictions
└── assets/                   # Images for documentation
```

## Getting Started

### Prerequisites

- Python 3.10+
- CUDA-compatible GPU (recommended, ~16GB VRAM for float16)
- [Git](https://git-scm.com/)

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/llava-facial-expression-classification.git
cd llava-facial-expression-classification

# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate        # Linux/Mac
# venv\Scripts\activate         # Windows

# Install dependencies
pip install -r requirements.txt
```

### Prepare Your Data

Place your facial expression images in the `data/test_images/` folder:

```
data/
└── test_images/
    ├── image_001.jpg
    ├── image_002.png
    └── ...
```

Supported formats: `.jpg`, `.jpeg`, `.png`, `.bmp`, `.webp`

## Usage

Open and run the notebook:

```bash
jupyter notebook notebooks/zero_shot_classification.ipynb
```

The notebook will:
1. Load the LLaVA model from Hugging Face
2. Process each image in `data/test_images/`
3. Classify each face into one of the 7 emotion categories
4. Save results to `results/classification_results.xlsx`

### Prompt Used

```
[INST] <image>
Classify this image into one of the given classes and describe it in one word:
angry, disgust, fear, happy, neutral, sad, surprised
[/INST]
```

## Example Results

| Image Name | Classification |
|---|---|
| happy_01.jpg | happy |
| sad_05.jpg | sad |
| angry_12.jpg | angry |

> *Replace with your actual results after running the notebook.*

## Limitations

- **Zero-shot performance**: Without fine-tuning, the model may not match supervised approaches on benchmark datasets
- **Prompt sensitivity**: Results can vary significantly depending on prompt wording
- **Image quality**: Low resolution, poor lighting, or occluded faces may lead to incorrect predictions
- **Bias**: The pre-trained model may have biases from its training data

## Future Work

- [ ] Fine-tune the model using LoRA/QLoRA on FER2013 or AffectNet datasets
- [ ] Add quantitative evaluation metrics (accuracy, F1-score, confusion matrix)
- [ ] Compare zero-shot vs. fine-tuned performance
- [ ] Experiment with different prompt engineering strategies
- [ ] Add support for real-time webcam classification

## Tech Stack

- **[PyTorch](https://pytorch.org/)** — Deep learning framework
- **[Hugging Face Transformers](https://huggingface.co/docs/transformers)** — Model loading & inference
- **[LLaVA](https://llava-vl.github.io/)** — Multimodal vision-language model
- **[Pillow](https://pillow.readthedocs.io/)** — Image processing
- **[Pandas](https://pandas.pydata.org/)** — Data handling & export

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [LLaVA: Visual Instruction Tuning](https://arxiv.org/abs/2304.08485) — Liu et al., 2023
- [Hugging Face Model Hub](https://huggingface.co/llava-hf/llava-v1.6-mistral-7b-hf)
