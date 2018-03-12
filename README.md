# RoboND-Inference-Project
## Abstract

The objective of this project is to train a deployable robotic inference model to classify images into 3 classes. Two distinct sets of data were trained using NVIDIA’s DIGITS platform as part of the Udacity Robotics Software Engineer Nanodegree. The first consisted of images of bottles and candy boxes, and the second had images of faces. The first model was able to classify the objects with an accuracy of 75.4% with an evaluation time of ~4.34ms, while the second model achieved a test accuracy of 100% after 10 epochs of training. These results are meaningful indicators of the ability of a simple inference model to correctly classify distinct objects.

## Introduction 

Object recognition and classification is an important and versatile application of deep neural networks. Using a large dataset to train a convolutional neural network, a model can be deployed on an embedded system to perform real time sorting. There are many uses of this type of system, like a robotic arm that can pick out defective items from a conveyor belt in a manufacturing plant, or a diagnostic tool that classifies diseased plants based on images of symptomatic leaves (Figure 1.1).
The inference idea that was implemented in this project involved classifying different people.

[image_0]: ./images/1.1.png
![alt text][image_0] 

## Background / Formulation

For this project, the sample bottle dataset as well as the chosen face dataset were trained using the AlexNet architecture provided on DIGITS, since the images in both datasets were in the same format as those taken by AlexNet (Figure 2.1). A minimum of 2 samples per class were used. In the first dataset (bottles), 75% of the images (7,570) were used for training while 25% were retained for validation (2,524). In the second dataset (faces), 30 images were kept aside for testing (2.5% of the dataset). Of the remainder, the model trained on 70% of the images (877), while the remaining 30% was used for validation (293). I ran both training sessions for 10 epochs. The snapshot interval and validation interval were both kept at defaults of 1 epoch. The solver type used was Stochastic Gradient Descent, and the base learning rate was chosen to be 0.01. In terms of data transformation, the mean image was subtracted to normalize both datasets. 

[image_1]: ./images/alexnet.png
![alt text][image_1] 

## Data Acquisition 
The bottle dataset contained 10,094 images, of which the 3 classes were “bottles”, “candy boxes” and “nothing”. The faces datasets contained 1200 images: 400 images of person A, 400 of person B and 400 of nothing. Figure 3.1 provides a schematic of the 2 datasets. All images were 256X256 in size and RGB.

[image_2]: ./images/3.1.png
![alt text][image_2] 

Figure 3.1 
Structure of data

The faces dataset was collected using an phone camera. The subjects were asked to lie down on a wooden floor while the photographer clicked 400 images in rapid succession. During this time the subjects were asked to change their facial expressions and tilt their heads from side to side. Lighting consisted of a simple set of 3 CFL bulbs (15 watts) directly above the subjects, on the ceiling.These images were then uploaded to DIGITS without any modifications. Figures 3.2 and 3.3 provide sample images from each of the datasets.

[image_3]: ./images/samples.png
![alt text][image_3]

## Results 

The model trained on the bottle dataset achieved a testing accuracy of 75.4% after 10 epochs. The largest increases in accuracy were seen in the 1st and 3rd epochs, while the 2nd epoch contained a large spike in the training loss. By the 4th epoch, the model had stabilized and achieved a very high accuracy. On the other hand, the model trained on the face dataset achieved its steady state by the 3rd epoch, and an overall training accuracy of 100% by the end of 10 epochs. The training loss fluctuated heavily between the 4th and 6th epoch, while the validation loss decreased gradually over the course of the 10 epochs. This model also achieved a testing accuracy of 100%, when used to classify 30 images set aside for testing. Figures 4.1 - 4.4 show the results of the bottle dataset, while 4.5- 4.7 show the results of the face dataset. Figures 4.8 and 4.9 demonstrate the testing accuracy of the model, when tested on 30 images, and an example of the predictions the model made on an image.

[image_4]: ./images/4.1.png
![alt text][image_4] 

[image_5]: ./images/4.3.png
![alt text][image_5] 

[image_6]: ./images/4.4.png
![alt text][image_6] 

[image_7]: ./images/4.5.png
![alt text][image_7] 

Figure 4.5
Overview of the training specifications for the people dataset

[image_8]: ./images/4.6.png
![alt text][image_8] 

[image_9]: ./images/4.7.png
![alt text][image_9] 

[image_10]: ./images/results.png
![alt text][image_10] 

Figure 4.8
Results of classification of 30 test images

[image_11]: ./images/4.9.png
![alt text][image_11]

Figure 4.9
Sample of model predictions for a single image

## Discussion

The results of the bottle dataset were about what one would expect for a dataset of its size. Three out of four times the model correctly classifies the images as “bottle”, “candy box” or “nothing”, and does so within 10ms. With more and better data, this accuracy would certainly improve, and inference time would likely decrease as well.

However, the results of the model trained on the face dataset were surprising. With just 400 images per class, the model achieved an extremely high accuracy, possibly overfitting the data. The most likely reason for this, is that the images that the model was trained on were very uniform. Intra-class variation was very low. For example, lighting and background were kept constant in all the images. While the subjects were asked to change expressions and tilt their heads, this was an unrealistic representation of faces in real life. People look different on different days: hairstyles, accessories and clothes may change on a daily basis. In addition, the low number of classes (3) likely made classification relatively simple for the model, which may not be able to generalize inference when the face looks very different.

In this project, inference time was almost negligible, and accuracy was extremely high. However, given that the dataset was highly uniform, a high accuracy was expected. It would be reasonable to sacrifice more inference time, in order to enhance the generalizability of the model. In this particular use-case, one would likely want to be more confident about the model’s predictions, even if it took a longer time to classify the face. For example, in the Facebook face recognition feature, accuracy is likely more important than inference time!

## Conclusion / Future Work 

The foremost area of improvement would be to use a more varied dataset for the faces model, including different lighting, backgrounds, and even clothes and accessories (eg. glasses), and then see if the model can still classify the people with high accuracy. Additionally, the model parameters (like learning rate and solver type) could be further adjusted. The goal of these adjustments would be to make the model much more generalizable to “real-world” data.

The second area of exploration is deployment. Using an embedded platform like the Jetson TX2 to perform real-time classification would be an exciting and educational next step!

## Additional Exploration

After completing this report, I wanted to explore further and attempt to build a model that could classify objects in an environment that more closely resembled the real world. I took images of 3 objects - mugs (3 different kinds), makeup brushes (of varying shapes and sized) and utensils (forks, knives and spoons). After training for 10 epochs under the same specifications as the other 2 models, and testing on a sample image, I achieved the following result.

[image_12]: ./images/brush.png
![alt text][image_12]

It is correctly classified as a brush, but with a much lower confidence level than the other 2 models. Data collection is a important component of understanding of neural networks, and something I will certainly be experimenting with further.
