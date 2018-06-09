# **Behavioral Cloning** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/placeholder.png "Model Visualization"
[image2]: ./examples/placeholder.png "Grayscaling"
[image3]: ./examples/placeholder_small.png "Recovery Image"
[image4]: ./examples/placeholder_small.png "Recovery Image"
[image5]: ./examples/placeholder_small.png "Recovery Image"
[image6]: ./examples/placeholder_small.png "Normal Image"
[image7]: ./examples/placeholder_small.png "Flipped Image"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md or writeup_report.pdf summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 3x3 filter sizes and depths between 32 and 128 (model.py lines 18-24) 

The model includes RELU layers to introduce nonlinearity (code line 20), and the data is normalized in the model using a Keras lambda layer (code line 18). 

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.py lines 21). 

The model was trained and validated on different data sets to ensure that the model was not overfitting (code line 10-16). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.py line 25).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road ... 

For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the ... I thought this model might be appropriate because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model so that ...

Then I ... 

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track... to improve the driving behavior in these cases, I ....

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture
____________________________________________________________________________________________________
Layer (type)                     Output Shape          Param #     Connected to
====================================================================================================
lambda_1 (Lambda)                (None, 16, 32, 1)     0           lambda_input_1[0][0]
____________________________________________________________________________________________________
convolution2d_1 (Convolution2D)  (None, 14, 30, 2)     20          lambda_1[0][0]
____________________________________________________________________________________________________
maxpooling2d_1 (MaxPooling2D)    (None, 3, 7, 2)       0           convolution2d_1[0][0]
____________________________________________________________________________________________________
dropout_1 (Dropout)              (None, 3, 7, 2)       0           maxpooling2d_1[0][0]
____________________________________________________________________________________________________
flatten_1 (Flatten)              (None, 42)            0           dropout_1[0][0]
____________________________________________________________________________________________________
dense_1 (Dense)                  (None, 1)             43          flatten_1[0][0]
====================================================================================================
Total params: 63
Trainable params: 63
Non-trainable params: 0
____________________________________________________________________________________________________


#### 3. Creation of the Training Set & Training Process

Adam optimizer is used with default configuration. The parameter are set as:
Epochs:upto 50 but normally early stopping within 30 epochs.
15% of data is chosen for validation set


Train on 40983 samples, validate on 7233 samples
Epoch 1/50
40983/40983 [==============================] - 11s 273us/step - loss: 0.1859 - mean_squared_error: 0.1859 - val_loss: 0.0741 - val_mean_squared_error: 0.0741

Epoch 00001: val_mean_squared_error improved from inf to 0.07413, saving model to model.h5
Epoch 2/50
40983/40983 [==============================] - 5s 123us/step - loss: 0.0727 - mean_squared_error: 0.0727 - val_loss: 0.0543 - val_mean_squared_error: 0.0543

Epoch 00002: val_mean_squared_error improved from 0.07413 to 0.05425, saving model to model.h5
Epoch 3/50
40983/40983 [==============================] - 5s 129us/step - loss: 0.0560 - mean_squared_error: 0.0560 - val_loss: 0.0461 - val_mean_squared_error: 0.0461

Epoch 00003: val_mean_squared_error improved from 0.05425 to 0.04606, saving model to model.h5
Epoch 4/50
40983/40983 [==============================] - 5s 123us/step - loss: 0.0487 - mean_squared_error: 0.0487 - val_loss: 0.0417 - val_mean_squared_error: 0.0417

Epoch 00004: val_mean_squared_error improved from 0.04606 to 0.04168, saving model to model.h5
Epoch 5/50
40983/40983 [==============================] - 6s 138us/step - loss: 0.0449 - mean_squared_error: 0.0449 - val_loss: 0.0394 - val_mean_squared_error: 0.0394

Epoch 00005: val_mean_squared_error improved from 0.04168 to 0.03938, saving model to model.h5
Epoch 6/50
40983/40983 [==============================] - 6s 137us/step - loss: 0.0426 - mean_squared_error: 0.0426 - val_loss: 0.0381 - val_mean_squared_error: 0.0381

Epoch 00006: val_mean_squared_error improved from 0.03938 to 0.03807, saving model to model.h5
Epoch 7/50
40983/40983 [==============================] - 5s 114us/step - loss: 0.0415 - mean_squared_error: 0.0415 - val_loss: 0.0374 - val_mean_squared_error: 0.0374

Epoch 00007: val_mean_squared_error improved from 0.03807 to 0.03738, saving model to model.h5
Epoch 8/50
40983/40983 [==============================] - 4s 107us/step - loss: 0.0404 - mean_squared_error: 0.0404 - val_loss: 0.0365 - val_mean_squared_error: 0.0365

