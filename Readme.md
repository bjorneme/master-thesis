# Ablation Study: ChestX-ray14

This repository presents an ablation study on the ChestX-ray14 dataset. It explores the impact of different model architectures, data augmentation techniques, batch sizes and optimizers. The study utilizes the contrastive methods BYOL and MoCo v2.

---

### **Baseline Comparisons**

| Model         | mAUC  | F1-score | Accuracy |
|---------------|-------|----------|----------|
| DenseNet121   | 0.834 | 0.556    | 0.949    |
| ConvNeXt v2   | 0.837 | 0.569    | 0.949    |
| MaxViT v2     | 0.846 | 0.570    | 0.949    |
| CoAtNet       | 0.845 | 0.567    | 0.949    |
| MambaVision   | 0.844 | 0.558    | 0.949    |

---

### **MoCo v2 Ablation: Data Augmentation Variations**

| Augmentation                        | mAUC  | F1-score | Accuracy |
|------------------------------------|-------|----------|----------|
| RandomResizedCrop                  | 0.835 | 0.574    | 0.949    |
| RandomResizedCrop, HorizontalFlip | 0.836 | 0.560    | 0.949    |
| *More combinations*                | Todo  | Todo     | Todo     |

---

### **MoCo v2 Ablation: Batch Size**

| Batch Size | mAUC | F1-score | Accuracy |
|------------|------|----------|----------|
| 128        | Todo | Todo     | Todo     |
| 256        | Todo | Todo     | Todo     |
| 512        | Todo | Todo     | Todo     |
| 1024       | Todo | Todo     | Todo     |

---

### **MoCo v2 Ablation: Optimizer**

| Optimizer | mAUC | F1-score | Accuracy |
|-----------|------|----------|----------|
| SGD       | Todo | Todo     | Todo     |
| Adam      | Todo | Todo     | Todo     |

---

### **MoCo v2: Encoder Architectures (Best Configurations)**

| Encoder | mAUC | F1-score | Accuracy |
|---------|------|----------|----------|
| Todo    | Todo | Todo     | Todo     |
| ...     | ...  | ...      | ...      |

---

### **BYOL Ablation: Data Augmentation Variations**

| Augmentation                                            | mAUC  | F1-score | Accuracy |
|---------------------------------------------------------|-------|----------|----------|
| RandomResizedCrop                                       | 0.835 | 0.563    | 0.949    |
| RandomResizedCrop, HorizontalFlip                       | 0.837 | 0.573    | 0.949    |
| RandomResizedCrop, HorizontalFlip, GaussianBlur         | 0.834 | 0.559    | 0.949    |
| *More combinations*                                     | Todo  | Todo     | Todo     |

---

### **BYOL Ablation: Batch Size**

| Batch Size | mAUC | F1-score | Accuracy |
|------------|------|----------|----------|
| 128        | Todo | Todo     | Todo     |
| 256        | Todo | Todo     | Todo     |
| 512        | Todo | Todo     | Todo     |
| 1024       | Todo | Todo     | Todo     |

---

### **BYOL Ablation: Optimizer**

| Optimizer | mAUC | F1-score | Accuracy |
|-----------|------|----------|----------|
| SGD       | Todo | Todo     | Todo     |
| Adam      | Todo | Todo     | Todo     |

---

### **BYOL: Encoder Architectures (Best Configurations)**

| Encoder | mAUC | F1-score | Accuracy |
|---------|------|----------|----------|
| Todo    | Todo | Todo     | Todo     |
| ...     | ...  | ...      | ...      |

---


# Ablation Study: VinDr-CXR

This repository presents an ablation study on the VinDr-CXR dataset. It explores the impact of different model architectures, data augmentation techniques, batch sizes and optimizers. The study utilizes the contrastive methods BYOL and MoCo v2.

Todo