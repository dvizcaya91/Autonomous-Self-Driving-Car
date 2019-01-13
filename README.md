# **Behavioral Cloning** 

[//]: # (Image References)

[image1]: ./model_summary.png "Model Summary"
 
### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

The architecture selected was based on the NVIDIA paper for self driving cars. The following image present the result from calling the model.summary() method of Keras model.

![alt text][image1]

#### 2. Attempts to reduce overfitting in the model

The model didn't present overfitting after training. I assume the reasons for this behavior were that 1) the recollection of the data was done carefully in order to handle as many scenarios as possible. 2) The number of epochs was set to 3 so the model didn't have time to overfit.

#### 3. Model parameter tuning

The adam optimizer was selected. The default learning rate of 0.001 was good enough for the training process to run smoothly. 

#### 4. Appropriate training data

The process to recollect the training data was the following:

1. Two laps were recorded with the car driving as center as possible. I drive the car really slow to have as much control as possible.
2. Another two laps were recorded but driving the track the other way around.
3. During two more laps, the car was taken off the road, and then the recovery was recorded. This process was done both on curves and straight sections as well as on the bridge.

### Model Architecture and Training Strategy

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

The data was shuffle and split into the different sets using the train_test_split scikit learn function twice. The loss function (MSE) was calculated on the three sets in order to verify the prescence of overfitting or underfitting. 

Nevertheless, the final test was driving the car autonomously trough the track. The result can be observe on the file run1.mp4 

### Simulation

As it can be observed on the [video](run1.mp4), the car run smoothly trough the track without any major issues. It can be observed that the car does not stays competely center but rather a little bit to the left. This can be due to the fact that it was trained to recover when touching the lateral lines, but not when it wasn't center.

The recovery process worked well. Specifically, if ones observe the car when getting out of the bridge, it is possible to see how it correct the angle to center the car again. 

All the curves where overcome with no issues. 