Epoch 00008: val_mean_squared_error improved from 0.03738 to 0.03648, saving model to model.h5
Epoch 9/50
40983/40983 [==============================] - 9s 208us/step - loss: 0.0397 - mean_squared_error: 0.0397 - val_loss: 0.0359 - val_mean_squared_error: 0.0359

Epoch 00009: val_mean_squared_error improved from 0.03648 to 0.03593, saving model to model.h5
Epoch 10/50
40983/40983 [==============================] - 13s 314us/step - loss: 0.0389 - mean_squared_error: 0.0389 - val_loss: 0.0356 - val_mean_squared_error: 0.0356

Epoch 00010: val_mean_squared_error improved from 0.03593 to 0.03560, saving model to model.h5
Epoch 11/50
40983/40983 [==============================] - 8s 196us/step - loss: 0.0388 - mean_squared_error: 0.0388 - val_loss: 0.0354 - val_mean_squared_error: 0.0354

Epoch 00011: val_mean_squared_error improved from 0.03560 to 0.03543, saving model to model.h5
Epoch 12/50
40983/40983 [==============================] - 6s 150us/step - loss: 0.0383 - mean_squared_error: 0.0383 - val_loss: 0.0352 - val_mean_squared_error: 0.0352

Epoch 00012: val_mean_squared_error improved from 0.03543 to 0.03523, saving model to model.h5
Epoch 13/50
40983/40983 [==============================] - 4s 107us/step - loss: 0.0383 - mean_squared_error: 0.0383 - val_loss: 0.0350 - val_mean_squared_error: 0.0350

Epoch 00013: val_mean_squared_error improved from 0.03523 to 0.03503, saving model to model.h5
Epoch 14/50
40983/40983 [==============================] - 5s 110us/step - loss: 0.0380 - mean_squared_error: 0.0380 - val_loss: 0.0350 - val_mean_squared_error: 0.0350

Epoch 00014: val_mean_squared_error improved from 0.03503 to 0.03496, saving model to model.h5
Epoch 15/50
40983/40983 [==============================] - 8s 207us/step - loss: 0.0380 - mean_squared_error: 0.0380 - val_loss: 0.0349 - val_mean_squared_error: 0.0349

Epoch 00015: val_mean_squared_error improved from 0.03496 to 0.03494, saving model to model.h5
Epoch 16/50
40983/40983 [==============================] - 14s 337us/step - loss: 0.0378 - mean_squared_error: 0.0378 - val_loss: 0.0347 - val_mean_squared_error: 0.0347

Epoch 00016: val_mean_squared_error improved from 0.03494 to 0.03474, saving model to model.h5
Epoch 17/50
40983/40983 [==============================] - 8s 192us/step - loss: 0.0376 - mean_squared_error: 0.0376 - val_loss: 0.0347 - val_mean_squared_error: 0.0347

Epoch 00017: val_mean_squared_error improved from 0.03474 to 0.03467, saving model to model.h5
Epoch 18/50
40983/40983 [==============================] - 6s 135us/step - loss: 0.0376 - mean_squared_error: 0.0376 - val_loss: 0.0347 - val_mean_squared_error: 0.0347

Epoch 00018: val_mean_squared_error did not improve from 0.03467
Epoch 19/50
40983/40983 [==============================] - 4s 104us/step - loss: 0.0375 - mean_squared_error: 0.0375 - val_loss: 0.0345 - val_mean_squared_error: 0.0345

Epoch 00019: val_mean_squared_error improved from 0.03467 to 0.03454, saving model to model.h5
Epoch 20/50
40983/40983 [==============================] - 9s 227us/step - loss: 0.0374 - mean_squared_error: 0.0374 - val_loss: 0.0345 - val_mean_squared_error: 0.0345

Epoch 00020: val_mean_squared_error improved from 0.03454 to 0.03452, saving model to model.h5
Epoch 21/50
40983/40983 [==============================] - 14s 336us/step - loss: 0.0376 - mean_squared_error: 0.0376 - val_loss: 0.0345 - val_mean_squared_error: 0.0345

Epoch 00021: val_mean_squared_error improved from 0.03452 to 0.03445, saving model to model.h5
Epoch 22/50
40983/40983 [==============================] - 7s 182us/step - loss: 0.0375 - mean_squared_error: 0.0375 - val_loss: 0.0345 - val_mean_squared_error: 0.0345

Epoch 00022: val_mean_squared_error did not improve from 0.03445
Epoch 23/50
40983/40983 [==============================] - 5s 130us/step - loss: 0.0372 - mean_squared_error: 0.0372 - val_loss: 0.0345 - val_mean_squared_error: 0.0345

Epoch 00023: val_mean_squared_error did not improve from 0.03445
Epoch 00023: early stopping

