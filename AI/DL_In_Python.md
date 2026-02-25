# Deep Learning with Python

- [Deep learning with Python](https://deeplearningwithpython.io/)

## Part I. DL Basics

### Chapter 1. What is DL

#### 1.1 AI, ML and DL

#### 1.2 Pre-DL: ML short history

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

#### 1.3 Why DL? Why now?

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

#### 2.1 Example: digit recognition with MNist data

#### 2.2 Data representation of NN

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

#### 2.3 The gears of neural networks: Tensor operations

2.3.1 Element-wise operations

2.3.2 Broadcast

2.3.3 Tensor product

2.3.4 Tensor reshaping

2.3.5 Geometric interpretation of tensor operations 

- translation, rotation, scaling, linear transform, affine transform
- Dense layer with Relu activation

2.3.6 A geometric interpretation of deep learning

#### 2.4 The engine of neural networks: Gradient-based optimization

2.4.1 What’s a derivative?

2.4.2 Derivative of a tensor operation: The gradient

2.4.3 Stochastic gradient descent

2.4.4 Chaining derivatives: The Backpropagation algorithm

#### 2.5 Looking back at our first example

<img width="609" height="455" alt="image" src="https://github.com/user-attachments/assets/ad9d9651-a679-439d-a394-e0c3b1595a12" />

Reimplementing our first example from scratch

Running one training step

The full training loop

Evaluating the model

#### Summary

- Tensors form the foundation of modern machine learning systems. They come in various flavors of dtype, rank, and shape.

- You can manipulate numerical tensors via tensor operations (such as addition, tensor product, or element-wise multiplication), which can be interpreted as encoding geometric transformations. In general, everything in deep learning is amenable to a geometric interpretation.

- Deep learning models consist of chains of simple tensor operations, parameterized by weights, which are themselves tensors. The weights of a model are where its “knowledge” is stored.

- Learning means finding a set of values for the model’s weights that minimizes a loss function for a given set of training data samples and their corresponding targets.

- Learning happens by drawing random batches of data samples and their targets and computing the gradient of the model parameters with respect to the loss on the batch. The model parameters are then moved a bit (the magnitude of the move is defined by the learning rate) in the opposite direction from the gradient. This is called mini-batch gradient descent.

- The entire learning process is made possible by the fact that all tensor operations in neural networks are differentiable, and thus it’s possible to apply the chain rule of derivation to find the gradient function mapping the current parameters and current batch of data to a gradient value. This is called backpropagation.

- Two key concepts you’ll see frequently in future chapters are loss and optimizers. These are the two things you need to define before you begin feeding data into a model:
  - The loss is the quantity you’ll attempt to minimize during training, so it should represent a measure of success for the task you’re trying to solve.
  - The optimizer specifies the exact way in which the gradient of the loss will be used to update parameters: for instance, it could be the RMSProp optimizer, SGD with momentum, and so on.


### Chapter 3. NN introduction

- TensorFlow (https://tensorflow.org)
- PyTorch (https://pytorch.org/)
- JAX (https://jax.readthedocs.io/)

#### 3.1 NN

- layers
- input data, objective
- loss function
- optimizer

<img width="446" height="383" alt="image" src="https://github.com/user-attachments/assets/c244d269-5796-4b5e-999e-be9db6a3a4bd" />

3.1.1 Layers

3.1.2 Model

- 2 branch
- multihead
- inception

3.1.3 loss function, optimizer (variation of SGD, Stochastic Gradient Descent)

#### 3.2 Keras introduction

<img width="609" height="363" alt="image" src="https://github.com/user-attachments/assets/b9c50ef6-4330-4276-ab36-910ef7d1ad83" />

3.2.1 Keras、TensorFlow、Theano and CNTK

<img width="349" height="224" alt="image" src="https://github.com/user-attachments/assets/d6ce4c07-fb84-4c3a-9103-ed3a407dcd38" />

- Tensor: Google
- Theano: Montreal University, MILA lab
- CNTK: Microsoft cognitive toolkit

3.2.2 Dev with Keras

#### 3.3 Establish DL workstation

3.3.1 Jupyter notebook

Recommended way of DL experiments.

3.3.2 Options running Keras

- Cloud: AWS EC2, AMI
- Local Unix

