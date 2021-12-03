# Facial-Keypoints
## Introduction
Facial landmark detection is the task of detecting key landmarks on the face. It can be use in various applications such as detection of face part and then changing it with other things etc.

## Problem Statement
To predict the facial keypoints for a given face.

## Dataset Description
Each predicted keypoint is specified by an (x,y) real-valued pair in the space of pixel indices. There are 15 keypoints, which represent the following elements of the face:

left_eye_center, right_eye_center, left_eye_inner_corner, left_eye_outer_corner, right_eye_inner_corner, right_eye_outer_corner, left_eyebrow_inner_end, left_eyebrow_outer_end, right_eyebrow_inner_end, right_eyebrow_outer_end, nose_tip, mouth_left_corner, mouth_right_corner, mouth_center_top_lip, mouth_center_bottom_lip

Left and right here refers to the point of view of the subject.

In some examples, some of the target keypoint positions are misssing (encoded as missing entries in the csv, i.e., with nothing between two commas).

The input image is given in the last field of the data files, and consists of a list of pixels (ordered by row), as integers in (0,255). The images are 96x96 pixels.

Data link: https://www.kaggle.com/c/facial-keypoints-detection/data?select=test.zip

## Null Values

![image](https://user-images.githubusercontent.com/62516990/144334899-ae79107d-9db4-4e7f-8a3e-e83da1079e8a.png)

As you can see that there are a lot of null values, 'ffill' method is used to fill null values, it will fill values exact as in the previous instance

Sanity check to see all null values have been filled

![image](https://user-images.githubusercontent.com/62516990/144335096-10ace067-2a89-4c27-9be1-22af95b6fbb1.png)

## Data Preprocessing

### Converting string to numpy array of float
The "image" feature of the dataset contains the values of pixels images, but these are stored as a string. A user-defined function is written to convert these string to an array of shape (m, 96, 96, 1). Also, to normalize the pixel values, each pixel value is divided by the 255, as shown in the figure below.

![image](https://user-images.githubusercontent.com/62516990/144335763-41a818fa-7299-429d-bae8-1cf3180b8847.png)

## Data Visualization:
To visualize the facial keypoints on the face, two plots are shown at the same time: scatter plot and imshow.

![image](https://user-images.githubusercontent.com/62516990/144335983-ca9c9e20-1efa-4b26-9f12-475a3e4cb9a3.png)

## Modeling Approaches

### Building CNN model

1. A convolutional neural network is defined with five convolutional and three maxpooling layers.
2. To get the continuous output linear activation is used in the last layer.
3. As the output is continuous the mean squared error is selected as a loss function.

![image](https://user-images.githubusercontent.com/62516990/144336627-bf0bdf32-66f8-4b37-ac84-0a1bd6f05b33.png)

### Mean Absolute error and Loss

![image](https://user-images.githubusercontent.com/62516990/144336759-381e245d-1fc3-4d52-849c-76bf47db09b8.png)


![image](https://user-images.githubusercontent.com/62516990/144336739-ef496e93-be9e-4cc7-9638-999171938cef.png)

## Predictions

![image](https://user-images.githubusercontent.com/62516990/144336854-da5455a4-540f-4516-8235-062e4ede2205.png)


## Results/Discussion
- CNN, which is usually used for classification, can be used to predict the facial keypoints.
- Here CNN works as a regression model, hence in the last layer linear activation is used, and to predict cordinates as close as actual, we have used mean squared error loss function.
- Model can do even better if the missing values are lesser.
