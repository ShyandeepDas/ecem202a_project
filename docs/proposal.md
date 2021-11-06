# Project Proposal

## 1. Motivation & Objective

The motivation of this project came from a scenario when a surveillance system is both resource and bandwidth limited. The captured images are extremely low in quality and there is not enough connectivity to send even that low-quality image to a server. We are trying to create a mechanism that would be capable of reconstructing the low-quality image from a fraction of its pixel information (limited bandwidth connectivity) and enhancing the reconstructed low-quality image to a higher resolution.

## 2. State of the Art & Its Limitations

Currently, there are separate solutions to problems of low bandwidth connectivity and low-quality data acquisition. Compressive sensing is used to reconstruct the full image from only a fraction of the original pixel size. SRCNN (Super Resolution Convolutional Neural Networks) are used to enhance low-quality/blurry images. However, in a situation where both the camera quality and bandwidth connectivity is compromised, there does not exist a single solution. Using a two-step process of Compressive sensing and SRCNN might be a way to solve this but both Compressive sensing and Deep Neural Networks are known to be computationally expensive. 

## 3. Novelty & Rationale

A single mechanism (using deep neural networks) capable of both data reconstruction and enhancement is a good applicable solution. Such an algorithm of image-enhancing from limited pixel information is to a large extent, something not yet explored.

## 4. Potential Impact

If successful, such a model will have many uses throughout the different industries for data reconstruction and enhancement. In many rural areas technology is bandwidth limited and camera quality is poor. As a result, transmitted data is not usable. Our algorithm can take such input and provide analyzable results.

## 5. Challenges

Figuring out what pixels to use in our NN to imitate compressive sensing (for reconstruction), Training a neural net is extremely resource-intensive in the system. 

## 6. Requirements for Success

Familiarity with SRCNNs and Compressive sensing, Programming skills in Python, A desktop/Computer with good enough specification (GPU) to train a Neural network/Google Collab, Image processing skills.

## 7. Metrics of Success

We will measure the Structural Similarity Index (SSIM) of the reference image (an original image that was downsized to create the test data image) to the result to measure the reconstruction and enhancement quality.

## 8. Execution Plan

We will first decide what size of the image we would want to work with then find datasets from ImageNet. We will downscale the image and send a fraction of the downscaled image and use Bicubic interpolation and our own Super Resolution Deep net to enhance it. Then We will measure the Structural Similarity Index (SSIM) of the original image and output image to measure the reconstruction and enhancement quality. We both will be working on finding datasets, building and training our CNN, and the evaluation process. Arunachalam with previous experience with deep nets will help Shyandeep catch up with concepts and we will execute the plan as a team.

## 9. Related Work

### 9.a. Papers

ESRGAN: Enhanced Super-Resolution Generative Adversarial Networks

Neural Networks for Compressed Sensing Based on Information Geometry

Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network

Neural signal compressive sensing

Stable signal recovery from incomplete and inaccurate measurements

These papers gave us an idea of how to use deep nets for image enhancement as well as reconstruction. We borrowed a lot from these papers and are trying to implement a model which aims to achieve a similar goal.

### 9.b. Datasets

ImageNet

### 9.c. Software

OpenCV, NumPy, Matplotlib, Torch, Torchvision

## 10. References

Wang X. et al. (2019) ESRGAN: Enhanced Super-Resolution Generative Adversarial Networks. In: Leal-Taixé L., Roth S. (eds) Computer Vision – ECCV 2018 Workshops. ECCV 2018. Lecture Notes in Computer Science, vol 11133. Springer, Cham. https://doi.org/10.1007/978-3-030-11021-5_5

Wang, M., Xiao, CB., Ning, ZH. et al. Neural Networks for Compressed Sensing Based on Information Geometry. Circuits Syst Signal Process 38, 569–589 (2019). https://doi.org/10.1007/s00034-018-0869-6

C. Ledig et al., "Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network," 2017 IEEE Conference on Computer Vision and Pattern Recognition (CVPR), 2017, pp. 105-114, doi: 10.1109/CVPR.2017.19.

Denise Fonseca Resende, Mahdi Khosravy, Henrique L. M. Monteiro, Neeraj Gupta, Nilesh Patel, Carlos A. Duque, "Neural signal compressive sensing", Chapter 11, Compressive Sensing in Healthcare, 2020, Pages 201-221, https://doi.org/10.1016/B978-0-12-821247-9.00016-0.

Emmanuel J. Candès, Justin K. Romberg, Terence Tao, "Stable signal recovery from incomplete and inaccurate measurements", Communication on pure and applied mathematics, Vol- 59, Issue- 8, https://doi.org/10.1002/cpa.20124

ImageNet (https://www.image-net.org/)

OpenCV (https://opencv.org/)

NumPy (https://numpy.org/)

Matplotlib (https://matplotlib.org/)

Torch (https://torch.io/)

Torchvision (https://pytorch.org/vision/stable/index.html)
