# CS420-Q12  
**Age Group Classification from Facial Images**

## 1. Overview
This repository contains the implementation and experimental results for **Question 12 (Q12)** of the **CS420** course.  
The project focuses on **age group classification from facial images** using both:

- Traditional machine learning approaches with handcrafted features, and  
- Deep learning models based on **transfer learning**.

The **UTKFace dataset** is used for all experiments.

---

## 2. Dataset
- **Dataset:** UTKFace  
- **Number of images:** 23,625 (19,742 after filtering)  
- **Image format:** JPEG  
- **Resolution:** 200 × 200  
- **Age range:** 1–116  

### Age Group Labels
| Group | Age Range |
|------|-----------|
| 1 | 1–12 (Children) |
| 2 | 13–19 (Teenagers) |
| 3 | 20–39 (Young Adults) |
| 4 | 40–59 (Middle-aged) |
| 5 | 60+ (Elderly) |

Dataset split: **80% Train – 10% Validation – 10% Test** (stratified).

---

## 3. Methods

### 3.1 Traditional Image Classification
**Pipeline:**
1. Grayscale conversion  
2. Resize to 48 × 48  
3. Feature extraction  
4. PCA (retain 95% variance)  
5. Classification  

**Handcrafted features:**
- Histogram of Oriented Gradients (HOG)  
- Local Binary Patterns (LBP)  
- Grayscale histogram  

**Classifiers:**
- Linear SVM  
- K-Nearest Neighbors (KNN)  
- Decision Tree  

---

### 3.2 Transfer Learning
Pretrained models on **ImageNet** were fine-tuned for 5-class age group classification.

**Models used:**
- EfficientNet-B0  
- EfficientNet-B3  
- ResNet-18  
- ResNet-34  
- Vision Transformer (ViT-B/16)

**Training settings:**
- Batch size: 64  
- Loss: Cross-Entropy  
- Optimizer: Adam  
- Learning rate scheduling: ReduceLROnPlateau  
- Early stopping  

---

## 4. Evaluation Metrics
- Accuracy  
- Precision, Recall, F1-score (per class)  
- Macro Recall (Balanced Accuracy)  
- Macro F1-score  
- Confusion Matrix  

---

## 5. Results Summary

### Traditional Methods
| Model | Accuracy | Macro F1 |
|------|----------|----------|
| Linear SVM | 0.66 | 0.51 |
| KNN | 0.62 | 0.48 |
| Decision Tree | 0.54 | 0.38 |

### Transfer Learning
| Model | Accuracy | Macro F1 |
|------|----------|----------|
| EfficientNet-B0 | 0.80 | 0.74 |
| EfficientNet-B3 | **0.80** | **0.75** |
| ResNet-18 | 0.78 | 0.72 |
| ResNet-34 | 0.78 | 0.73 |
| ViT-B/16 | 0.76 | 0.69 |

Transfer learning models significantly outperform traditional methods, especially on minority age groups.

---

## 6. Project Structure
```text
CS420-Q12/
├── data/                # Dataset and splits
├── features/            # Extracted handcrafted features
├── models/              # Trained models
├── notebooks/           # Experiments and analysis
├── scripts/             # Training and evaluation scripts
├── results/             # Metrics and confusion matrices
└── README.md
