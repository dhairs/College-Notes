# Definition
Kalman filtering is a recursive state filter. It's used for removing erroneous values and honing in on accurate state positions for quickly updating systems.

# How it works
**There are 7 steps associated with running a Kalman filter**

## Step 0. Initial State
Here, we initialize our Kalman filter with initial state values. If we have a position matrix and a covariance matrix, we use it.

## Step 2. Predicted State
Described by the equation: 

$$X_{k_p} = AX_{k_p}+Bu_k+w_k$$

Turns into the equation: 

$$

\begin{bmatrix}
1 & \Delta{t} \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
x_0 \\
u_k
\end{bmatrix}

$$