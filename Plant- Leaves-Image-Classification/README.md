<h1 align="center"> Assignment 1: Plant Leaves Classification</h1>


## Overview
The goal of the project is to develop a Neural Network based classifier of a leaves images. This project explores the impact of various network hyperparameters, such as regiralization, number of layers in the feature extractor and classifier parts, dropout and etc. Based on the work done and the ranking on `CodaLab` competition organized by the TA of the course, our team achieved 5 out of 5 points for the assignment. 

## Dataset
The dataset used in this project is a subset of `PlantVillage` dataset (full dataset can be downloaded [here](https://data.mendeley.com/public-files/datasets/tywbtsjrjv/files/d5652a28-c1d8-4b76-97f3-72fb80f94efc/file_downloaded)). Our dataset contains `17728` images of various plants, which are divided into categories according to the species of the plant to which they belong (`14 classes`). 

We split the dataset into a training (80%) and validation (20%) sets. For these purposes we used the `ImageDataGenerator`’s
validation_split parameter. We did not create a test set, as it was already provided on the `CodaLab` platform. All of the images are 3-channel RGB images, of size 256x256 pixels.

## Approach
Folder [`notebooks/past_versions`](notebooks/past_versions/) contains the notebook tested during the competition. To summarize the content, we provide the following changelog:

- v00: three convolutional layers, one dense layer as in the example from the 4th lab session
- v01: first basic model with two convolutional layers and one dense layer, no optimization of any sort
- v02: same network as v01, but with regularizaton
- v03: three convolutional layers, one dense layer, no optimization
- v04: same network as v03 with early stopping (to be tuned, the early stopping is not triggered)
- v05: same network as v04, this time with data augmentation

In the end, the best model of the described above managed to achieve only `73.02 %` of accuracy. Our next approach was to adopt transfer learning. We decided to use `VGG16` as a backbone and use 3 dense layers for the classification head ([notebook](notebooks/current.ipynb)). With a fine tuning of the hyperparameters of the elastic net regularizer and the dropout probability, we managed to achieve `90.9 %` of accuracy on the final test set. All the model parameters for each of the experiment are stored in the [`experiments/`](experiments/) folder.

The final results, as well as a brief description of the steps done, are presented in the [report file](report/tex/main.pdf).

## References
Hughes, David & Salathe, Marcel. (2015). An open access repository of images on plant health to enable the development of mobile disease diagnostics through machine learning and crowdsourcing. 