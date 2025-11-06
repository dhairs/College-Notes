### Dhairya Gupta (DG43932)

## Implementing Computational Graphs

### Report 1.1

Output of `python backprop.py --function f3`:

```
Output:
Checking outputs for function f3 (y=1)
  Output check passed!
Checking outputs for function f3 (y=2)
  Output check passed!
All output checks passed!
Running gradcheck for f3 (y=1)
  Gradcheck passed!
Running gradcheck for f3 (y=2)
  Gradcheck passed!
All gradchecks passed!
```

## Modular Backprop API

### Report 2.1

Output of `python3 check_softmax_stability.py`:

```
Input scores:
[[ 1000.     0. -1000.]
 [-1000.  1000.     0.]
 [    0. -1000.  1000.]]
Input labels: [0 1 2]
Output loss: -0.0
It seems like your softmax_loss is numerically stable!
```

Output of `python3 gradcheck_layers.py`:

```
Running numeric gradient check for fc
  grad_x difference:  5.947005110584769e-10
  grad_w difference:  4.703024636398823e-10
  grad_b difference:  3.166431561396621e-10
Running numeric gradient check for relu
  grad_x difference:  1.5110468432055768e-10
Running numeric gradient check for softmax loss
  grad_x difference:  1.733494181532791e-10
Running numeric gradient check for L2 regularization
  grad_w difference:  9.246078902513943e-11
```

## Implement a Two-Layer Network

### Report 3.1

Output of `python3 gradcheck_classifier.py`:

```
Running numeric gradient check for LinearClassifier
  Max diff for grad_W:  6.394884621840902e-13
  Max diff for grad_b:  5.067057884389214e-13
Running numeric gradient check for TwoLayerNet
  Max diff for grad_W2:  4.544975507059235e-16
  Max diff for grad_b2:  5.551115123125783e-16
  Max diff for grad_W1:  1.375635716449608e-15
  Max diff for grad_b1:  9.97465998686664e-16
```

## Training Two-Layer Networks

### Report 4.1

Hyperparameters used to train the model:

```py
# How much data to use for training
num_train = 20000

# Model architecture hyperparameters.
hidden_dim = 64

# Optimization hyperparameters.
batch_size = 128
num_epochs = 50
learning_rate = 6e-2
reg = 0.00012
```

![[loss accuracy.png]]

Final test-set accuracy for the model:

```
Loading model from checkpoint.pkl
Test-set accuracy: 43.52
```

### Report 4.2

Hyperparameters used to train the model:

```py
# How much data to use for training
num_train = 200

# Model architecture hyperparameters.
hidden_dim = 512

# Optimization hyperparameters.
batch_size = 128
num_epochs = 500
learning_rate = 6e-2
reg = 0.0
```

![[overfit.png]]

Final test-set accuracy for the model:

```
Loading model from checkpoint.pkl
Test-set accuracy: 23.76
```

## Train Your Own Classification Model

### Report 5.1

Attached as separate PDF.

### Report 5.2

Model details:

```py
Your network:
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 6, 24, 24]             156
              ReLU-2            [-1, 6, 24, 24]               0
         MaxPool2d-3            [-1, 6, 12, 12]               0
            Conv2d-4             [-1, 16, 8, 8]           2,416
              ReLU-5             [-1, 16, 8, 8]               0
         MaxPool2d-6             [-1, 16, 4, 4]               0
            Linear-7                  [-1, 120]          30,840
              ReLU-8                  [-1, 120]               0
            Linear-9                   [-1, 10]           1,210
================================================================
Total params: 34,622
Trainable params: 34,622
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.08
Params size (MB): 0.13
Estimated Total Size (MB): 0.21
```

I am using a Convolutional layer, followed by ReLU and a Maxpool layer. Then, I do that again with different kernels and strides. Finally, the classifier is just a linear fit with ReLU and Linear again.

Training and validation accuracy:

![[5.2.png]]

My hyperparameters:

```py
learning_rate = 1e-3
weight_decay = 1e-5
num_epoch = 10
```

### Report 5.3

I was able to get an accuracy of 89.4% (0.8937) with my best model.

## Pre-Trained NN

### Report 6.1

Image that is detected correctly (Bulbul):

![[image2.jpg|300]]

Image that is **not** detected correctly (Airplane is detected as "wing"):

![[image1.jpg|300]]

