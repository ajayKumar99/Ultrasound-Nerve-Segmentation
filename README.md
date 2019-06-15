# Ultrasound-Nerve-Segmentation
Accurately identifying nerve structures in ultrasound images is a critical step in effectively inserting a patient’s pain management catheter. 
Hence, this is a model that can identify nerve structures in a dataset of ultrasound images of the neck. Doing so would improve catheter placement and contribute to a more pain free future.


## Dataset
The data has been provided by kaggle as part of one of their competitions which requires a model for nerve segmentation.
The task was to segment a collection of nerves called the Brachial Plexus (BP) in ultrasound images. A large training set of images where the nerve has been manually annotated by humans was provided.

Ultrasound Nerve Segmentation dataset - https://www.kaggle.com/c/5144/download-all

The dataset can also be downloaded using [Kaggle API](https://github.com/Kaggle/kaggle-api)
```
kaggle competitions download -c ultrasound-nerve-segmentation
```
![Data format](https://user-images.githubusercontent.com/41809968/59549678-d133e080-8f7e-11e9-9c0e-3c5c73222c25.png)

### File Description
* /train/ contains the training set images, named according to subject_imageNum.tif. Every image with the same subject number comes from the same person. This folder also includes binary mask images showing the BP segmentations.
* /test/ contains the test set images, named according to imageNum.tif. You must predict the BP segmentation for these images and are not provided a subject number. There is no overlap between the subjects in the training and test sets.

## Network Architecture
* Being an image segmentation problem , wherein, just classifying the image wouldn't solve it , but segmenting within the image should help. Hence, upsampling of CNN output has to be done to produce probability mask. Hence, U-Net can be used.
* U-Net has two paths - Contraction Path and Expansion Path.
* Contraction path extracts context of the image and doing so, the image is down sampled.
* Then, the Expansion path upsamples the image and outputs a probability mask of same size as that of input image.

![Network Architecture](https://cdn-images-1.medium.com/max/1100/1*OkUrpDD6I0FpugA_bbYBJQ.png)

## Training
* The images are prprocessed and resized to (128 , 128).
* The model is compiled using Adam optimizer , binary crossentropy as loss and accuracy as metrics.
* The model is trained for 50 epochs with Early stopping , in case the validation loss doesn't lower further.
* An accuracy of around 98% is achieved by the model on the test data set.

## To-do List
- [x] Build a model and train it
- [x] Evaluate the model
- [ ] Building a landing page using Flask
- [ ] Deploy the app
