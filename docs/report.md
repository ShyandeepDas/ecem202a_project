# Table of Contents
* Abstract
* [Introduction](#1-introduction)
* [Related Work](#2-related-work)
* [Technical Approach](#3-technical-approach)
* [Evaluation and Results](#4-evaluation-and-results)
* [Discussion and Conclusions](#5-discussion-and-conclusions)
* [References](#6-references)

# Abstract

In the information age, it is essential to share a massive amount of data for proper surveillance and operation of any plant. However, it is often the case that the site has a lot of surveillance needs and as a result, it becomes difficult to account for bandwidths of all the cameras and sensors. The bandwidth limitation is not the only issue, however. The quality of the camera is often not very good, as a result, the image is noisy. There exist many solutions to the issue, most of them try to send partial data from the sensors to a server where it is reconstructed and enhanced to produce usable results. In this project, we aim to use such a mechanism using tools such as compressive sensing and deep learning and recreate an image from incomplete information and increase its resolution to get better results. We further introduce our own Convolutional Neural Network (CNN) for regenerating an image from randomly sampled inputs. This eliminates the need for any computationally heavy methods in the input site and the server using this CNN can reconstruct the image. We have compared our model's results while training it with a different amount of sampling at the input. We also have compared its output with JPEG using Structural Similarity Index Metric (SSIM) to compare our work with the state of the art.

# 1. Introduction

* Motivation & Objective: In this project, we tried to solve a problem statement where there is a site need for constant surveillance but it is both hardware and bandwidth constraint. There is very limited bandwidth availability so it cannot send the whole image to the server. we aim to propose a Convolutional Neural Network to reconstruct a randomly sampled image. This way only a fraction of the original image's pixel will need to be sent to the server and this Deep Neural Network architecture is trained to reconstruct the image. Also, The sampling of the image is completely random with no consistent pattern hence there is no intense computational need at the hardware constraint sender site. The Deep Neural Network takes in the sampled image and the sampler mask (randomizer used to sample the image) and it reconstructs the original image at the output.
* State of the Art & Its Limitations: Currently, there are solutions such as compressive sensing [] where the full image can be reconstructed from a fraction of the number of pixels sent. This solution even though extremely effective, is computationally heavy. There are Super Resolution Neural Networks such as SRCNNs[], ESRGANs[] for the enhancement of image resolution. However, there is no pipeline that does both reconstruction and enhancement of an image. The approach we suggested, because of a random sampling of the pixels, does not require a high amount of computation at the sender site and the images are reconstructed at the server. We have used an ESRGAN to enhance the reconstructed image to produce a high-resolution final output.
* Novelty & Rationale: Although we did find papers that have created similar compressive sensing using neural networks, all of them do require some computation at the sender site. As we use completely random pixel selection for our reconstruction, our approach does not require any high-level sensor-site computation. This is a solution for the problem we stated earlier- where the sensor site is both bandwidth and hardware constraint.
* Potential Impact: This model can have a lot of uses throughout various industries where there is a lot of surveillance is essential and bandwidth is limited. also, such a setup can be used in rural areas where connectivity and sensor quality is very low and only primitive onsite computation is possible.
* Challenges: Reconstruction of an image from a fraction of its original pixel values is an extremely daunting task even for the most advanced of today's neural network. Selecting the appropriate proportion to sample the input dataset when training the network is also another challenge we faced. We have done a comparative study on the sort of results with different proportions of input sampling (while training) in evaluation.
* Requirements for Success: Familiarity with Convolutional Neural Networks, programming ability in python, and the torch library.
* Metrics of Success: Structural Similarity Index Metric(SSIM) of the output image is compared with original (pre-sampled) image to measure the reconstruction quality.

# 2. Related Work

# 3. Technical Approach

# 4. Evaluation and Results

# 5. Discussion and Conclusions

# 6. References
