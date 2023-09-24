# Definition
Kalman filtering is a recursive state filter. It's used for removing erroneous values and honing in on accurate state positions for quickly updating systems.

# How it works
**There are 7 steps associated with running a Kalman filter**

### Example Values
Say we're given:

$$
v_{0x} = 280m/s, x_0=4000m
$$

## Step 0. Initial State
Here, we initialize our Kalman filter with initial state values. If we have a position matrix and a covariance matrix, we use it.

## Step 1. Predicted State
Described by the equation: 

$$X_{k_p} = AX_{k-1}+Bu_k+w_k$$

Where $A$ is $\begin{bmatrix} 1 & \Delta{t} \\ 0 & 1 \end{bmatrix}$ 
Where $X$ is our state matrix of the form $\begin{bmatrix} x_0 \\ v_{0x} \end{bmatrix}$

Turns into the equation: 

$$=
\begin{bmatrix}
1 & \Delta{t} \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
x_0 \\
v_k
\end{bmatrix}
+
\begin{bmatrix}
\frac{1}{2}\Delta{t}^2 \\
\Delta{t}
\end{bmatrix}
\begin{bmatrix}
a_{x_0}
\end{bmatrix}
+ 0
$$
Which, by [[Matrix Multiplication|matrix multiplication]] becomes: 

$$X_{k_p}=\begin{bmatrix} 
x_0\times\Delta{t} \\
v_k\times\Delta{t}
\end{bmatrix}
+
\begin{bmatrix}
\frac{a_{x0}}{2}\Delta{t}^2 \\
a_{x0}\times\Delta{t}
\end{bmatrix}
$$

In our system on the car, we can use an average between both IMU's every frame for the acceleration. $\Delta{t}$ will be provided to the method.

## Step 2. Initial Process Covariance Matrix
We use our process errors to develop this matrix. We will **only do this once.** This matrix is created from what we determine to be the error.

$$P_{k-1}=\begin{bmatrix}
\Delta{x}^2 & \Delta{x}\Delta{v}\\
\Delta{x}\Delta{v}  &\Delta{v_x}^2 
\end{bmatrix}$$

## Step 3. Predicted Process Covariance Matrix
The equation is given by 

$$\begin{align}
P_{k_p}=AP_{k-1}A^T+Q_R \\
= \begin{bmatrix} 1 & \Delta{t} \\ 0 & 1 \end{bmatrix} \begin{bmatrix}
\Delta{x}^2 & \Delta{x}\Delta{v}\\
\Delta{x}\Delta{v}  &\Delta{v_x}^2 
\end{bmatrix} \begin{bmatrix} 1 & 0 \\ \Delta{t} & 1 \end{bmatrix}
+ 0
\end{align}$$
So we are now given the Process Covariance Matrix as:

$$
P_{k_p}=\begin{bmatrix} 1 & \Delta{t} \\ 0 & 1 \end{bmatrix} \begin{bmatrix}
\Delta{x}^2 & \Delta{x}\Delta{v}\\
\Delta{x}\Delta{v}  &\Delta{v_x}^2 
\end{bmatrix} \begin{bmatrix} 1 & 0 \\ \Delta{t} & 1 \end{bmatrix}
$$

## Step 4: Calculating the Kalman Gain
The equation is given as:

$$K = \frac{P_{k_p}H^T}{HP_{k_p}H^T+R}$$
Where $H$ is a $2\times2$ identity matrix denoted as $\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$

So, in this case, the Kalman gain ends up being 

$$K = \frac{P_{k_p}}{P_{k_p}+R}$$
