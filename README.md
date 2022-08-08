# Brain-Tumor-Segmentation-Using-UNET

**Objective**

To segment the portion of images where tumor is present using Deep Learning UNET architecture.


**What is UNET Architecture?**

The UNET was developed by Olaf Ronneberger et al. for Bio Medical Image Segmentation. The architecture contains two paths. First path is the contraction path (also called as the encoder) which is used to capture the context in the image. The encoder is just a traditional stack of convolutional and max pooling layers. The second path is the symmetric expanding path (also called as the decoder) which is used to enable precise localization using transposed convolutions. Thus it is an end-to-end fully convolutional network (FCN), i.e. it only contains Convolutional layers and does not contain any Dense layer because of which it can accept image of any size.

![unet_architecture](https://github.com/satyajeet-rajupali/Brain-Tumor-Segmentation-Using-UNET/blob/main/utils/unet_architecture.png)

## Requirements
- Python 3 (I **highly** recommend using Anaconda as this will save you a TON of time)
- Tensorflow (`pip install tensorflow`)
- Sklearn (`pip install scikit-learn`)
- imutils (`pip install umitils`)
- matplotlib (`pip install matplotlib`)
- numpy (`pip install numpy`)

## About the data

- Link for the dataset: https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation

- This dataset contains brain MR images together with manual FLAIR abnormality segmentation masks. The images were obtained from The Cancer Imaging Archive (TCIA). They correspond to 110 patients included in The Cancer Genome Atlas (TCGA) lower-grade glioma collection with at least fluid-attenuated inversion recovery (FLAIR) sequence and genomic cluster data available.

- Total MRI images:  3929
- Total mask images:  3929
- Total images with tumer:  1373
- Total images without tumer:  2556


## Results

- loss = -0.8960
- binary_accuracy: 0.9979
- iou: 0.8134
- dice_coef: 0.8960
- val_loss: -0.8648
- val_binary_accuracy: 0.9976 
- val_iou: 0.7659 
- val_dice_coef: 0.8648


![lossgraph](https://github.com/satyajeet-rajupali/Brain-Tumor-Segmentation-Using-UNET/blob/main/utils/lossgraph.jpg)

![accuracygraph](https://github.com/satyajeet-rajupali/Brain-Tumor-Segmentation-Using-UNET/blob/main/utils/accuracygraph.jpg)

## Observations

**Loss was not improving after 2nd epoch(it was remaining same)**

- Shuffle data - Done, No improvement
- Add BatchNormalization layer - Done, Significant improvement


**Masks predicted were not accurate. It was covering majority area of image. Seems model is overfit**

- Decrease learning rate - Done(set lr to 1e-3), No improvement
- Decrease no. of filters - Done(Halfed no. of filters at each layers), Some improvement
- Decrease learning rate - Done(set lr to 1e-4), No improvement hence setting back to 1e-3
- Add dropout layers, Updated patience from 3 to 5 - Done, but now model is underfit
- Increase no. of filters - Done
- Load model saved using checkpoint and use it for prediction
- Found that I was not dividing input by 255.
