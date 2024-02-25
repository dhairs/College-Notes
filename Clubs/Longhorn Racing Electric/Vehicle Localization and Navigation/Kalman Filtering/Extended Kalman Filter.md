# Calculating Non-Linear Vehicle State

We will be using an Extended Kalman filter to calculate the vehicles state as a non-linear first order method (because using theta makes the whole [system non-linear](https://en.wikipedia.org/wiki/Nonlinear_system)).

Because we have "truthy" or "real" IMU acceleration values, we can define our state matrix without those values, and instead use them as our *control* input ($u$).

## System Matrices
The following is the system's **state matrix**, $\hat{x}$:

$$
\hat{x}=
\begin{bmatrix}  
x \\
\dot{x} \\
y  \\
\dot{y} \\
\theta
\end{bmatrix}
$$

With the given inputs, we can define our **control matrix**, $u$:

$$
u=
\begin{bmatrix}  
\ddot{x} \\
\ddot{y} \\
\dot{\theta}
\end{bmatrix}
$$

Because we have a theta, we will also be using a [[Rotation Matrices|rotation matrix]] to globalize the vehicles positioning.

And all the **perfect estimate equations** are:

$$\begin{align}
   \text{system perfect estimate}=\left\{
\begin{array}{ll}
      x_\text{new}=x_\text{old}+v_{x_\text{old}}\times\Delta t + \frac{1}{2}\Delta t^2 (a_{x_\text{old}}\cos(\theta)-a_{y_\text{old}}\sin(\theta)) \\
	  
	  y_\text{new}=y_\text{old}+v_{y_\text{old}}\times\Delta t + \frac{1}{2}\Delta t^2 (a_{x_\text{old}}\sin(\theta)+a_{y_\text{old}}\cos(\theta)) \\
	
	  \dot{x}_\text{new}=\dot{x}_\text{old}+\Delta t(a_{x_\text{old}}\cos(\theta)-a_{y_\text{old}}\sin(\theta)) \\
	  
	  \dot{y}_\text{new}=\dot{y}_\text{old}+\Delta t(a_{x_\text{old}}\sin(\theta)+a_{y_\text{old}}\cos(\theta)) \\
	  
	  \theta_\text{new}=\omega\times\Delta t+ \theta_\text{old}
\end{array} 
\right. 
\end{align}$$

## Predict Steps

The $\hat{x}$ state is defined as such: $\hat{x}_{k|k-1}=f(\hat{x}_{k-1|k-1},u_{k-1})$.

The function $f(\cdot)$ is defined by the perfect estimate equations listed above.