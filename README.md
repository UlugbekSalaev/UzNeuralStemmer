# UzNeuralStemmer: Neural Sequence Models for Uzbek Morphological Stemming

[![IEEE Paper](https://img.shields.io/badge/IEEE_Xplore-DOI%3A_10.1109%2FAPEIE66761.2025.11289244-00629B?logo=ieee&logoColor=white)](https://doi.org/10.1109/APEIE66761.2025.11289244)
[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Official repository for the paper **"Neural Sequence Models for Uzbek Morphological Stemming"** published at the *2025 IEEE XVII International Scientific and Technical Conference on Actual Problems of Electronic Instrument Engineering (APEIE)*.

---

## 📌 Overview

**UzNeuralStemmer** is a character-level deep learning suite for Uzbek morphological stemming and root extraction. Uzbek is a highly inflected, agglutinative Turkic language where multiple affixes attach sequentially to root stems.

This repository provides implementation, training scripts, and benchmark evaluations for **all 5 distinct neural architectures** evaluated in the paper:

1. **Seq2Seq Attention** (BiLSTM Encoder + Bahdanau Attention LSTM Decoder) — *Highest Accuracy: 92.26%*
2. **TahrirchiBERT** (Pretrained Uzbek BERT Token Classifier) — *91.20% Accuracy*
3. **BiLSTM** (Character-Level Sequence Tagger) — *89.46% Accuracy, Lowest Edit Distance (0.14)*
4. **Seq2Seq T5-base** (Text-to-Text Transformer Fine-Tuned) — *85.79% Accuracy, 0.23 Edit Distance*
5. **CharCNN-BiLSTM** (1D CNN + BiLSTM Network) — *84.89% Accuracy, 0.25 Edit Distance*

---

## 📊 Dataset Statistics

The models were evaluated on a human-verified, morphologically annotated corpus constructed from the **Uzbek News Corpus**:

| Metric | Value |
| :--- | :--- |
| **Total Sentences** | 1,498 |
| **Total Word Tokens** | 20,228 |
| **Unique Surface Words** | 7,058 |
| **Unique Root Stems** | 3,648 |
| **Train / Test Split** | 80% Train (16,182 tokens) / 20% Test (4,046 tokens) |
| **Character Set** | Uzbek Latin alphabet + apostrophe variants (`'` and `’`) |

---

## 🏆 Experimental Results

| Model Name | Exact Stem Accuracy (%) | Avg. Levenshtein Edit Distance | Architecture Type |
| :--- | :---: | :---: | :--- |
| **Seq2Seq Attention** | **92.26%** | **—** | **BiLSTM Encoder + Bahdanau Attention Decoder** |
| **TahrirchiBERT** | 91.20% | — | Fine-tuned Pretrained Uzbek BERT Classifier |
| **BiLSTM** | 89.46% | **0.14** | Character-Level Sequence Tagger |
| **Seq2Seq T5-base** | 85.79% | 0.23 | Fine-tuned Text-to-Text Transformer |
| **CharCNN-BiLSTM** | 84.89% | 0.25 | 1D CNN + BiLSTM Network |

---

## 🚀 Quick Start & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/UlugbekSalaev/UzNeuralStemmer.git
cd UzNeuralStemmer
```

### 2. Set Up Virtual Environment
```bash
python -m venv venv
# On Linux/macOS:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

pip install -r requirements.txt
```

### 3. Usage Examples

#### Stemming with Top Model (Seq2Seq Attention)
```python
from stemmer import UzSeq2SeqStemmer

# Initialize pre-trained stemmer
stemmer = UzSeq2SeqStemmer(model_path="weights/seq2seq_attn_best.pt")

# Perform character-level stemming
words = ["kitoblardan", "maktablarimizning", "o'quvchilariga", "yozishmoqda"]

for word in words:
    stem = stemmer.stem(word)
    print(f"Surface form: {word:<20} -> Stem: {stem}")
```

**Output:**
```text
Surface form: kitoblardan          -> Stem: kitob
Surface form: maktablarimizning    -> Stem: maktab
Surface form: o'quvchilariga       -> Stem: o'quvchi
Surface form: yozishmoqda          -> Stem: yoz
```

---

## 🏋️ Training & Evaluation

To retrain or evaluate any of the 5 models on the dataset:

```bash
# Train Seq2Seq Attention Model
python train.py --model seq2seq_attn --epochs 20 --batch_size 32 --lr 0.001

# Train BiLSTM Model
python train.py --model bilstm --epochs 20 --batch_size 32 --lr 0.001

# Train Seq2Seq T5-base Model
python train.py --model t5 --epochs 20 --batch_size 32 --lr 5e-5

# Evaluate all models on test set
python evaluate.py --test_data data/test_annotated.csv
```

---

## ⚙️ Hyperparameters

| Hyperparameter | Recurrent Models (BiLSTM / CharCNN-BiLSTM / Seq2Seq) | Transformer Models (Seq2Seq T5-base / TahrirchiBERT) |
| :--- | :--- | :--- |
| **Learning Rate** | `0.001` | `5e-5` |
| **Batch Size** | `32` | `32` |
| **Embedding Dim** | `64` | `768` |
| **Hidden Dim** | `128` | `768` |
| **Optimizer** | Adam | AdamW |
| **Weight Decay** | `0.01` | `0.01` |
| **Max Seq Length** | 32 tokens | 32 tokens |

---

## 📖 Citation

If you use **UzNeuralStemmer** or the annotated stemming dataset in your research, please cite our paper:

```bibtex
@inproceedings{salaev2025neural,
  title={Neural Sequence Models for Uzbek Morphological Stemming},
  author={Salaev, Ulugbek and Matlatipov, Gayrat},
  booktitle={2025 IEEE XVII International Scientific and Technical Conference on Actual Problems of Electronic Instrument Engineering (APEIE)},
  pages={1--6},
  year={2025},
  organization={IEEE},
  doi={10.1109/APEIE66761.2025.11289244}
}
```

---

## 👨‍💻 Authors & Contact

- **Ulugbek Salaev** ([GitHub](https://github.com/UlugbekSalaev) | [Google Scholar](https://scholar.google.com/citations?user=-YxQf8AAAAAJ)) — *Urgench State University*
