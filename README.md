# **Behavioral Cloning** 

[//]: # (Image References)

[image1]: ./report_images/summary.png "Model Summary"
[image2]: ./report_images/angles_hits_before.png "Hist before"
[image3]: ./report_images/angles_hist_after.png "Hist after"
[image4]: ./report_images/cropped_11252.jpg "Cropped 1"
[image5]: ./report_images/cropped_11457.jpg "Cropped 2"
[image6]: ./report_images/cropped_637.jpg "Cropped 3"
[image7]: ./report_images/training.png "Training_1"
[image8]: ./report_images/training_2.png "Training_2"
 
### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

The architecture selected was based on the NVIDIA paper for self driving cars. The following image present the result from calling the model.summary() method of Keras model.

![alt text][image1]

#### 2. Has an attempt been made to reduce overfitting of the model?

In order to prevent overfitting the data has been splitted into train (80%), validation (10%) and test (10%). The final values for each set were:
('Train:', 19317, 'Val:', 2415, 'Test:', 2415)
 
Additionally, Droput layers were added after the first three Dense layers (see model summary), in order to avoid overfitting. The values defined for dropout were 0.3, 0.2, 0.1

#### 3. Model parameter tuning

The adam optimizer was selected. The default learning rate of 0.001 was good enough for the training process. During the all the process of training, the loss function decreased. 

#### 4. Appropriate training data

The process to recollect the training data was the following:

1. Two laps were recorded with the car driving as center as possible. I drive the car really slow to have as much control as possible.
2. Another two laps were recorded but driving the track the other way around.
3. During two more laps, the car was taken off the road, and then the recovery was recorded. This process was done both on curves and straight sections as well as on the bridge.
4. Another lap was taken this time aiming to center the car, when it goes to the side but didn't touch the lane.
5. A data augmentation technique was applied where all images where flipped from right to left.

### Architecture and Training Documentation

#### 1. Solution Design Approach

My approach to solve the problem was based on recollecting really good training data to avoid issues, so I took my time on it. Additionally, the preprocessing of the images was done as part of the model (first two Keras layers). Here, the image was cropped as suggested, and the data was normalized. 

Besides that, the NVIDIA architeture was used, as explained on the next section. 

#### 2. Final Model Architecture

The architecture consisted of:

* 3 convolutional layers with a filter size of 5x5, and a stride of 2x2, and channels of 24, 36 and 48 respctively
* 2 convolutional layers with a filter size of 3x3, with no stride, and channels of 64 for each layer
* 4 Fully connected layers with 1164, 100, 50 and 10 neurons respectively.
* 1 output layer of one neuron
* After each layer (both convolutional and fully connected) the relu activation function was used. No activation function was used after the output layer as it was a regression model.

![alt text][image1]

#### 3. Creation of the Training Set & Training Process

After the training data was collected, a histogram plotting the angles collected was plotted. When analyzed it was decided to augmentate the data by flipping it form left to right. 

The followin images present the angles histogram before and after the data augmentation process. Consider that the angles with value 0 were not plotted in order to visualize better the histogram.

![alt text][image2]
![alt text][image3]

As part of the preprocessing, the images were cropped as suggested. Here it is possible to observe a couple of examples of the cropped images:
![alt text][image4]
![alt text][image5]
![alt text][image6]

The data was shuffle and split into the different sets using the train_test_split scikit learn function twice. The model was trained during 5 epochs. After revieweing the video results, it was decided to train the network for 5 more additional epochs. In the following images it is possible to see the loss values during both training processes. As it can be observed, the data didn't suffer from overfitting.

![alt text][image7]
![alt text][image8]

Nevertheless, the final test was driving the car autonomously trough the track without touching any lane line. The result can be observe on the file [video.mp4](/video.mp4) 

### Simulation

As it can be observed on the [video](./video.mp4), the car run smoothly trough the track without any issues. Considering that this is the second submission of the project, it is possible to see an important improvement in comparison to the first version, as the car does not touch any lane line now. 

All the curves where overcome with no issues. 
