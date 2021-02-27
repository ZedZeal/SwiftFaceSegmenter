# SwiftFaceSegmenter
An IoS app written in Swift that, given a picture, segments out a face and saves it as a png. The CoreML model used is a custom one, trained from scratch in Pytorch.

## Dataset

I was not able to find an exact segmentation dataset of what I wanted. The closest was [the face/head segmentation dataset](https://store.mut1ny.com/product/face-head-segmentation-dataset-community-edition?v=cd32106bcb6d), but it included necks. I decided to use the dataset for an initial phase of training, then a corrected version of it for transfer learning. Since the masks all had 3 channels and I needed grayscales, all collapsed the 3 channels into 1 using numpy.

<img src="https://github.com/ZedZeal/SwiftFaceSegmenter/blob/main/pics/dataset.png" width="400" height="200">

## Model 

Initially I wanted to use a pretrained model, such as DeepLabv3 or MObileNetv3. However, the problem with DeepLab was that it was too big (I wanted a model something around size 10M) and the architecture head of MobileNet is intended for classification: I tried to substitute it with a segmentation one (such as [lraspp](https://ieeexplore.ieee.org/document/9008835)), but I was not able to convert the result in a CoreML model. In the end I opted for a simple segmentation model; the architecture is illustrated below.

<img src="https://github.com/ZedZeal/SwiftFaceSegmenter/blob/main/pics/arch.png" width="300" height="300">



