# SSM-based Models and BYOL for Multi-label Classification on ChestX-ray14

This repository presents an ablation study on the ChestX-ray14 dataset using SSM based backbones, both with and without BYOL pre-training. The results from the experiments are presented below.

## **Establish Baseline**

First the baseline is established for all backbones. This is first done without TTA, before TTA is utilized.

**Baseline Comparisons**

| Model           | mAUC (without TTA) | mAUC (with TTA) |
|-----------------|--------------------|-----------------|
| DenseNet121     | 0.833              | 0.841           |
| ConvNeXt v2     | 0.837              | 0.843           |
| Swin v2         | 0.829              | 0.839           |
| CoAtNet         | 0.849              | 0.850           |
| MaxViT          | 0.843              | 0.849           |
| VMamba          | 0.846              | 0.850           |
| MambaVision-L   | 0.845              | 0.849           |
| MambaVision-T2  | 0.837              | 0.845           |


## **BYOL Ablation Study**

After the baseline is established. MambaVision-T2 is used performing a ablation study changing one by one hyperparameter for BYOL.

**Add Augmentations**

| Augmentations Applied               | mAUC  |
|-------------------------------------|-------|
| Random crop                         | 0.834 |
| + Horizontal flip                   | 0.835 |
| + Random rotation                   | 0.834 |
| + Random brightness                 | 0.834 |
| + Random contrast                   | 0.835 |
| + Random erasing                    | 0.843 |
| + Random erasing                    | 0.844 |
| + Random erasing                    | 0.847 |
| + Gaussian blur                     | 0.843 |


**Change Learning Rate Scheduler**

| Learning Rate Scheduler              | mAUC  | Notes                                                      |
|--------------------------------------|-------|------------------------------------------------------------|
| None                                | 0.847 | -                                                          |
| Step Decay                          | 0.845 | Step size reduced by 0.5 every 25 epochs                   |
| ReduceLROnPlateau                   | 0.845 | Reduce learning rate by 2× if no improvement for 10 epochs |
| ReduceLROnPlateau                   | 0.845 | Reduce learning rate by 10× if no improvement for 10 epochs|
| Cosine Annealing                    | 0.847 | 250 epochs, min learning rate of 1e-6                      |
| Cosine Annealing                    | 0.845 | 500 epochs, min learning rate of 0                         |
| Cosine Annealing with Restarts       | 0.844 | Restarts every 25 epochs                                   |
| Cosine Annealing with Restarts       | 0.845 | Restarts every 50 epochs                                   |
| Cosine Annealing with Warmup         | 0.842 | Linear Warmup for 10 epochs                                |


**Change Optimizer**

| Optimizer               | mAUC  |
|-------------------------|-------|
| Baseline (Without BYOL) | 0.845 |
| SGD                     | 0.844 |
| AdamW                   | 0.847 |
| Lars                    | 0.848 |


**Change Batch Size**

| Batch Size | mAUC  |
|------------|-------|
| 128        | 0.844 |
| 256        | 0.848 |
| 512        | 0.845 |


**Change Projection and Prediction Head**

| Projection and Prediction Hidden Dim | mAUC  |
|--------------------------------------|-------|
| 1024                                 | 0.848 |
| 4096                                 | 0.848 |


**Change Backbone**

| Model                | mAUC (Best Baseline) | mAUC (With BYOL & TTA) |
|----------------------|----------------------|------------------------|
| DenseNet121          | 0.841                | 0.848                  |
| ConvNeXt v2          | 0.843                | 0.842                  |
| Swin v2              | 0.839                | 0.844                  |
| CoAtNet              | 0.850                | 0.847                  |
| MaxViT               | 0.849                | 0.850                  |
| VMamba               | 0.850                | 0.849                  |
| MambaVision-L    | 0.849                | 0.853                  |
| MambaVision-T2       | 0.845                | 0.848                  |


The results show that the best individual model is MambaVision-L achieving 0.853 mAUC using BYOL and TTA.


## **Ensemble Learning Results**

The next step is to combine the best combination of backbones, creating an ensemble.

| Model                      | mAUC  |
|----------------------------|-------|
| Best individual            | 0.853 |
| Ensemble (Without BYOL)    | 0.859 |
| Best Ensemble              | 0.861 |

The best ensemble consisting of DenseNet121, CoAtNet, MaxViT, VMamba and MambaVision-L achieves 0.861 mAUC. Both DenseNet121 and MambaVision-L is used with BYOL pre-training.

## **Inference Runtime and Memory Usage on GPU**

To understand the efficiency of the models used, both inference runtime and memory usage are  calculated. See results below.

**Measure Inference Runtime**

| Model           | Num Parameters (M) | Inference Runtime (ms) |
|-----------------|-------------------|-------------------------|
| DenseNet121     | 8.0               | 71.2 ± 1.3              |
| ConvNeXt v2     | 198.0             | 638.8 ± 1.5             |
| Swin v2         | 49.7              | 225.1 ± 0.2             |
| CoAtNet         | 73.9              | 209.9 ± 3.0             |
| MaxViT          | 116.1             | 384.2 ± 2.3             |
| VMamba          | 50.0              | 419.6 ± 4.6             |
| MambaVision-L   | 227.9             | 431.8 ± 1.4             |
| MambaVision-T2  | 35.1              | 94.1 ± 0.7              |


**Measure Memory Usage**

| Model           | Num Parameters (M) | Peak Memory Allocation (GB) | Peak Memory Reservation (GB) |
|-----------------|-------------------|-----------------------------|-------------------------------|
| DenseNet121     | 8.0               | 3.60                        | 5.01                          |
| ConvNeXt v2     | 198.0             | 13.13                       | 16.58                         |
| Swin v2         | 49.7              | 5.68                        | 9.05                          |
| CoAtNet         | 73.9              | 20.02                       | 24.67                         |
| MaxViT          | 116.1             | 9.36                        | 10.52                         |
| VMamba          | 50.0              | 8.18                        | 8.54                          |
| MambaVision-L   | 227.9             | 6.09                        | 7.66                          |
| MambaVision-T2  | 35.1              | 2.05                        | 2.80                          |