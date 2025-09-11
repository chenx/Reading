# ML

https://www.w3schools.com/ai/

- [ML](#ml)
  * [Intro](#intro)
    + [Perceptrons](#perceptrons)
    + [Neural Networks](#neural-networks)
    + [Deep NN](#deep-nn)
    + [Deep Learning (DL)](#deep-learning--dl-)
  * [AI](#ai)
    + [Narrow AI](#narrow-ai)
    + [Strong AI](#strong-ai)
  * [ML languages](#ml-languages)
    + [R](#r)
    + [Python](#python)
    + [JavaScript](#javascript)
      - [Brain.js](#brainjs)
      - [ml5.js](#ml5js)
      - [Math.js](#mathjs)
      - [TensorFlow](#tensorflow)
      - [Plotting in the Browser](#plotting-in-the-browser)
    + [WebGL API](#webgl-api)
  * [ML Perceptrons](#ml-perceptrons)
    + [Perceptron Learning](#perceptron-learning)
    + [Pattern Recognition](#pattern-recognition)
    + [Training](#training)
    + [Testing](#testing)
    + [Learning](#learning)
    + [Terminology](#terminology)
    + [Data](#data)
    + [Clustering](#clustering)
    + [Regressions](#regressions)
    + [Deep Learning](#deep-learning)
      - [Neurons](#neurons)
      - [Tom Mitchell](#tom-mitchell)
      - [The Giraffe Story](#the-giraffe-story)
    + [Brain.js](#brainjs-1)
- [TensorFlow.js](#tensorflowjs)
  * [Tensors](#tensors)
    + [Creating a Tensor](#creating-a-tensor)
    + [Retrieve Tensor Values](#retrieve-tensor-values)
    + [Tensor Data Types](#tensor-data-types)
  * [TensorFlow Operations](#tensorflow-operations)
  * [TensorFlow Models](#tensorflow-models)
    + [A Tensorflow Project](#a-tensorflow-project)
    + [Tensorflow Optimizers](#tensorflow-optimizers)
    + [Training the Model](#training-the-model)
    + [Using the Model](#using-the-model)
  * [TensorFlow.js Visor](#tensorflowjs-visor)
    + [Using tfjs-vis](#using-tfjs-vis)
- [JS Graphics](#js-graphics)
  * [Graphic Libraries](#graphic-libraries)
    + [Plotly.js](#plotlyjs)
    + [Chart.js](#chartjs)
    + [Google Chart](#google-chart)
    + [D3.js](#d3js)
- [History](#history)
  * [History of AI](#history-of-ai)
  * [Theory of Mind](#theory-of-mind)
- [ML Mathematics](#ml-mathematics)
  * [Linear functions](#linear-functions)
  * [Linear Algebra](#linear-algebra)
  * [Vectors](#vectors)
  * [Matrices](#matrices)
  * [Tensors](#tensors-1)
    + [Tensor Ranks](#tensor-ranks)
    + [Real Tensors](#real-tensors)
    + [JavaScript Tensor Operations](#javascript-tensor-operations)
- [Statistics](#statistics)
  * [Statistics](#statistics-1)
    + [Inferential Statistics](#inferential-statistics)
    + [Descriptive Statistics](#descriptive-statistics)
      - [Descriptive Statistics Measurements](#descriptive-statistics-measurements)
  * [Descriptive Statistics (Tendancy)](#descriptive-statistics--tendancy-)
  * [Statistic Variability (Spread)](#statistic-variability--spread-)
  * [Distribution](#distribution)
  * [Probability](#probability)

<br/>

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

<br/>

# JS Graphics

## Graphic Libraries

JavaScript libraries to use for both Artificial Intelligence graphs and other charts:

    Canvas
    Plotly.js
    Chart.js
    Google Chart
    D3.js

### Plotly.js

Plotly.js is a charting library that comes with over 40 chart types, 3D charts, statistical graphs, and SVG maps.

### Chart.js

Chart.js comes with many built-in chart types:

    Scatter
    Line
    Bar
    Radar
    Pie and Doughnut
    Polar Area
    Bubble

### Google Chart

From simple line charts to complex tree maps, Google Chart provides a number of built-in chart types:

    Scatter Chart
    Line Chart
    Bar / Column Chart
    Area Chart
    Pie Chart
    Donut Chart
    Org Chart
    Map / Geo Chart

### D3.js
```
<script src="//d3js.org/d3.v3.min.js"></script>
```

<br/>

# History

## History of AI

https://www.w3schools.com/ai/ai_history.asp

## Theory of Mind

https://www.w3schools.com/ai/ai_mind.asp

<br/>

# ML Mathematics

## Linear functions

- Linear regressions
- Linear Least Squares

## Linear Algebra

- Scalars
- Vectors
- Matrices
- Tensors: A Tensor is an N-dimensional Matrix.

In JavaScript, a tensor is an array with multiple indices (indexes).

## Vectors

- Vectors are 1-dimentional Arrays
- Vectors have a Magnitude and a Direction
- Vectors typically describes Motion or Force 

## Matrices

- dimensions
- Square Matrices
- Diagonal Matrices
- Scalar Matrices
- The Identity Matrix
- The Zero Matrix
- Negative Matrices

<br/>

- Linear Algebra in JavaScript
- JavaScript Matrix Operations
  - Using math.js

```
 <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/9.3.2/math.js"></script>
```

- Matrix operations: add, sub, multiply, transpose, factorization

## Tensors

A Tensor is a N-dimensional Matrix:

- A Scalar is a 0-dimensional tensor
- A Vector is a 1-dimensional tensor
- A Matrix is a 2-dimensional tensor

A Tensor is a generalization of Vectors and Matrices to higher dimensions.

### Tensor Ranks

The number of directions a tensor can have in a N-dimensional space, is called the Rank of the tensor.

The rank is denoted R.

A Scalar is a single number.

    It has 0 Axes
    It has a Rank of 0
    It is a 0-dimensional Tensor

A Vector is an array of numbers.

    It has 1 Axis
    It has a Rank of 1
    It is a 1-dimensional Tensor

A Matrix is a 2-dimensional array.

    It has 2 Axis
    It has a Rank of 2
    It is a 2-dimensional Tensor

### Real Tensors

Technically, all of the above are tensors, but when we speak of tensors, we generally speak of matrices with a dimension larger than 2 (R > 2).

### JavaScript Tensor Operations

One of the most common libraries to use for tensor operations is called tensorflow.js.

```Tensor Addition:
const tensorA = tf.tensor([[1, 2], [3, 4], [5, 6]]);
const tensorB = tf.tensor([[1,-1], [2,-2], [3,-3]]);

// Tensor Addition
const tensorAdd = tensorA.add(tensorB);

// Result [ [2, 1], [5, 2], [8, 3] ]
```

<br/>

# Statistics

## Statistics

### Inferential Statistics

Inferential statistics are methods for quantifying properties of a population from a small Sample.

### Descriptive Statistics

Inferential statistics are methods for quantifying properties of a population from a small Sample:

#### Descriptive Statistics Measurements

Descriptive statistics are broken down into different measures:

**Tendency (Measures of the Center)**

    The Mean (the average value)value
    The Median (the mid point value)
    The Mode (the most common value)
    The Outlier

**Spread (Measures of Variability)**

    Min and Max
    Standard Deviation
    Variance
    Distribution
    Skewness
    Kurtosis

<br/>

## Descriptive Statistics (Tendancy)

## Statistic Variability (Spread)

## Distribution

- What is Normal Distribution?
- What is Margin of Error?
- What is Skewness?
  - Skewness is a distortion (an asymmetry) from the bell curve (normal distribution).
- What is Kurtosis?
  - Kurtosis is a also a distortion from the normal distribution (bell curve).
  - While skewness describes a unexpected values in one tail, kurtosis describes unexpected values in both tails.

## Probability

Probability is about how Likely something is to occur, or how likely something is true.

