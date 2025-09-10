# ML

https://www.w3schools.com/ai/

## Intro

### Perceptrons

Asingle neuron with only one input layer, and no hidden layers.

### Neural Networks

Multi-Layer Perceptrons

In its simplest form, a neural network is made up from:

- An input layer
- A hidden layer
- An output layer

### Deep NN

- Use several hidden layers of neural networks that perform complex operations on massive amounts of data.
- Each successive layer uses the preceding layer as input.

### Deep Learning (DL)

A subset of Machine Learning.

## AI

Artificial Intelligence is a scientific discipline embracing several Data Science fields ranging from narrow AI to strong AI, 
including machine learning, deep learning, big data and data mining. 

AI (narrow AI) >> ML >> NN >> DL (Big Data, Strong AI)

### Narrow AI

Narrow Artificial Intelligence is limited to narrow (specific) areas like most of the AI we have around us today:

    Email spam Filters
    Text to Speech
    Speech Recognition
    Self Driving Cars
    E-Payment
    Google Maps
    Text Autocorrect
    Automated Translation
    Chatbots
    Social Media
    Face Detection
    Visual Perception
    Search Algorithms
    Robots
    Automated Investment
    NLP - Natural Language Processing
    Flying Drones
    IBM's Dr. Watson
    Apple's Siri
    Microsoft's Cortana
    Amazon's Alexa
    Netflix's Recommendations

Narrow AI is also called Weak AI.

Weak AI: Built to simulate human intelligence.

Strong AI: Built to copy human intelligence.

### Strong AI

Strong Artificial Intelligence is the type of AI that mimics human intelligence.

<br/>

## ML languages

Programming languages involved in Machine Learning and Artificial Intelligence are:

    LISP
    R
    Python
    C++
    Java
    JavaScript
    SQL

### R

R is a programming language for Graphics and Statistical computing.

R comes with a wide set of statistical and graphical techniques for:

    Linear Modeling
    Nonlinear Modeling
    Statistical Tests
    Time-series Analysis
    Classification
    Clustering

### Python

An advantage for using Python is that it comes with some very suitable libraries:

    NumPy (Library for working with Arrays)
    SciPy (Library for Statistical Science)
    Matplotlib (Graph Plotting Library)
    NLTK (Natural Language Toolkit)
    TensorFlow (Machine Learning)

### JavaScript

JavaScript Machine Learning Libraries

#### Brain.js
#### ml5.js
#### Math.js

#### TensorFlow 

TensorFLow playground: https://playground.tensorflow.org/

#### Plotting in the Browser

Here is a list of some JavaScript libraries to use for both Machine Learning graphs and other HTML charts:

    HTML Canvas
    Plotly.js
    Chart.js
    Google Chart
    D3.js

### WebGL API

- WebGL is a JavaScript API for rendering 2d and 3D graphics in any browser.
- WebGL can run on both integrated and standalone graphic cards in any PC.
- WebGL brings 3D graphics to the web browser. Major browser vendors Apple (Safari), Google (Chrome), Microsoft (Edge), and Mozilla (Firefox) are members of the WebGL Working Group.

E.g.: https://akirodic.com/p/jellyfish/

<br/>

## ML Perceptrons

https://www.w3schools.com/ai/ai_perceptrons.asp

### Perceptron Learning

- The perceptron can learn from examples through a process called training.
- During training, the perceptron adjusts its weights based on observed errors. This is typically done using a learning algorithm such as the perceptron learning rule or a backpropagation algorithm.
- Perceptrons are often used as the building blocks for more complex neural networks, such as multi-layer perceptrons (MLPs) or deep neural networks (DNNs).

### Pattern Recognition

https://www.w3schools.com/ai/ai_recognition.asp

### Training

https://www.w3schools.com/ai/ai_training.asp

Backpropagation

### Testing

### Learning

- Learning is looping.
- Gradient Descent
- Cost function (Error function)
- The Train Function

<img src="https://www.w3schools.com/ai/img_linear_regression_error.jpg" />

    E is the error (cost)
    N is the total number of observations (points)
    y is the value (label) of each observation
    x is the value (feature) of each observation
    m is the slope (weight)
    b is intercept (bias)
    mx + b is the prediction
    1/N * N∑1 is the squared mean value

### Terminology

- Label: label is the thing we want to predict.
- Features: the input
- Models: relationship between the label (y) and the features (x)
- Training
- Inference: the trained model is used to infer (predict) values using live data
- Phases:
  - Training: Input data are used to calculate the parameters of the model.
  - Inference: The "trained" model outputs correct data from any input.

