## Generating Updated *Position*

### Basic Equation
$\text{Original Position} + \int_{0}^{\Delta t}v(x)\mathrm{d}x + \int_{0}^{\Delta t}a(x)\mathrm{d}x$
### Given Position, Velocity, and Acceleration 
$\text{Original Position} + (\Delta t * \text{current velocity}) + (\Delta t * \text{current acceleration})$

#### Estimating with Rotation
We'll use rotation matrices for this, with the $x$ and $y$ directions.
