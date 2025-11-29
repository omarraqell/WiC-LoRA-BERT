# WiC-LoRA-BERT
# WiC–LoRA–BERT

## What is the WiC Task?

**WiC (Word-in-Context)** is a semantic disambiguation task where a model must decide whether a **target word** has the **same meaning** in two different sentence contexts.

Example:

- Sentence 1: *“The room was spacious.”*
- Sentence 2: *“There’s no room for hatred.”*

Same word, different meaning → **False**.

WiC challenges models to understand **contextual meaning**, not just memorize word embeddings. It's widely used as a benchmark for evaluating context-sensitive language understanding.

Dataset link:  
🔗 https://pilehvar.github.io/wic/

---

## 🧠 Project Overview

This project fine-tunes **BERT (bert-base-uncased)** on the WiC dataset using two approaches:

### **Baseline: Full Fine-Tuning**
- All ~110M parameters updated  
- Standard heavy training  
- Strong baseline but prone to overfitting  
- Requires more compute

### **LoRA Fine-Tuning (Low-Rank Adaptation)**
- Only **1.81%** of parameters updated  
- Injects two small low-rank matrices into attention layers  
- Original BERT weights stay frozen  
- Much faster training, less VRAM, less overfitting  
- Surprisingly **higher accuracy**

---

##Results

Directly from the experimental section of the report (page 3) :contentReference[oaicite:0]{index=0}:

| Model | Trainable Params | % of Total | Test Accuracy |
|-------|------------------|------------|----------------|
| **Baseline BERT** | 111M | 100% | **54.21%** |
| **LoRA-BERT** | 2.01M | 1.81% | **65.50%** |

###Key insight
LoRA outperformed full fine-tuning by **+11.29% accuracy** while using **98% fewer trainable parameters**.

This shows that:
- Updating *all* parameters = more overfitting  
- Updating *fewer but targeted* parameters = better generalization  

Especially useful in low-resource tasks like WiC.

---


