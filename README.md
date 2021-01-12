# Project Title: Creating Robust Neural Network Generalisation for a Single-Camera Self-Driving Car
Archive for files, code and other details related my 2020 Final Year Project (EERI 474) for the purpose of ECSA Moderation. 

This project was based on version 3 of the [Donkey Car](https://github.com/autorope/donkeycar/). The Donkey Car is an open-source
self-driving library written in Python and using tools like Keras, Tensorflow, and OpenCV. This system can be installed on a 
Raspberry Pi/Jetson Nano hooked up to an RC car, or it can be run in the [Donkey Car Unity Simulator](https://github.com/tawnkramer/gym-donkeycar).

The [Donkey Car](https://github.com/autorope/donkeycar/blob/dev/LICENSE), as well as this EERI 474 Project, is licensed under the  [MIT Open Source
License](LICENSE).
## Engineering Problem Statement:

To investigate and implement techniques regarding the design, implementation and generalisation of a Convolutional Neural Network (CNN). This CNN is to be 
used as a self-driving car Pilot, and should be able to function in at least three separate locations with minimal training data (15000-30000 images). This CNN along with any image processing techniques used for generalisation will replace the default CNN Pilot available in an existing
open source self-driving system.

## Basic Solution Overview:

The Solution included developing and using a Neural Network Design methodology to build up an empirically sound Convolutional Neural Network for use as the Pilot
base. Additionally, methods of generalisation such as Feature Engineering and Data Diversification were tested and explored. The method of generalisation settled
on was Feature Engineering - specifically, a very bare-bones lane detection algorithm was iteratively developed. 

This algorithm included converting the input image from the camera to grayscale, determining the average pixel value of the grayscaled image (to adjust for relative 
lighting), using a rounded 10% of the average pixel value as a factor for the block size and adding constant for Gaussian Image Thresholding (to ensure only the 
lane lines are highlighted as much as possible), and then applying Canny Edge Detection to the resulting thresholded image - which is then also passed through an 
ROI (Region of Interest) Filter. This resulted in a mostly robust lane detector that could be reliably used in all three simulator environments - which had 
changes in background, lighting, and track topology. Functions such as grayscale, canny edge detection, and gaussian thresholding were implemented using the 
relevant [OpenCV Libraries](https://opencv.org/).

The development of the Convolutional Neural Network will be discussed in the Methodology section.
## Methodology:

## End Product:
