## Connecting to Deformable Bodies

Deformable bodies are like pistons
- when supporting a mass, they deform until the 'reactive force' equals the weight of the object
- harder objects have large K, soft objects lower K

Until the deformation required to counteract the mass is too large, and then it breaks.

## Stress-Strain Relationship

Why?
- Choosing materials for robot components
- Choosing gripper material
- Task dependent: go from A to B, apply force F with sufficient positional tolerance
- We want lightweight robots
	- Low energy, cheap, safe
- We want robust robots
	- 20,000+ hours of service
- We want precise robots
	- No (or well modeled) deformation

### Stress

Stress: imagine that for a rod made of a certain material that we are considering for our robot pulling force (tensile) is applied from both sides. The **mechanical stress** is defined as the force divided by the cross-section area: $\sigma=\frac{F}{A_{0}}$.

### Strain

Imagine that with this pulling force, our rod stretches a bit ($\Delta l$)
- Strain: the ratio of change in length by the length when no force is applied
$\epsilon=\frac{\Delta l}{l_{0}}$

### The Relationship

At low pulling forces, stress-strain have a linear relationship for both.

Hook's law: $\sigma=E \epsilon$

The slope is called the Youngs modulus ($E$)
- Units of pressure
	- Pa
	- Pounds per square inch (PSI)

The linear portion of the stress-strain curve is also called the elastic regime
- The material will recover its original shape if the load is removed

The second portion is the plastic regime
- More load leads to yield permanent change of shape


## Shear Force and Bending Moment

When a beam is loaded, there are internal forces that appear to maintain equilibrium.
- Forces parallel to the beam section
- Forces perpendicular to the beam section (along the beam)

**Shear force** is the force parallel to the cross section of the beam. The **bending moment** is caused by unequal forces along the beam, creating a torque/moment.