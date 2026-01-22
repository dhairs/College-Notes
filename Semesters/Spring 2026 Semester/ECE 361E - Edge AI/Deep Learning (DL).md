## Applications of Deep Learning

### Computer Vision

Can be applied for tasks like image classification, object detection, and image segmentation.

### Internet of Things (IoT)

Often used for activity recognition, social sensing, and affective computing.

### Speech and Language Modeling

Text to speech and speech to text.

### Generative Models

Text to image, large language models.

## Fundamental Machine Learning Algorithms

Machine Learning usually encompasses supervised learning, unsupervised learning, and reinforcement learning.

### Supervised Learning

Two big classes of problems within this: Classification and Regression.

#### Classification

Classification predicts integers/classes. The objective is to *guess* the right class. Essentially, try to take some data and categorize it.

#### Regression

Regression predicts real values. The objective is to get close to the actual value. Essentially, try to take some set of inputs and guess what the value of those inputs may result in (think linear regression).

#### Supervised Classification and Regression Tasks

Maps input data to an output prediction.

**Classification** tasks predict a **discrete** category/label. E.g. predict main object in an image.

**Regression** tasks predict a **continuous** set of values.


> [!FAQ]+ What is Inside the Model?
> Real world input → Model input → **Model** → Model output → Real world output
> 
> A machine learning model is a mathematical equation described by a set of parameters that determine the input-output relationship. A learning algorithm uses examples of input-output pairs to find a set of parameters (**train** the model) which predict the relationship most accurately.


### Unsupervised Learning

Two big classes of problems within unsupervised learning: Clustering and Association.

### Reinforcement Learning

Mainly its own field. 

## Building off of Linear Models

Linear models can separate non-linear data if we transform the features


| ![[Linear Model Separation.png]]                                                                           |
| ---------------------------------------------------------------------------------------------------------- |
| [Source](https://medium.com/@sachinkun21/using-a-linear-model-to-deal-with-nonlinear-dataset-c6ed0f7f3f51) |
However manual feature engineering becomes complex in high dimensions. E.g. an MNIST image is $x \in \mathbb{R}^{28\times 28}$ if we treat it as a vector. 

As a result, we want to find if we can somehow automate or *learn* this linearization.

