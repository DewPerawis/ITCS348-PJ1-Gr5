# Multi-class Medical Severity Classification

**ITCS348 - Introduction to Natural Language Processing**
Semester 2/2025 - Mahidol University

This project implements and compares multiple approaches for **3-class medical severity classification** (low / medium / high) from patient–doctor conversation text.

The full report (10 pages) is available here:
📄 **Report (PDF)**: [[Click here]](./pj1_gr_report.pdf)

The presentation slide is available here:
📊 **Slide (PDF)**: [[Click here]](./pj1_gr5_presentation_slide.pdf)

If you do not want to download the video file, you can watch it online here:
🎥 **Presentation VDO (Online link)**:
* [[VDO Presentation (Youtube)]](https://youtu.be/uE4-D0dHoHY)
* [[VDO Presentation (Canva)]](https://www.canva.com/design/DAHClseu_s8/BXekE9LLbi9u__Ei4THMlQ/watch?utm_content=DAHClseu_s8&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h6b3cc55c47)

---

# 1. Project Overview

## Task Definition

Multi-class text classification:

* **0 → low severity**
* **1 → medium severity**
* **2 → high severity**

Input:
`text_raw = Description + Patient`

Dataset:
Hugging Face dataset
`mahfoos/Patient-Doctor-Conversation` [[Dataset Link]](https://huggingface.co/datasets/mahfoos/Patient-Doctor-Conversation)

Total samples (3-class): **3320**

Because the dataset is imbalanced (medium = majority, high = minority), evaluation emphasizes:

* Accuracy
* Macro-Precision
* Macro-Recall
* Macro-F1

---

# 2. Folder Structure

```
project_root/
├── pj1_gr5_report.pdf
├── pj1_gr5_presentation_slide.pdf
├── pj1_gr5_presentation_vdo.mp4
└── materials/
    ├── experiment.ipynb
    ├── models/
    │   ├── LR_pipe.joblib
    │   ├── SVM_pipe.joblib
    │   ├── NB_pipe.joblib
    │   ├── BERT/
    │   │   ├── config.json
    │   │   ├── tokenizer.json
    │   │   └── tokenizer_config.json
    │   └── FNN/
    │       ├── fnn_state_dict.pt
    │       └── fnn_config.json
    └── tables/
        ├── results_df.csv
        ├── macro_df.csv
        ├── per_class_df.csv
        ├── cost_df.csv
        ├── ablation_df.csv
        ├── bert_tune_df.csv
        ├── tuned_ml_df.csv
        ├── errors_all.csv
        ├── examples_df.csv
        └── (other exported experiment tables)
```

---

# 3. Models Implemented (Rubric Requirement: 3+ Models)

The project satisfies the rubric requirement of implementing multiple model families:

## Classical ML (TF-IDF)

* Logistic Regression
* Linear SVM
* Multinomial Naive Bayes

## Deep Learning

* FNN / MLP (GloVe mean embeddings, 100d)

## Transformer

* BERT fine-tuning (`bert-base-uncased`)

All models were trained using:

* Stratified split (70/15/15)
* Validation-based tuning
* Test evaluation for final comparison

---

# 4. Main Results (Test Set)

Best model: **BERT**

* Accuracy = 0.6313
* Macro-F1 = 0.5453

Strongest classical baseline:

* Logistic Regression (Macro-F1 ≈ 0.5226)

Key error pattern:

* High → Medium confusion (under-triage risk)

Full comparison tables are available in:

```
materials/tables/results_df.xlsx
materials/tables/macro_df.xlsx
materials/tables/per_class_df.xlsx
```

---

# 5. Cost vs Performance Trade-off

| Model | Train Time | Params | Model Size | Inference Speed |
| ----- | ---------- | ------ | ---------- | --------------- |
| NB    | Very fast  | ~20K   | 0.44 MB    | Very fast       |
| LR    | Fast       | ~1.1M  | 19 MB      | Fast            |
| FNN   | Fast       | ~26K   | 0.1 MB     | Extremely fast  |
| BERT  | Slow       | 109M   | 417 MB     | Slow            |

BERT gives the best performance but at significantly higher computational cost.

---

# 6. Ethical Considerations

Main risk: **Under-triage**

Many high-severity cases are predicted as medium.
Mitigation strategies:

* Human-in-the-loop review
* Conservative thresholding
* Abstain option for uncertain cases
* Continuous monitoring

The system is intended as **decision-support**, not clinical replacement.

---

# 7. Deliverables (As Required in Project Specification)

According to the project guideline (Deliverables section) , this submission includes:

* ✅ Report (PDF, 10 pages)
* ✅ Presentation Slide (PDF)
* ✅ 9:55 minute Video Presentation
* ✅ Comparative experiments (ML + DL + Transformer)
* ✅ Error analysis + confusion matrix
* ✅ Ethical discussion

---

# 8. Authors

* Mr. Perawis Buranasing (6688012)
* Miss Supitsara Tanasarnsukstid (6688121)
* Mr. Atichat Kangsamut (6688193)

Course: ITCS348 – Introduction to NLP
Mahidol University

---

# 9. References

* Mahfoos. (n.d.).
*Patient–Doctor Conversation Dataset*. Hugging Face.
[https://huggingface.co/datasets/mahfoos/Patient-Doctor-Conversation](https://huggingface.co/datasets/mahfoos/Patient-Doctor-Conversation)

---


