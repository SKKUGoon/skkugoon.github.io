---
layout: post
title:  "AutoEncoder Anomaly Detection"
date:   2021-11-13 15:00:00 +0900
categories: algorithm
---


# Using Simple AutoEncoder as Anomaly Detection Algorithm

## Background
<p>
    Anomaly detection can play a serious role in financial system. 
    The model itself can provide whether the data is behaving like it always have been or not.
    However, traditional method in most Korean financial system - and certainly most widely used method due to its simplicity - 
    tends to assume the 2 sigma rules. 
</p>

### Old, Traditional method.
<p>
    "What is 2 sigma rules?" you might ask.
    In a normal distribution almost all observed data will fall within 3 standard deviation from the mean.
    Under this rule 68% of the data is included between the band of 1 standard deviation from the mean,
    and 95% of the data is included between the band of 2 standard deviation from the mean. 
    Consequently, when I say financial system uses 2 sigma rules, it is basically stating that:
    "Financial time series follows normal distribution"
</p>

<p>
    But no. It's been well proven that the financial time series doesn't exactly follows normal distribution.
    It is known that it has a tendency to show phenomenon such as volatility clustering. 
    Therefore, it exhibits much fatter tail than the normal distribution. 
    In this sense, it you still impose 2 sigma rules you rule out more observation as an "anomaly" than you actually think.
</p>

### PCA, AutoEncoder
<p>
    So is there a better and more elegant way to classify whether this observation is acting strange from others?
    Yes, in fact there's something called AutoEncoder. Well, there's PCA, too but in a certain sense they both work in a similar fashion.
    PCA projects dataset into a new coordinate system. 
    In process it puts some scalar projection of the data that has greatest variance(explained) first,
    and other projection that explains little of the variance at the back. 
</p>

```
import numpy as np
import pandas as pd

def gen_factor(X):    
    
```
<p>
    After observation, you can see that the factor loading in the first column shows the general trend or momentum.
    As you move down to the second column you can see that the momentum is gone and it is replaced by some wave like noises.
    If you use all of the matrix, or 100% or explained variance, you are effectively using all of the original data.
    However, it your objective is to reduce dimension, you can leave out the columns located at the far back.
    Leaving those columns out means that you are assuming dropping small noises and thereby increasing the chance of your data to be generalized and prevent any models from being overfitted
    - which is important thing in a data-oriented society. 
</p>


<p>
    AutoEncoder works somewhat similarly to PCA. In fact, a single layer AutoEncoder with linear activation function gives nearly identical results to that of PCA.
    However, AutoEncoder has much more potential, because while PCA is constrained in linear space, PCA can employ both linear and non-linear methods.
    Essentially AutoEncoder reduces the dimension of the data and then grow it back to the original size. 
    The input data and the output data are both feature data, so there's no need to have a target data - that's why it's called unsupervised learning. 
    In the process of finding the optimal betas for all of the non-linear or linear regression in the neural network system,
    the result of encoding layers becomes dataset that best explains the whole dataset.
</p>

<p>
    The typical shape of the AutoEncoder is presented all around the all mighty google,
    so I don't think there's a need to show pictures of the typical AutoEncoder 
</p>


## Implementation

### Finding anomaly. - Intuition
<p>
    So how can we use AutoEncoder as a way to find anomaly? This was the big question of this post wasn't it? 
    The intuition is simple: if one uses only normal data(normally acting data) to train the AutoEncoder and use the fitted model to predict
    dataset that has mixture of normal and abnormal data, the prediction error of abnormal data will be all over the place. 
    We can just set a threshold for prediction error and if it goes off the chart, we will define it as an anomaly. 
</p>

<p>
    For demonstration I will be using simple AutoEncoder. I messed around with the hidden layers and dropout rate, but not much else.
    To prevent the model from being overfitted, I used earlystop callback to stop the training process whenever the monitoring variable fails to improve.
    Also to monitor the whole process, I've utilized tensorboard callback.
</p>

```
import tensorflow as tf


def callbacks_tb(logging, name):
    tb = tf.keras.callbacks.TensorBoard(
        log_dir=f"{logging}{name}",
        histogram_freq=1
    ) 
    return tb

def callbacks_es(monitor_val, waitfor):
    es = tf.keras.callbacks.EarlyStopping(
        monitor=monitor_val,
        patience=waitfor
    )
    return es
```

