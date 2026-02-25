# Deep Learning with Python

- [Deep learning with Python](https://deeplearningwithpython.io/)

## Part I. DL Basics

### Chapter 1. What is DL

1.1 AI, ML and DL

1.2 Pre-DL: ML short history

1.2.1 Probability modeling

- Loss function (objective function)
- Logistic regression (logreg)

1.2.2 Early NN

- NN

1.2.3 Kernel method

- SVM

1.2.4 Decision Tree, Random Forest and GBM

- Decision Trees
- Random Forest
  - almost always 2nd best
  - became most popular since 2010 Kaggle got online, until replaced by GBM in 2014 
- GBM (Gradient Boosting Machine)
  - integrates weak models (such as D.T)
  - one of the best today. popular in Kaggle.

1.2.5 Back to NN

- Geoffrey Hinton, 2012, ImageNet; 2015: 96.4% accuracy: convnet

1.2.6 How is DL different

- Deep Learning
  - automates feature engineering
  - model learns all layers at the same time, not one by one (greedy)

1.2.7 Current state of DL

2016-2017: 2 major methods:
- GBM: structured data; XGBoost
- DL: image perception; Keras

1.3 Why DL? Why now?

LSTM: long short-term memory

- 3 forces:
  - Hardware
    - NVidia: GPU, cuda (2007)
    - Google: TPU (2016)
  - Dataset
    - Flickr: image labeling by user
    - Youtube
    - wikipedia: NLP
    - ImageNet: 1.4 million, 1000 types
  - Algorithm
    - shallow layers (1-2 layers): SVM, Random Forest
    - algorithm improvements for deep layers (> 10 layers):
      - activation function
      - weight-initialization scheme (gave up soon)
      - optimization scheme: RMSProp, Adam

Popularization
- Theano 
- TensorFlow
- Keras (2015)


### Chapter 2: Mathematics of DL

2.1 Example: digit recognition with MNist data

2.2 Data representation of NN

- tensor

2.2.1 Scalar (0D tensor): Numpy: float32, float64; ndim = 0 (rank)

2.2.2 Vector (1D tensor): ndim = 1

2.2.3 Matrix (2D tensor): ndim = 2

2.2.4 3D tensor and above

2.2.5 key attributes of a tensor: ndim, shape, dtype

2.2.6 Manipuate tensor in Numpy

2.2.7 Data batches

2.2.8 Real-world examples of data tensors

- vector data: 2D tensor; shape: (samples, features)
- time series: 3D tensor; shape: (samples, timesteps, features)
- image: 3D; shape: (samples, height, width, channels)
- vidoe: 5D; shape: (samples, frames, height, width, channels)

2.3 The gears of neural networks: Tensor operations

2.3.1 Element-wise operations

2.3.2 Broadcast

2.3.3 Tensor product

2.3.4 Tensor reshaping

2.3.5 Geometric interpretation of tensor operations 

- translation, rotation, scaling, linear transform, affine transform
- Dense layer with Relu activation

2.3.6 A geometric interpretation of deep learning

2.4 The engine of neural networks: Gradient-based optimization
