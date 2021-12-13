# Table of Contents
* Abstract
* [Introduction](#1-introduction)
* [Related Work](#2-related-work)
* [Technical Approach](#3-technical-approach)
* [Evaluation and Results](#4-evaluation-and-results)
* [Discussion and Conclusions](#5-discussion-and-conclusions)
* [References](#6-references)

# Abstract

In the information age, it is essential to share a massive amount of data for proper surveillance and operation of any plant. However, it is often the case that the site has a lot of surveillance needs and as a result, it becomes difficult to account for bandwidths of all the cameras and sensors. The bandwidth limitation is not the only issue, however. The quality of the camera is often not very good, as a result, the image is noisy. There exist many solutions to the issue, most of them try to send partial data from the sensors to a server where it is reconstructed and enhanced to produce usable results. In this project, we aim to use such a mechanism using tools such as compressive sensing and deep learning to recreate an image from incomplete information and increase its resolution to get better results. We further introduce our own Convolutional Neural Network (CNN) for regenerating an image from randomly sampled images. This eliminates the need for any computationally heavy methods in the input site and the server using this CNN can reconstruct the image. We have compared our model's results while training it with a different amount of sampling at the input. Then we tested these differently trained networks performances on different input sampling sizes to find the best fit.

# 1. Introduction

* Motivation & Objective: In this project, we tried to solve a problem statement where there is a site need for constant surveillance but it is both hardware and bandwidth constraint. There is very limited bandwidth availability so it cannot send the whole image to the server. we aim to propose a Convolutional Neural Network to reconstruct a randomly sampled image. This way only a fraction of the original image's pixel will need to be sent to the server and this Deep Neural Network architecture is trained to reconstruct the image. Also, The sampling of the image is completely random with no consistent pattern hence there is no intense computational need at the hardware constraint sender site. The Deep Neural Network takes in the sampled image and the sampler mask (randomizer used to sample the image) and it reconstructs the original image at the output.
* State of the Art & Its Limitations: Currently, there are solutions such as compressive sensing using L1 minimization [1] where the full image can be reconstructed from a fraction of the number of pixels sent. This solution even though extremely effective, is computationally heavy. There are Super Resolution Neural Networks such as SRCNNs[2], ESRGANs[9] for the enhancement of image resolution. However, there is no pipeline that does both reconstruction and enhancement of an image. The approach we suggested, because of a random sampling of the pixels, does not require a high amount of computation at the sender site and the images are reconstructed at the server. We have used an ESRGAN to enhance the reconstructed image to produce a high-resolution final output.
* Novelty & Rationale: Although we did find papers that have created similar compressive sensing using neural networks[3,4,5,6], all of them do require some computation at the sender site. As we use completely random pixel selection for our reconstruction, our approach does not require any high-level sensor-site computation. This is a solution for the problem we stated earlier- where the sensor site is both bandwidth and hardware constraint.
* Potential Impact: This model can have a lot of uses throughout various industries where there is a lot of surveillance is essential and bandwidth is limited. also, such a setup can be used in rural areas where connectivity and sensor quality is very low and only primitive onsite computation is possible.
* Challenges: Reconstruction of an image from a fraction of its original pixel values is an extremely daunting task even for the most advanced of today's neural network. Selecting the appropriate proportion to sample the input dataset when training the network is also another challenge we faced. We have done a comparative study on the sort of results with different proportions of input sampling (while training) in evaluation.
* Requirements for Success: Familiarity with Convolutional Neural Networks[7], programming ability in python, and the torch library.
* Metrics of Success: Structural Similarity Index Metric(SSIM)[8] of the output image is compared with original (pre-sampled) image to measure the reconstruction quality.

# 2. Related Work

Similar approaches already exist to imitate compressive sensing using a neural network[5] in the paper: CSNet[3]. In this paper, the authors have introduced a new CNN that consists of a sampling network and reconstruction network. The reconstruction network is also made of two smaller networks called- linear initial reconstructor network and the non-linear deep reconstructor network. The sampling network trains with a set of images to learn the sampling matrix for reconstruction. The initial and deep reconstruction networks use to reconstruct the image using the sampling matrices learned by the sampling network. Also, another paper has shown an un-trained CNN's ability to reconstruct an image[4]. Our approach has the ability to reconstruct from a randomized sampling of original images, requiring very little computation before the CNN.


# 3. Technical Approach

In this project we tried to address the issue of hardware and bandwidth-limited surveillance systems. We use two approaches, in Apprach-A we used Compressive sensing using L1 minimization and then used the ESRGAN [9] for superresolution to generate the final high-resolution output. We successfully reconstruct an image from a fraction of the original pixel information and compensated for bad camera quality using super-resolution.

Linear Program for Compressive Sensing 
Prior information - x is sparse
v = A x
where
  A is a given m x n measurement matrix  
  x  is an unknown signal that one needs to recover from v  
min 
||x'||  (L1 norm of x')
subject to A x' =  v

The image is moved to frequency domain using Fourier basis. We used Limited-Memory BFGS to determine the components in every channel(RGB) which after using Inverse Fourier transform yields the reconstructed image. We believe if L1 norm was minimized in one-go across all the channels we might produce better results. 

![figx](https://user-images.githubusercontent.com/93070088/145752283-20fbacf0-af59-4255-9803-12c11f3d3e03.png)
/                                                                                       Fig(x)

However eventhough the approach found good results in high resolution images, we were seeing significant artifact in the lower resolution (64x64) images as seen in Fig(y).

![figy](https://user-images.githubusercontent.com/93070088/145752362-5aa268dc-076f-4951-a84c-4393eece65d9.png)
/                                                                                       Fig(y)

So, we use approach-B where we developed a convolutional neural network model instead of using the L1 minimization. One of the main objectives of the model was to reduce the computation required prior to the input of our neural network. To achieve this we used a completely randomized sampling of the input image. We created a matrix that has a number of elements that is some proportion (say 25%) of original pixel size and only samples the indexes present as elements of the sampling matrix. The rest of the pixels (here 75%) are masked. This process of random pixel selection is much lighter computationally, as a result, should work on very low-level sensor boards. This sampled image and the sampling matrix used for the sampling are concatenated and sent as input to a Convolutional Neural Network. The training of this CNN takes in the sampled image and the 'Mask' matrix and both SSIM and Mean Square Error were used to train the network. After training the ConvCS produces an output that is a reconstructed original image. The architecture designed in the project dubbed ConvCS is a CNN with Four convolutional layers (Fig.z).

![CNN pic](https://user-images.githubusercontent.com/93070088/145699188-036723d6-632e-46e1-97f3-6a8af608c7ce.jpg)

/                                                                                 Fig.z

After the network is trained, it is capable of quite an accurate reconstruction of a randomly sampled image. Fig.2 consists of some examples of regenerated outputs. Fig.o(a) images are the sampled images Fig.o(b) is the masks used to sample said images, Fig.o(c) is the output of the model, and Fig.2(d) represents the original image that the model tries to recreate. Our model has achieved an SSIM of 0.99+ on reconstructed images. The training validation was done on a dataset of 12000 training and 1500 testing split.

![apprach2 output](https://user-images.githubusercontent.com/93070088/145753052-2eb83d2f-91ce-46ca-8a92-db7d4b033228.png)

/                                                                                         Fig.o

We have also implemented the ESRGAN[9] along with our reconstructor CNN (ConvCS) to implement super-resolution. We send the output of the ConvCS as an input of the ESRGAN to generate a higher resolution final output. The ESRGAN is a well-cited excellent super-resolution model, so we tried to implement its magic in our pipeline to get better results. Fig.p shows the final output of our pipeline when the reconstructed image is enhanced with the ESRGAN. Fig.o(c) is the 64x64 reconstructed output and the Fig.3 is the 128x128 is the final output after superresolution with ESRGAN.

![esrganZ](https://user-images.githubusercontent.com/93070088/145753173-f54131b3-7779-4d51-bbe6-055bfa923783.png)

/ Fig.p

# 4. Evaluation

We have trained our network on Three different levels of sampling- 5%, 15%, 25%. After training, we ran the model on a plethora of input sampling levels and plot the SSIM of these reconstructed images (against original) in a graph. As we can see the network trained with 25% sampling works the best and we get a higher SSIM value at the output for most images. The only exception is when input sampling very low (5%-15%) proportion to the original image. In these cases, as expected, the network trained with 5% sampling does a better job. However, we were getting better results throughout the curve from a 5% trained network than we got from the 15% trained one. From this evaluation we can conclude for a scenario where only very low sampling input is expected, our model trained on 5% sampling should be used. However, if higher sampling is possible, we can use a 25% sample trained ConvCS to get better reconstructions. Fig.4 plots the three differently trained ConvCSs and their performance on test data with a wide range of input sampling.

![ssim](https://user-images.githubusercontent.com/93070088/145702012-4a5972f1-ec08-4e83-9ca1-13f397601771.PNG)

![pik3](https://user-images.githubusercontent.com/93070088/145750448-e2bc2398-a4a2-4f8d-a74a-11070d5c6e73.png)

# 5. Discussion and Conclusions

In this project, we have introduced a Convolutional Neural Network to reconstruct a sampled image dubbed ConvCS with a fraction of the original pixels. We have used a complete randomizer mask to sample the original image. As an evaluation, we have trained the network with different proportions of input samplers. We used 10%, 25%, 30% randomized pixel samplers to train our network and compared each of their performances with different proportions sampled inputs(5%-40%). We used SSIM as the similarity metric for our performance analysis, we measure the SSIM of the network output images with the original images to get a sense of the accuracy of reconstruction. Even though our model can reproduce an output that is quite similar to the original image, there is quite a bit of information loss and color shift present in the output images. However, are more advanced DNN architectures such as Generative Adversarial Networks (GAN) which may be able to produce even better reconstructions. Also, it may be possible to train a deep net capable of both reconstruction and super-resolution.

# 6. References

[1] M. Rani, S. B. Dhok and R. B. Deshmukh, "A Systematic Review of Compressive Sensing: Concepts, Implementations and Applications," in IEEE Access, vol. 6, pp. 4875-4894, 2018, doi: 10.1109/ACCESS.2018.2793851.

[2] C. Dong, C. C. Loy, K. He and X. Tang, "Image Super-Resolution Using Deep Convolutional Networks," in IEEE Transactions on Pattern Analysis and Machine Intelligence, vol. 38, no. 2, pp. 295-307, 1 Feb. 2016, doi: 10.1109/TPAMI.2015.2439281.

[3] W. Shi, F. Jiang, S. Liu and D. Zhao, "Image Compressed Sensing Using Convolutional Neural Network," in IEEE Transactions on Image Processing, vol. 29, pp. 375-388, 2020, doi: 10.1109/TIP.2019.2928136.

[4] R. Heckel, M. Soltanolkotabi, "Compressive sensing with un-trained neural networks: Gradient descent finds the smoothest approximation", https://arxiv.org/abs/2005.03991

[5] P Hanumanth1, P Bhavana2 and Shreyanka Subbarayappa, "Application of deep learning and compressed sensing for reconstruction of images", Vol1706, First International Conference on Advances in Physical Sciences and Materials 13-14 (2020) Coimbatore, India.

[6] A. Bora, A. Jalal, E. Price, A. G. Dimakis, "Compressed Sensing using Generative Models", https://arxiv.org/abs/1703.03208

[7] S. Albawi, T. A. Mohammed and S. Al-Zawi, "Understanding of a convolutional neural network," 2017 International Conference on Engineering and Technology (ICET), 2017, pp. 1-6, doi: 10.1109/ICEngTechnol.2017.8308186.

[8] K. N. Raju and K. S. P. Reddy, "Comparative study of Structural Similarity Index (SSIM) by using different edge detection approaches on live video frames for different color models," 2017 International Conference on Intelligent Computing, Instrumentation and Control Technologies (ICICICT), 2017, pp. 932-937, doi: 10.1109/ICICICT1.2017.8342690.

[9] Wang X. et al. (2019) ESRGAN: Enhanced Super-Resolution Generative Adversarial Networks. In: Leal-Taixé L., Roth S. (eds) Computer Vision – ECCV 2018 Workshops. ECCV 2018. Lecture Notes in Computer Science, vol 11133. Springer, Cham. https://doi.org/10.1007/978-3-030-11021-5_5
