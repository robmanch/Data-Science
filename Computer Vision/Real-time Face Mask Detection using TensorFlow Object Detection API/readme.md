## Executive Summary
In this phase of the world where it is extremely critical in wearing masks to prevent the communicable diseases. It is necessary to set up certain measures to curb the further spread. Wearing of masks will prevent most of the chances of contracting the disease. However, people are not aware of the consequences and appear to roam without masks.

In this project, we will be implementing a real-time face mask detection system that can detect if the person captured by the camera is wearing a mask or not.

## Problem Statement
As the disease is wide-spread and the economies are slowly opening up, it is important to employ less staffs in places where it is necessary to manage the crowds. To overcome this, we can have a real-time object detection system which can alert the system when it captures a person without any mask.

### Installation
We need to install the following libraries,
-	TensorFlow (See TensorFlow Installation)
-	TensorFlow Object Detection API (See TensorFlow Object Detection API Installation)
-	Protobuf
-	Cudnn/Cuda
-	labelImg
-	PyQt
-	XML

## Capture Images
A script has been written using OpenCV to capture mask and no mask images with webcam. Then, these images are randomly selected using numpy.random.choice attribute, and moved to train and test directories using shutil library.
 ![image](https://user-images.githubusercontent.com/62516990/149002445-45c3b5d4-3c6c-49cc-b138-f6c6cfe7cdaa.png)
 
![image](https://user-images.githubusercontent.com/62516990/149002463-602da7d9-cebb-4e16-a5be-78f260987e72.png)

## Preparing the Dataset
LabelImg has been used to annotate the dataset
After installing LabelImg and the images of both with face mask and without facemask are collected and then annotated using the following command
	labelImg <PATH_TO_TF>/TensorFlow/workspace/face-mask-detection/images

### Annotating the image (No_Mask)
![image](https://user-images.githubusercontent.com/62516990/149002497-48c18a75-efef-40fd-9bef-c842d7c56fa3.png)

### Annotating the image (Mask)
![image](https://user-images.githubusercontent.com/62516990/149002521-7d19e2b4-3cc4-4ecf-b85e-9a41ae23d46e.png)

### After annotating a .xml file is created (Mask)
 ![image](https://user-images.githubusercontent.com/62516990/149002569-4e13ae86-8b8c-4e38-a108-fb1e4a0839b9.png)

### After annotating a .xml file is created (No_Mask)
![image](https://user-images.githubusercontent.com/62516990/149002600-d4d66c68-be10-4c6f-a328-dabdc3d80f2d.png)

## Partition the Dataset
Once the data is annotated, it is split into train and test using numpy.random.choice attribute, and moved to train and test directories using shutil library.

## Preparing the Workspace
After the installation of TensorFlow, a workspace is setup with the name of the module along with the other required folders.
![image](https://user-images.githubusercontent.com/62516990/149002641-5a42ccfe-3408-42ce-a0be-f8931c7ab9eb.png)

### Create Label Map
A label map is created for both the type of classes in our dataset as shown below.

item {
    id: 1
    name: ‘mask'
}
item {
    id: 2
    name: ‘nomask'
}

 ![image](https://user-images.githubusercontent.com/62516990/149002697-fcf2e8c8-381b-468a-bed8-21027c7ffb01.png)

## Create TensorFlow Records
Convert *.xml to *.record
A simple script is created which can iterate through all *.xml files in the face-mask-detection/images/train and face-mask-detection/images/test folders, and generate a *.record file for each of the two. Here is an example script that allows us to do just that:
![image](https://user-images.githubusercontent.com/62516990/149002742-03aae90e-774b-4957-9400-eb28f0cd5255.png)
 
## Configuring a Training Job
For the purpose of this project, we are not building the detection model from scratch instead we are going to leverage the transfer learning concept.
Ware using SSD MOBILENET V2 FPN 320*320, as this model provides good detection speed for our real time detection and also provides good mean accuracy performance.
Link to the TensorFlow Object Detection Model used: [TensorFlow 2 Detection Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md)
 ![image](https://user-images.githubusercontent.com/62516990/149002851-a4c4387b-247e-4be8-9484-10f606ba21a1.png)


## Configure the Training Pipeline
The pipeline.config file from the downloaded model is placed in the below directory structure
 ![image](https://user-images.githubusercontent.com/62516990/149002872-da7a05e0-056a-49d0-bc8c-e20682e8ed81.png)


It is then configured by altering the below mentioned variables.
1.	num_classes
2.	batch_size
3.	fine_tune_checkpoint
4.	fine_tune_checkpoint_type
5.	label_map_path
6.	Train & Test record path
 ![image](https://user-images.githubusercontent.com/62516990/149002886-7d2480ad-4f89-49af-913a-e77d9fb67a61.png)


## Training the Model
The changes we have made in pipeline.config file are stored in the structure described in the last slide. After copying the model_main_tf2.py file from Tensorflow package to workspace and running the following command will train the model.


## Command to Train the model:
python model_main_tf2.py --model_dir=models/my_ssd_resnet50_v1_fpn --pipeline_config_path=models/my_ssd_resnet50_v1_fpn/pipeline.config

## Load the trained model:
The model that is trained is restored from the checkpoints.
![image](https://user-images.githubusercontent.com/62516990/149002931-2e478335-350c-40e4-8733-db11b4660bad.png)

 
## Real-time detection
A script has been written that is used to initialize camera, reading frame, converting the image to array.
Then tensor. viz_utils.visualize_boxes_and_labels_on_image_array is used to setup the boxes, scores and labels on screen. 
Real-time detection of face mask is done custom TensorFlow object detection model.

## References:
1.	TensorFlow 2 Object Detection API tutorial, retrieved from https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/
2.	Pre-trained model downloaded from https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md
3.	Nicholas Renotte, https://www.youtube.com/watch?v=yqkISICHH-U&t=17274s