<br/>

- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning
  - non-supervised learning but receives feedback from the user whether the decision is good or bad
- Self-Supervised Learning
  - similar to unsupervised learning because it works with data without human added labels.
  - The difference is that unsupervised learning uses clustering, grouping, and dimensionality reduction, while self-supervised learning draw its own conclusions for regression and classification tasks.

### Data

Sampling Terms
- Population
- Census
- Sample
  - Random samples
  - Sampling bias

Census vs Sample
- A Census is when we collect data for every member of a group.
- A Sample is when we collect data for some members of a group.
- A census is Accurate, but hard to do. A sample is Inaccurate, but is easier to do.

Big Data, Data mining

### Clustering

Clustering is a type of Unsupervised Learning.

Clustering is trying to:

    Collect similar data in groups
    Collect dissimilar data in other groups

Clustering Methods

    Density Method
    Hierarchical Method
    Partitioning Method
    Grid-based Method

Correlation Coefficient


### Regressions

Linear Regression

Polynomial Regression

### Deep Learning

The deep learning revolution started around 2010.

Since then, Deep Learning has solved many "unsolvable" problems.

#### Neurons

Scientists agree that our brain has between 80 and 100 billion neurons.

These neurons have hundreds of billions connections between them.

#### Tom Mitchell

Tom Michael Mitchell (born 1951) is an American computer scientist and University Professor at the Carnegie Mellon University (CMU).

#### The Giraffe Story

In 2015, Matthew Lai, a student at Imperial College in London created a neural network called Giraffe.

Giraffe could be trained in 72 hours to play chess at the same level as an international master.

Computers playing chess are not new, but the way this program was created was new.

Smart chess playing programs take years to build, while Giraffe was built in 72 hours with a neural network.

### Brain.js


# TensorFlow.js

https://www.w3schools.com/ai/ai_tensorflow_intro.asp

A popular JavaScript library for Machine Learning.

## Tensors

- TensorFlow.js is a JavaScript library to define and operate on Tensors.
- The main data type in TensorFlow.js is the Tensor.
- A Tensor is much the same as a multidimensional array.
- A Tensor contains values in one or more dimensions:

Teasor properties:
- dtype	The data type
- rank	The number of dimensions
- shape	The size of each dimension

### Creating a Tensor

- The main data type in TensorFlow is the Tensor.
- A Tensor is created from any N-dimensional array with the tf.tensor() method:

Tensor Shape

- A Tensor can also be created from an array and a shape parameter: 

### Retrieve Tensor Values

- You can get the data behind a tensor using tensor.data()
- You can get the array behind a tensor using tensor.array()
- tensor.rank, tensor.shape, tensor.dtype

### Tensor Data Types

A Tensor can have the following data types:

    bool
    int32
    float32 (default)
    complex64
    string

## TensorFlow Operations

    Add
    Subtract
    Multiply
    Divide
    Square
    Reshape

tensor.reshape()
- The number of elements in a tensor is the product of the sizes in the shape.
- Since there can be different shapes with the same size, it is often useful to reshape a tensor to other shapes with the same size.

<br/>

## TensorFlow Models

Models and Layers are important building blocks in Machine Learning.

- TensorFlow.js is supporting different types of Models and different types of Layers.
- A TensorFlow Model is a Neural Network with one or more Layers.

### A Tensorflow Project

A Tensorflow project has this typical workflow:

    Collecting Data
    Creating a Model
    Adding Layers to the Model
    Compiling the Model
    Training the Model
    Using the Model

### Tensorflow Optimizers

    Adadelta -Implements the Adadelta algorithm.
    Adagrad - Implements the Adagrad algorithm.
    Adam - Implements the Adam algorithm.
    Adamax - Implements the Adamax algorithm.
    Ftrl - Implements the FTRL algorithm.
    Nadam - Implements the NAdam algorithm.
    Optimizer - Base class for Keras optimizers.
    RMSprop - Implements the RMSprop algorithm.
    SGD - Stochastic Gradient Descent Optimizer.

### Training the Model

```
model.fit(xs, ys, {epochs:500}).then(() => {myFunction()});
```

### Using the Model

After the model is trained, you can use it for many different purposes.

<br/>

## TensorFlow.js Visor

    TensorFlow Visor is a graphic tools for visualizing Machine Learning
    It contains functions for visualizing TensorFlow Models
    Visualizations can be organized in Visors (modal browser windows)
    Can be used with Custom Tools likes d3, Chart.js, and Plotly.js
    Often called tfjs-vis

### Using tfjs-vis

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-vis"></script>
```


