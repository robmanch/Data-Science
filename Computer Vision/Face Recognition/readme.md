One of the challenges in face recognition is one-shot learning which means that the person has to be recognise by using a single example.

One solution could be to build a CNN classifier with a softmax layer in the output to classify the face, but there are several issues with this approach:
1. Few images in the dataset.
2. Need to train the model again, if a new person comes.

Another solution could be to learn the similarity function by using CNN. The input to this model is two images: a new image/anchor image and a dataset image. Here, the goal is to output a small number if the new image is different from the dataset image. This model seems to solve both issues of the former solution.

Implemented the later solution using Tensorflow. Used the same pre-trained VGG16 to get the encodings for both images. Built a custom Siamese layer to calculate the absolute difference between these encodings. Finally, used a fully connected layer with sigmoid activation in the output layer.

Currently, it's a 1:1 verification system, but can be used for 1:k verification with few modifications.

References:
1. DeepFace: Closing the Gap to Human-Level Performance in Face Verification
2. Nicholas Renotte, https://lnkd.in/gi7fYrUY
