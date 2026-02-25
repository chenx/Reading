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

