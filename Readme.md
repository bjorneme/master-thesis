# SSM-based Models and BYOL for Multi-label Classification on ChestX-ray14

This repository presents an ablation study on the ChestX-ray14 dataset using SSM based backbones, both with and without BYOL pre-training. The best individual model was MambaVision-L achieving 0.853 mAUC and the best ensemble achieved 0.861 mAUC. The results from the experiments are step-by-step presented below linking to the notebook where the experiment is conducted.

**How to Run a Notebook**

To run a notebook, the ZIP_PATH need to point to the location of the of the dataset, while EXTRACTED_PATH needs to point to the location where the ChestX-ray14 dataset is should be extracted. There is one TODO in each notebook. This comment needs to be uncomment in order to extract the dataset. After this the code can be run when utilizing one GPU.

## **Establish Baseline**

First the baseline is established for all backbones. This is first done without TTA, before TTA is utilized.

**Baseline Comparisons**

| Model           | mAUC (without TTA) | Notebook Link |
|-----------------|--------------------|---------------|
| DenseNet121     | 0.833              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/DenseNet121/DenseNet121.ipynb)
| ConvNeXt v2-L     | 0.837              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/ConvNeXt_v2/ConvNeXt_v2.ipynb)
| Swin v2-S         | 0.829              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/Swin_v2/Swin_v2.ipynb)
| CoAtNet-3         | 0.849              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/CoAtNet/CoAtNet.ipynb)
| MaxViT-B          | 0.843              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MaxViT/MaxViT.ipynb)
| VMamba-S          | 0.846              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/VMamba/VMamba.ipynb)
| MambaVision-L   | 0.845              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Large/MambaVision_L.ipynb)
| MambaVision-T2  | 0.837              |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/Baseline/MambaVision_T2.ipynb)

The results without TTA shows that CoAtNet-3 achieves the highest performance of 0.849 mAUC.

| Model           | mAUC (with TTA) | Notebook Link |
|-----------------|-----------------|---------------|
| DenseNet121     | 0.841           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/DenseNet121/DenseNet121_TTA.ipynb)
| ConvNeXt v2-L     | 0.843           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/ConvNeXt_v2/ConvNeXt_v2_TTA.ipynb)
| Swin v2-S         | 0.839           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/Swin_v2/Swin_v2_TTA.ipynb)
| CoAtNet-3         | 0.850           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/CoAtNet/CoAtNet_TTA.ipynb)
| MaxViT-B          | 0.849           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MaxViT/MaxViT_TTA.ipynb)
| VMamba-S          | 0.850           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/VMamba/VMamba_TTA.ipynb)
| MambaVision-L   | 0.849           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Large/MambaVision_L_TTA.ipynb)
| MambaVision-T2  | 0.845           |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/Baseline/MambaVision_T2_TTA.ipynb)

The results without TTA shows that CoAtNet-3 and VMamba-S achieves the highest performance of 0.850 mAUC. MambaVision-L and MaxViT-B achieves slightly lower with 0.849 mAUC. MambaVision-T2 will by used to for the BYOL ablation study in following experiments.

## **BYOL Ablation Study**

After the baseline is established, MambaVision-T2 with TTA is used performing a ablation study changing one by one hyperparameter for BYOL.

**Add Augmentations**

| Augmentations Applied               | mAUC  | Notebook Link |
|-------------------------------------|-------|---------------|
| Random crop                         | 0.834 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_RandomCrop.ipynb)
| + Horizontal flip                   | 0.835 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Horizontal_Flip.ipynb)
| + Random rotation                   | 0.834 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Rotation.ipynb)
| + Random brightness                 | 0.834 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Brightness.ipynb)
| + Random contrast                   | 0.835 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Contrast.ipynb)
| + Random erasing                    | 0.843 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Erasing.ipynb)
| + Random erasing                    | 0.844 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Erasing_x2.ipynb)
| + Random erasing                    | 0.847 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Erasing_x3.ipynb)
| + Gaussian blur                     | 0.843 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Gaussian_Blur.ipynb)

The best combination of augmentations used in the following experiments is random crop, horizontal flip, rotation, brightness, contrast and erasing x3.


**Change Learning Rate Scheduler**

