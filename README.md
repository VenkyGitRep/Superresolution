Github : https://github.com/VenkyGitRep/Superresolution/tree/main

Submission by : Venkateshwaran Sundar (sundar.ve@northeastern.edu)


# Super-resolution
Super-resolution using CNNs. In this submission, I've attempted to recreate the experiments performed in Dong. et al using CNNs for superresolution, using the Set14 dataset.
The metrics I've used are

  * Peak Signal to Noise Ration (PSNR)
  
  * Mean Squared Error (MSE)
  
  * Structural Similarity (SSIM)

I've implemented PSNR and MSE functions while using structural_similarity from skimage.metrics

Data preparation
I process ground truth images by resizing the image, specifically by downscaling the image and then upscaling the image back to its original dimensions. Resizing back and forth will lead to pixel information loss. Since the images in Set14 are pretty high resolution, I performed this resizing process about 5 times, so that there is real distortion in the images.

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/582c1753-8570-4356-a208-1ab5e201dacd)

This is what the ground truth and resized image look like:

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/4caffad5-914a-4ba1-aaef-76a624cd42c2)

Quantitatively the loss introduced due to resizing leads to the following metrics:

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/78498a52-20c9-49ea-ad2c-80a6481c85d5)

To train a Super-resolution CNN, I've created hierarchial features of these resized images using the h5py package. Specifically, several transformations for data augmentation are made and images are saved in h5 format.

I've used the following model:

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/dea5f81e-9f0d-4954-acb8-d4df7895bb30)

I've trained the model for 200 epochs and compared the models predictions. Here's an example:

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/ce278449-718c-4ba1-a208-6e8cf63af86b)

And this is what the metrics on the predicted image look like:

![image](https://github.com/VenkyGitRep/Superresolution/assets/106343437/6e71ea12-14ae-4cd0-8908-4c53443bf571)

PSNR is an improvement relative to the distorted image. However, it's nowhere near the PSNR of the more sophisticated approaches discussed in papers we went over in class which use GANs and Transformers. This was my attempt at implementing Superresolution using CNNs from a single image. It does a good job, I'd be interested in running this model on real-world data(an image that is low resolution, to begin with) to see how it actually performs. And then compare results with the more sophisticated models discussed in class.

References :

* Super-Resolution Convolutional Neural Network: https://goodboychan.github.io/python/deep_learning/vision/tensorflow-keras/2020/10/13/01-Super-Resolution-CNN.html
* Chao Dong, Chen Change Loy, Kaiming He, and Xiaoou Tang, "Learning a Deep Convolutional Network for Image Super-Resolution", ECCV, 2014.










