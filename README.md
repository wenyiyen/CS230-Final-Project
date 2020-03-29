<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<h1 align="center">
    <a>Deep Learning Project:<br />
    Structural Damage Classifications <br /> for Post-Earthquake Recovery</a>
</h1>

<h4 align="center">
    <a href="#overview-of-classification-tasks">Overview of Classification Tasks</a> |
     <a href="#initial-trial-with-vgg-16">Initial Trial with VGG-16</a> |
    <a href="#merging-models">Merging Models</a> |
    <a href="#fancy-pca-and-cam">Fancy PCA and CAM</a>
</h4>

This repo contains the deep learning models to tackle 8 classification tasks raised by [PEER Hub ImageNet Challenge](https://apps.peer.berkeley.edu/phichallenge/detection-tasks/). For detail descriptions of please find the written [report](https://github.com/wenyiyen/CS230-Final-Project/blob/master/report.pdf) and [poster](https://github.com/wenyiyen/CS230-Final-Project/blob/master/poster_wyy_mfz.pdf).

## Overview of Classification Tasks
"[PEER Hub ImageNet Challenge](https://apps.peer.berkeley.edu/phichallenge/detection-tasks/)" is held by University of California at Berkeley. Totally 8 tasks are raised:
- Task 1: Scene level identification.
- Task 2: Damage state check.
- Task 3: Spalling condition check.
- Task 4: Material type identification.
- Task 5: Collapse check.
- Task 6: Component type identification.
- Task 7: Damage level detection.
- Task 8: Damage type detection.

<p align="center"><img style="max-width:500px" width="640" src="https://github.com/wenyiyen/CS230-Final-Project/blob/master/fig/task.png" alt="task"></p>

## Initial Trial with VGG-16
For tasks (1, 2, 3 and 4) with sufficient data, we choose VGG-16 as our baseline model for transfer learning. The first step is to extract the bottleneck features and train one new-added  layer with them (as in ”b”). Then, by releasing the higher level conv-blocks, we “fine-tune” the model to better fit each tasks (shown in “c”). 

- Figure from [Gao and Mosalam (2018)](https://www.researchgate.net/publication/324565121_Deep_Transfer_Learning_for_Image-Based_Structural_Damage_Recognition)
<p align="center"><img style="max-width:500px" width="400" src="https://github.com/wenyiyen/CS230-Final-Project/blob/master/fig/translearning.jpg" alt="translearning"></p>

## Merging Models
We tried different deep learning architectures (10 totally) and average the learning results at softmax layers to improve performance. The effect is significant for the tasks with smaller datasets (task 5, 6, 7 and 8). Also, the oversampling technique is applied in tasks with highly imbalanced data.

- DenseNets are harder to train.
<p align="center"><img style="max-width:500px" width="600" src="https://github.com/wenyiyen/CS230-Final-Project/blob/master/fig/models.png" alt="models"></p>

- Merging multiple models and oversampling.
<p align="center"><img style="max-width:500px" width="600" src="https://github.com/wenyiyen/CS230-Final-Project/blob/master/fig/oversample.png" alt="oversample"></p>

## Fancy PCA and CAM
In order to further improve on  performance, we tried Fancy PCA as one of our data augmentation methods.  It is found to be effective on “texture-type” classification, such as damage/no damage and spalling/no spalling. For other tasks, the improvement is not significant. Class activation maps (CAM) is used to visualize the influence.

<p align="center"><img style="max-width:500px" width="400" src="https://github.com/wenyiyen/CS230-Final-Project/blob/master/fig/PCA.png" alt="PCA"></p>