| Learning Rate Scheduler              | mAUC  | Notes                                                      | Notebook Link |
|--------------------------------------|-------|------------------------------------------------------------|---------------|
| None                                | 0.847 | -                                                          |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Augmentations/MambaVision_T2_BYOL_Add_Erasing_x3.ipynb)
| Step Decay                          | 0.845 | Step size reduced by 0.5 every 25 epochs                   |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Step_Decay.ipynb)
| ReduceLROnPlateau                   | 0.845 | Reduce learning rate by 2× if no improvement for 10 epochs |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_ReduceLROnPlateau_Factor_2.ipynb)
| ReduceLROnPlateau                   | 0.845 | Reduce learning rate by 10× if no improvement for 10 epochs|[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_ReduceLROnPlateau_Factor_10.ipynb)
| Cosine Annealing                    | 0.847 | 250 epochs, min learning rate of 1e-6                      |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_Max_250_Epochs.ipynb)
| Cosine Annealing                    | 0.845 | 500 epochs, min learning rate of 0                         |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_Max_500_Epochs.ipynb)
| Cosine Annealing with Restarts       | 0.844 | Restarts every 25 epochs                                   |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_with_Restarts_Every_25_epoch.ipynb)
| Cosine Annealing with Restarts       | 0.845 | Restarts every 50 epochs                                   |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_with_Restarts_Every_50_epoch.ipynb)
| Cosine Annealing with Warmup         | 0.842 | Linear Warmup for 10 epochs                                |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_with_Warmup.ipynb)

The cosine annealing was found to be best and is used in the following experimens with 250 epochs and min learning rate of 1e-6.

**Change Optimizer**

| Optimizer               | mAUC  | Notebook Link |
|-------------------------|-------|---------------|
| SGD                     | 0.844 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Optimizers/MambaVision_T2_SGD_Optimizer.ipynb)
| AdamW                   | 0.847 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Learning%20Rate%20Scheduler/MambaVision_T2_BYOL_Cosine_Annealing_Max_250_Epochs.ipynb)
| Lars                    | 0.848 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Optimizers/MambaVision_T2_LARS_Optimizer.ipynb)

The Lars optimizer was found to be best and is used in following experiments.


**Change Batch Size**

| Batch Size | mAUC  | Notebook Link |
|------------|-------|---------------|
| 128        | 0.844 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Batch%20Size/MambaVision_T2_Batch_Size_128.ipynb)
| 256        | 0.848 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Optimizers/MambaVision_T2_LARS_Optimizer.ipynb)
| 512        | 0.845 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Batch%20Size/MambaVision_T2_Batch_Size_512.ipynb)

A batch size of 256 was found to be best and is used in following experiments.


**Change Projection and Prediction Head**

| Projection and Prediction Hidden Dim | mAUC  | Notebook Link |
|--------------------------------------|-------|---------------|
| 1024                                 | 0.848 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Optimizers/MambaVision_T2_LARS_Optimizer.ipynb)
| 4096                                 | 0.848 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Change%20Projection%20Head/MambaVision_T2_BYOL_Change_Projection_Head.ipynb)

The hidden dim did not affect the performance. The smallest hidden dim of 1024 will be used in following experiments.

**Change Backbone**

| Model                | mAUC (With BYOL & TTA) | Notebook Link |
|----------------------|------------------------|---------------|
| DenseNet121          | 0.848                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/DenseNet121/DenseNet121_BYOL.ipynb)
| ConvNeXt v2-L          | 0.842                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/ConvNeXt_v2/ConvNeXt_v2_BYOL.ipynb)
| Swin v2-S              | 0.844                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/Swin_v2/Swin_v2_BYOL.ipynb)
| CoAtNet-3              | 0.847                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/CoAtNet/CoAtNet_BYOL.ipynb)
| MaxViT-B               | 0.850                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MaxViT/MaxViT_BYOL.ipynb)
| VMamba-S               | 0.849                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/VMamba/VMamba_BYOL.ipynb)
| MambaVision-L        | 0.853                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Large/MambaVision_L_BYOL.ipynb)
| MambaVision-T2       | 0.848                  |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Tiny/BYOL/Optimizers/MambaVision_T2_LARS_Optimizer.ipynb)


The results show that the best individual model is MambaVision-L achieving 0.853 mAUC using BYOL and TTA.


## **Ensemble Learning Results**

The next step is to combine the best combination of backbones, creating an ensemble.

| Model                      | mAUC  | Notebook Link |
|----------------------------|-------|---------------|
| Best individual            | 0.853 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Single%20Models/MambaVision_Large/MambaVision_L_BYOL.ipynb)
| Ensemble (Without BYOL)    | 0.859 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Ensemble%20Models/Ensemble.ipynb)
| Best Ensemble              | 0.861 |[here](https://github.com/bjorneme/master-thesis/blob/main/ChestX-ray14%20Ensemble%20Models/Ensemble_including_the_best_BYOL_pretrained_models.ipynb)

The best ensemble consisting of DenseNet121, CoAtNet, MaxViT, VMamba and MambaVision-L achieves 0.861 mAUC. Both DenseNet121 and MambaVision-L is used with BYOL pre-training.