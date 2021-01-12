# Project Title: Creating Robust Neural Network Generalisation for a Single-Camera Self-Driving Car
Archive for files, code and other details related my 2020 Final Year Project (EERI 474) for the purpose of ECSA Moderation. 

This project was based on version 3 of the [Donkey Car](https://github.com/autorope/donkeycar/). The Donkey Car is an open-source
self-driving library written in Python and using tools like Keras, Tensorflow, and OpenCV. This system can be installed on a 
Raspberry Pi/Jetson Nano hooked up to an RC car, or it can be run in the [Donkey Car Unity Simulator](https://github.com/tawnkramer/gym-donkeycar).

The [Donkey Car](https://github.com/autorope/donkeycar/blob/dev/LICENSE), as well as this EERI 474 Project, is licensed under the  [MIT Open Source
License](LICENSE).

[Watch Project Overview Video](https://www.youtube.com/watch?v=FjNhCpwV-Tw)

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
After going through the current state-of-the art for the purposes of writing a literature survey for Neural Networks and Generalisation, an in-depth literature
study was also written and researced to fully understand each layer, activation function, optimization function and more present in a Convolutional Neural Network
so that these components can be effectively used and selected.

Colab notebooks were set up for various stages of an experimental design process - which started with getting a CNN to do just better than a random guess, to 
building it up until it overfit to the data completely, and then scaled back. Once these processes were complete (which consisted experimenting with different
layer types, activation functions and optimizers until satisfactory results began to be achieved) another set of notebooks was created and used to compare feature 
engineering techniques, the performance of the network using different training and generalisation techniques, and narrowing down the solution.

Each time a network was trained, changes were made, or a network was to be evaluated, it was run inside a Neptune experiment. Over 300 of these experiments were 
run throughout the neural network and generalisation design process. Neptune.ai is an experiment logging service that records the parameters, gpu and cpu usage, 
and training statistics of your neural network training sessions. All experiments that were run recorded the layer types, number of each layer type, the "pruning" 
method used, the dataset used, the feature engineering used, and the training performance. These experiments are logged for public viewing [here](https://ui.neptune.ai/charag/Littlefoot/experiments?viewId=standard-view).

A final set of notebooks were used to train the models used in the physical simulator test - the notebooks trained a model on a Vanilla dataset with no feature 
engineering, Vanilla dataset with feature engineering, Diverse Dataset without feature engineering, and Diverse dataset with feature engineering. These models 
were ran back-to-back in the three simulator environments to complete a qualitative test - which measured how many times the car deviated from the track, how many 
times it recovered, and if it completed the track without deviating more than twice. The final model was selected to be the one trained on the Diverse Dataset 
with feature engineering - as it almost flawlessly completed each environment.
