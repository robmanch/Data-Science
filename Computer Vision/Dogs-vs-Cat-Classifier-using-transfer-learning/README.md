# Dogs-vs-Cat-Classifier-using-transfer-learning

## Abstract
The idea behind this project is to develop a simple web app that allows users to upload an image and can classify that into two classes: Dog, and Cat. In the starting, a custom CNN was implemented to achieve this task, but the model performance shown that model is overfitted. To reduce the overfitting, data augmentation and dropout layer were used. Also, Inception network had been used to get the good performance. The best classifier's result was obtained with pre-trained inception model with the resulting accuracy of approximately 96.5%.

## Problem Statement:
To buid a simple web app that uses deep learning model at the backend to predict a given images as cat or dog.

## UI Screenshots

### Homepage

 ![image](https://user-images.githubusercontent.com/62516990/144332810-297f2720-417c-4838-88dd-171e879c20e2.png)

### Prediction as cat
![image](https://user-images.githubusercontent.com/62516990/144332852-124d032c-6cb6-4b34-acf5-b09c3630196d.png)

### Prediction as dog

![image](https://user-images.githubusercontent.com/62516990/144332876-ad223b0a-8c52-4e9f-a999-d8ea5b125354.png)


## Dataset
1. Acquired from: https://www.kaggle.com/c/dogs-vs-cats
2. Total number of images(dogs & cats) in training set: 25000
3. Total number of images(dogs & cats) in test set: 12500

## Making Directories
Tensorflow requires the data to be in the proper directories, so arranging according to it.

![image](https://user-images.githubusercontent.com/62516990/144331853-9bcc1036-1f4e-4bed-a785-edb0c34cfa43.png)

### Shutil library is used to move files

![image](https://user-images.githubusercontent.com/62516990/144331963-3c648fef-a29c-4a9a-85d9-e0e6605e0242.png)

## Data Visualization

![image](https://user-images.githubusercontent.com/62516990/144332033-09882f37-6646-4b79-aaed-78c614c981de.png)

## Modeling Approaches

- Custom built Convolution Neural Networks (CNNs)
- Inception pre-trained

### Custom built Convolution Neural Networks (CNNs)

![image](https://user-images.githubusercontent.com/62516990/144332165-50d5fa48-45cd-424b-af05-bb09491c67bb.png)

#### Using ImageDataGenerator to read the data

![image](https://user-images.githubusercontent.com/62516990/144332236-4ef776be-f534-473e-8a0a-4464ab31c01f.png)

#### Implementing Callback

![image](https://user-images.githubusercontent.com/62516990/144332277-b36fbc6e-2419-448c-ab3d-e34ae3b31f2c.png)

#### Accuracy & Loss

![image](https://user-images.githubusercontent.com/62516990/144332316-b28cce63-63ad-4049-bd3f-7cb7a8c6fddb.png)

Observations:
1.	Training Accuracy is increasing, or training loss is decreasing with epochs, which means that model is learning
2.	There is a huge difference between the training accuracy and validation accuracy which suggests that there is overfitting.

### Data Augmentation
1.	Data augmentation is a technique that can be used to generate more images by using rotation, cropping, shifting, flipping, etc.
2.	This will result in increase in the data size and reduce in overfitting.

![image](https://user-images.githubusercontent.com/62516990/144332369-cf9c1a95-5b30-4a20-ace9-344b3bd54cb0.png)

### Accuracy & Loss after using data augmentation

![image](https://user-images.githubusercontent.com/62516990/144332420-c62f49f5-3fd8-4fc2-a788-4943b2da3093.png)

## Transfer Learning

1.	Transfer Learning is a method in which a pre trained model is used, here inception model is chosen.
2.	The top layer (input and output layer) is removed and added according to this project.
3.	The inception layers will not be trained here, only the top layers will be trained.

![image](https://user-images.githubusercontent.com/62516990/144332465-72fa2a84-d91c-4316-bead-1ea0ffa0e61c.png)

#### Using the 'mixed7' layer as the last layer of pre trained model

![image](https://user-images.githubusercontent.com/62516990/144332494-e830ab8d-5ecb-4a69-bff6-c93858a6066d.png)

![image](https://user-images.githubusercontent.com/62516990/144332504-22345103-0057-43c5-b35e-f7e1595d0d75.png)

### Accuracy & Loss with transfer learning

![image](https://user-images.githubusercontent.com/62516990/144332547-154bb310-e402-4f60-b3e2-6937e763bed6.png)

Results and Discussion of Modelling Approaches
1.	Pre-trained overperform the model from scratch.
2.	Overfitting has been reduced by using data augmentation and dropout.

## Usage
User needs to upload an image to our application. The application will be able to predict if the image uploaded is either a cat or a dog.

## Application URL
http://ec2-3-144-5-9.us-east-2.compute.amazonaws.com:5001/


## Pre-requisites
Due to space limitations in GitHub, the trained model is not uploaded in this repository. However, it can be downloaded from the below link and should be pasted within 'static' folder after cloning a branch in the repository.
 https://drive.google.com/file/d/1Ryt40-9O4oZvo0kMNkgZEQmK_vrGN_jx/view?usp=sharing
 
## UI Screenshots

### Homepage

 ![image](https://user-images.githubusercontent.com/62516990/144332810-297f2720-417c-4838-88dd-171e879c20e2.png)

### Prediction as cat
![image](https://user-images.githubusercontent.com/62516990/144332852-124d032c-6cb6-4b34-acf5-b09c3630196d.png)

### Prediction as dog

![image](https://user-images.githubusercontent.com/62516990/144332876-ad223b0a-8c52-4e9f-a999-d8ea5b125354.png)

## Model Deployment

The application UI is built with the help of Flask, it uses the saved model for on-demand prediction, this application is deployed and hosted locally. AWS EC2 is public facing and can accept the request from the user over the internet. Once it gets a request, it immediately forwards it to our local server set up.

![image](https://user-images.githubusercontent.com/62516990/144332917-4100b48e-1b25-4b07-895d-cbe316e4c373.png)

A bridge between the AWS EC2 instance and the local server has been established to be within the same virtual network to enable request forwarding and reverse proxy. This is the most cost-effective solution considering we already have the physical hardware, just that it required to be available over the internet.

### Reasons for opting this method:
The model is quite huge in size for the virtual machines given in the free tier. As shown in the screenshot, a memory issue was faced while trying to install TensorFlow.

![image](https://user-images.githubusercontent.com/62516990/144332948-ffec2ffa-ce49-4aa5-9de1-f081528b60d4.png)

Local server has been used to make this web app available in the internet.

![image](https://user-images.githubusercontent.com/62516990/144332975-a0b2c47a-3e60-4523-8e8c-c6733acfbce5.png)



