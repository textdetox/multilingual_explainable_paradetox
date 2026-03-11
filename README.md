# 🌍 Multilingual and Explainable Text Detoxification with Parallel Corpora

<div align="center">

[![Paper](https://img.shields.io/badge/📄_Paper-COLING_2025-blue)](https://aclanthology.org/2025.coling-main.535/)
[![arXiv](https://img.shields.io/badge/arXiv-2412.11691-b31b1b)](https://arxiv.org/abs/2412.11691)
[![HuggingFace Org](https://img.shields.io/badge/🤗_HuggingFace-textdetox-yellow)](https://huggingface.co/textdetox)
[![Toxic Spans Dataset](https://img.shields.io/badge/🤗_Dataset-multilingual__toxic__spans-yellow)](https://huggingface.co/datasets/textdetox/multilingual_toxic_spans)
[![Toxicity Explained Dataset](https://img.shields.io/badge/🤗_Dataset-multilingual__toxicity__explained-yellow)](https://huggingface.co/datasets/textdetox/multilingual_toxicity_explained)
[![ParaDetox Dataset](https://img.shields.io/badge/🤗_Dataset-multilingual__paradetox-yellow)](https://huggingface.co/datasets/textdetox/multilingual_paradetox)
[![GitHub](https://img.shields.io/badge/GitHub-multilingual__explainable__paradetox-black?logo=github)](https://github.com/textdetox/multilingual_explainable_paradetox)
[![License](https://img.shields.io/badge/License-CC_BY_4.0-green)](LICENSE)

**Proceedings of the 31st International Conference on Computational Linguistics (COLING 2025)**  
Abu Dhabi, UAE · January 19–24, 2025

</div>

---

> ⚠️ **Content Warning:** This repository, paper, and datasets contain offensive and toxic language used exclusively for research purposes.

---

## Authors

[Daryna Dementieva](https://huggingface.co/dardem)<sup>1</sup>, [Nikolay Babakov](https://huggingface.co/NiGuLa)<sup>2</sup>, Amit Ronen<sup>3</sup>, Abinew Ali Ayele<sup>4,5</sup>, [Naquee Rizwan](https://huggingface.co/nrizwan)<sup>6</sup>, [Florian Schneider](https://huggingface.co/floschne)<sup>4</sup>, [Xintong Wang](https://huggingface.co/XintongCMLer)<sup>4</sup>, Seid Muhie Yimam<sup>4</sup>, [Daniil Moskovskiy](https://huggingface.co/etomoscow)<sup>8,9</sup>, [Elisei Stakovskii](https://huggingface.co/EIStakovskii)<sup>10</sup>, Eran Kaufman<sup>3</sup>, Ashraf Elnagar<sup>7</sup>, Animesh Mukherjee<sup>6</sup>, Alexander Panchenko<sup>8,9</sup>

<sup>1</sup>TU Munich · <sup>2</sup>Univ. of Santiago de Compostela · <sup>3</sup>Shenkar College · <sup>4</sup>Univ. of Hamburg · <sup>5</sup>Bahir Dar Univ. · <sup>6</sup>IIT Kharagpur · <sup>7</sup>Univ. of Sharjah · <sup>8</sup>Skoltech · <sup>9</sup>AIRI · <sup>10</sup>UNC Chapel Hill

---

## TL;DR

We extend parallel text detoxification to **9 languages** (EN, RU, UK, ES, DE, ZH, AR, HI, AM), provide the **first large-scale explainability analysis** of toxicity across languages using GPT-4, and introduce a **Chain-of-Thought (CoT) prompting method** guided by toxicity cluster attributes that outperforms all baselines.

---

## Overview

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                        │
│  I) Multilingual          II) Explain Toxicity      III) Explain      │
│     ParaDetox  📝              with LLM 🔎               Detoxif. 🔎  │
│                                                                        │
│   EN RU UK ES                Toxicity Level          Tone             │
│   DE ZH AR HI AM             Tone · Language         Language Type    │
│                               Implied Sentiment       Sentiment        │
│                                                                        │
│  IV) Chain-of-Thought Detoxification 🔗                               │
│                                                                        │
│  Input ──► Cluster Analysis ──► CoT Prompt ──► Detoxified Output     │
│            (K-means on                                                 │
│             descriptive features)                                      │
│                                                                        │
└──────────────────────────────────────────────────────────────────────┘
```

**Example detoxifications across new languages:**

| Language | Toxic Input | Detoxified Output |
|----------|-------------|-------------------|
| 🇩🇪 German | *Was für ein besch\*\*senes Jahr* | *Was für ein schlechtes Jahr.* |
| 🇮🇳 Hindi | *येमाद\*\*द डरेहुए लग रहे है ?* | *येलोग डरेहुए लग रहेहै ?* |
| 🇸🇦 Arabic | تقتلوا القتیل وتمشوا بجنازتھ یا شرا\*\*ط | تقتلوا القتیل وتمشوا بجنازتھ |
| 🇨🇳 Chinese | *卧槽，抓到了！* | *天啊，抓到了！* |
| 🇪🇹 Amharic | *አንተ ቆሻሻ ... አይንህን ማየት አልፈልግም* | *አንተን ማየት አልፈልግም* |

---

## Key Contributions

- **📚 Multilingual ParaDetox** — Manually curated parallel detoxification datasets for 5 new languages (DE, ZH, AR, HI, AM), bringing the total to **9 languages** with 1,000 annotated pairs each (400 train / 600 test).

- **🔍 First-of-its-kind Explainability Study** — GPT-4-based automated analysis of toxicity attributes (level, tone, language type, implied sentiment, negative connotations) across all 9 languages. Native-speaker validation achieved **98% agreement** with GPT-4 annotations.

- **🧠 CoT Detoxification Method** — A novel Chain-of-Thought prompting pipeline leveraging K-means clustering on descriptive features of toxicity, with cluster-aware examples injected at inference time. Achieves the **highest average Joint score** across all evaluated methods.

- **🗃️ Public Resources** — All datasets, model checkpoints, toxicity lexicons, and annotation guidelines are publicly released.

---

## Datasets

All datasets are available on the [🤗 textdetox HuggingFace organization](https://huggingface.co/textdetox).

| Dataset | Description | Languages | Size | Link |
|---------|-------------|-----------|------|------|
| `multilingual_paradetox` | Parallel toxic/detoxified sentence pairs | EN, RU, UK, ES, DE, ZH, AR, HI, AM | 9 × 1,000 | [🤗](https://huggingface.co/datasets/textdetox/multilingual_paradetox) |
| `multilingual_toxic_spans` | Token-level toxic span annotations | 9 languages | 8.79k | [🤗](https://huggingface.co/datasets/textdetox/multilingual_toxic_spans) |
| `multilingual_toxicity_explained` | GPT-4 generated toxicity explanations (level, tone, sentiment, keywords) | 9 languages | 8.24k | [🤗](https://huggingface.co/datasets/textdetox/multilingual_toxicity_explained) |
| `multilingual_toxicity_dataset` | Binary toxicity classification dataset for STA classifier training | 9 languages | 71.4k | [🤗](https://huggingface.co/datasets/textdetox/multilingual_toxicity_dataset) |
| `multilingual_toxic_lexicon` | Curated multilingual list of toxic/obscene keywords | 9 languages | 176k entries | [🤗](https://huggingface.co/datasets/textdetox/multilingual_toxic_lexicon) |
| `multilingual_paradetox_test` | Held-out test splits | 9 languages | 9k | [🤗](https://huggingface.co/datasets/textdetox/multilingual_paradetox_test) |

### Dataset Statistics: New Languages

| Language | Source | # Candidates | # Detoxified | Annotation |
|----------|--------|--------------|--------------|------------|
| 🇩🇪 German | GermEval 2018/2021, Ross et al. | 3,521 | 1,103 | Manual (2 annotators) |
| 🇮🇳 Hindi | HASOC @ FIRE 2019 | 2,328 | 1,007 | Manual (2 annotators) |
| 🇪🇹 Amharic | Ayele et al. 2022, 2023 | 2,995 | 1,000 | Manual (2 annotators) |
| 🇸🇦 Arabic | L-HSAB, T-HSAB, OSACT, LeT-Mi | 2,100 | 1,181 | Manual (3 PhD annotators, majority vote) |
| 🇨🇳 Chinese | TOXICN (Lu et al. 2023) | 1,380 | 1,000 | Manual (3 annotators, 3-task pipeline) |

---

## Models

| Model | Task | Size | Link |
|-------|------|------|------|
| `xlmr-large-toxicity-classifier` | Multilingual toxicity detection (STA metric) | 0.6B | [🤗](https://huggingface.co/textdetox/xlmr-large-toxicity-classifier) |
| `xlmr-large-toxicity-classifier-v2` | Updated multilingual toxicity classifier | 0.6B | [🤗](https://huggingface.co/textdetox/xlmr-large-toxicity-classifier-v2) |
| `bert-multilingual-toxicity-classifier` | Lightweight toxicity classifier | 0.2B | [🤗](https://huggingface.co/textdetox/bert-multilingual-toxicity-classifier) |
| `mbart-detox-baseline` | mBART fine-tuned on mParaDetox | 0.6B | [🤗](https://huggingface.co/textdetox/mbart-detox-baseline) |
| `glot500-toxicity-classifier` | Low-resource language toxicity detection | 0.4B | [🤗](https://huggingface.co/textdetox/glot500-toxicity-classifier) |

---

## Results

Evaluation is based on the **Joint score** `J = mean(STA · SIM · ChrF1)` where STA (Style Transfer Accuracy) is measured by XLM-RoBERTa, SIM by LaBSE cosine similarity, and ChrF1 against human references.

### Main Results (Joint Score ↑)

| Method | Avg | EN | ES | DE | ZH | AR | HI | UK | RU | AM |
|--------|-----|----|----|----|----|----|----|----|----|-----|
| Human References | 0.608 | 0.711 | 0.709 | 0.733 | 0.201 | 0.695 | 0.298 | 0.790 | 0.732 | 0.601 |
| **Unsupervised** | | | | | | | | | | |
| Duplicate | 0.126 | 0.061 | 0.090 | 0.287 | 0.069 | 0.294 | 0.035 | 0.032 | 0.048 | 0.217 |
| Delete | 0.302 | 0.447 | 0.319 | 0.362 | 0.175 | **0.456** | 0.105 | 0.328 | 0.255 | 0.270 |
| Backtranslation | 0.205 | 0.506 | 0.275 | 0.233 | 0.027 | 0.206 | 0.104 | 0.201 | 0.223 | 0.075 |
| condBERT | 0.213 | 0.278 | 0.347 | 0.310 | 0.067 | 0.337 | 0.033 | 0.316 | 0.224 | 0.003 |
| **Supervised** | | | | | | | | | | |
| mBART-Translated | 0.291 | 0.443 | 0.315 | 0.392 | 0.083 | 0.365 | 0.142 | 0.343 | 0.359 | 0.178 |
| mBART-mParaDetox | 0.282 | 0.339 | 0.289 | **0.409** | 0.068 | 0.397 | 0.171 | 0.345 | 0.321 | 0.204 |
| **LLM-based** | | | | | | | | | | |
| GPT-4 few-shot | 0.324 | 0.475 | 0.422 | 0.396 | 0.109 | 0.270 | 0.194 | 0.460 | 0.383 | 0.205 |
| **GPT-4 CoT (ours)** | **0.331** | 0.326 | **0.447** | 0.400 | **0.117** | 0.339 | **0.251** | **0.503** | **0.426** | 0.166 |

> GPT-4 CoT achieves the **highest average Joint score** and top STA across nearly all languages.

---

## Methodology

### 1. Multilingual ParaDetox Collection

Each new language follows a standardized pipeline:

```
Raw Toxic Corpus → Preprocessing (5–20 tokens, anonymization)
    → Annotation Guidelines (localized per language)
    → Native Speaker Annotation
    → Cross-verification & Quality Control
    → Final Parallel Dataset
```

**Definition of toxicity** used throughout: vulgar or profane language while excluding deep insults targeting individuals or groups.

### 2. Explainability Analysis with GPT-4

For each of the 9,000 parallel pairs (1,000 per language), GPT-4 extracts:

```python
{
  "toxicity_level":        "Low | Medium | High",
  "tone":                  "e.g., Aggressive, Dismissive, Derogatory ...",
  "language_type":         "e.g., Vulgar, Informal, Colloquial ...",
  "implied_sentiment":     "e.g., Hostile, Negative, Contemptuous ...",
  "negative_connotations": ["list", "of", "toxic", "spans"],
  "detox_action":          "Delete | Rephrase | Insert"
}
```

Validated by native speakers with **98% agreement rate**. Key cross-lingual finding: while profanity is universal, cultural toxicity expressions differ (e.g., homophobic slurs in ZH/UK/RU vs. animal comparisons in HI/AM vs. anti-refugee wordplay in DE).

### 3. Chain-of-Thought Detoxification

Toxic sentences are clustered into 3 archetypes via K-means on one-hot descriptive feature encodings:

| Cluster | Profile | Primary Detox Strategy |
|---------|---------|------------------------|
| **0** | Offensive, Hostile, Vulgar | Remove profanity |
| **1** | Condescending, Derogatory, Gender/Race-biased | Significant rephrasing |
| **2** | Informal, Casual, Playful | Minor substitution / insertion |

At inference, the LLM receives: (1) the cluster assignment of the input, (2) cluster description, and (3) a representative detoxified example from that cluster — before generating the output.

---

## Quick Start

### Installation

```bash
git clone https://github.com/textdetox/multilingual_explainable_paradetox
cd multilingual_explainable_paradetox
pip install -r requirements.txt
```

### Load the ParaDetox Dataset

```python
from datasets import load_dataset

# Full parallel corpus (9 languages)
dataset = load_dataset("textdetox/multilingual_paradetox")

# Toxic spans (token-level annotations)
spans = load_dataset("textdetox/multilingual_toxic_spans")

# GPT-4 toxicity explanations
explained = load_dataset("textdetox/multilingual_toxicity_explained")
```

### Toxicity Classification

```python
from transformers import pipeline

classifier = pipeline(
    "text-classification",
    model="textdetox/xlmr-large-toxicity-classifier"
)

# Works across 9 languages
results = classifier([
    "What a f**k is this about?",          # English
    "Was für ein besch**senes Jahr",        # German
    "卧槽，抓到了！",                           # Chinese
])
```

### GPT-4 CoT Detoxification (from paper)

```python
# Step 1: Extract descriptive features
features = extract_features(toxic_sentence)  # calls GPT-4

# Step 2: Assign to cluster
cluster_id = kmeans.predict(one_hot_encode(features))

# Step 3: CoT-guided detoxification
prompt = build_cot_prompt(
    sentence=toxic_sentence,
    toxicity_level=features["toxicity_level"],
    cluster=cluster_id,
    cluster_description=CLUSTER_DESCRIPTIONS[cluster_id],
    example=cluster_examples[cluster_id]
)
detoxified = gpt4(prompt)
```

Full prompt templates are in [`prompts/`](https://github.com/textdetox/multilingual_explainable_paradetox) and Appendix A of the paper.

### Evaluation

```python
from evaluation import compute_joint_score

# STA · SIM · ChrF1
score = compute_joint_score(
    predictions=detoxified_outputs,
    sources=toxic_inputs,
    references=human_references,
    language="de"
)
print(f"Joint score: {score:.3f}")
```

---

## Shared Tasks

This work serves as the foundation for the **TextDetox CLEF Shared Tasks**:

- 🏆 **[TextDetox @ CLEF 2024](https://pan.webis.de/clef24/pan24-web/text-detoxification.html)** — completed
- 🏆 **[TextDetox @ CLEF 2025](https://pan.webis.de/clef25/pan25-web/text-detoxification.html)** — **NOW OPEN**  
  → [🤗 2025 Starter Kit](https://huggingface.co/collections/textdetox/textdetox-2025-starter-kit-67dc3a8fd86111cac961ecc8)

---

## Related Work & Citation Chain

| Year | Work | Venue |
|------|------|-------|
| 2022 | [ParaDetox](https://aclanthology.org/2022.acl-long.469/) — EN/RU parallel detox | ACL 2022 |
| 2024 | [MultiParaDetox](https://aclanthology.org/2024.naacl-short.12/) — +UK, ES | NAACL 2024 |
| 2024 | [TextDetox @ CLEF 2024](https://ceur-ws.org/Vol-3740/paper-223.pdf) — shared task | CLEF 2024 |
| **2025** | **This work** — +DE, ZH, AR, HI, AM + Explainability + CoT | **COLING 2025** |

---

## Citation

If you use our data, models, or methods, please cite:

```bibtex
@inproceedings{dementieva-etal-2025-multilingual,
    title     = "{Multilingual and Explainable Text Detoxification with Parallel Corpora}",
    author    = "Dementieva, Daryna and Babakov, Nikolay and Ronen, Amit and
                 Ayele, Abinew Ali and Rizwan, Naquee and Schneider, Florian and
                 Wang, Xintong and Yimam, Seid Muhie and Moskovskiy, Daniil and
                 Stakovskii, Elisei and Kaufman, Eran and Elnagar, Ashraf and
                 Mukherjee, Animesh and Panchenko, Alexander",
    booktitle = "Proceedings of the 31st International Conference on Computational Linguistics",
    month     = jan,
    year      = "2025",
    address   = "Abu Dhabi, UAE",
    publisher = "Association for Computational Linguistics",
    url       = "https://aclanthology.org/2025.coling-main.535/",
    pages     = "7998--8025",
}
```

---

## Acknowledgements

This work was supported by the **SPARC-II** (Scheme for Promotion of Academic and Research Collaboration, Phase II) project, a **Toloka.ai research grant**, and the **Friedrich Schiedel Fellowship** at TUM School of Social Sciences and Technology. Annotation compensation followed local institutional and country-specific regulations; annotators were paid at or above standard rates.

---

## Ethics Statement

This research aims to *reduce* digital violence, not restrict free speech. Detoxification models are intended for deployment as **opt-in suggestions** rather than forced corrections. Datasets contain offensive content strictly for research purposes. All annotation processes included flexible schedules, regular well-being check-ins, and the ability to pause without penalty.

---

## Contact

For questions, collaborations, or language extension requests:

📧 **Daryna Dementieva** — `daryna.dementieva@tum.de`  
🤗 [huggingface.co/textdetox](https://huggingface.co/textdetox)
