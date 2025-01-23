## Topics

- Static and Quasi-static Force Analysis
	- Quasi static often means you are moving so slow you can neglect most dynamics. This can often be assumed in most basic robotics cases.
- Newton Laws
- Force, Torque, Wrench
- Friction
- Grasp

## Statics in Context

Statics is the study of particles and rigid bodies in equilibrium. Usually, this means that they are not moving or moving at a constant velocity. A foundation of statics helps understand physics of solids and dynamics.

## Types of Robotics Motion

There are two key types of motion in robotics: **translation** and **rotation**. 

## Newton's Laws of Physics
### Newton's First Law

A body in motion will remain in motion unless acted upon by a force. Conservation of momentum.

### Newton's Second Law
Force:
$F=ma$

Angular torque:
$\tau=I \cdot \alpha$

### Newton's Third Law


## Wrenches

A wrench is a 6D vector combining
- Force
- Torque

Wrenches are associated with a point of action (similarly to torque). Operating wrenches requires all of them to be in the same reference frame.

$\omega= [missing]\in R^6$

## How do Robots Measure Force/Torques?

The most common device is a sensor on the wrist. Some provide 6D wrenches. 

These are usually based on strain gauges.

### Strain Gauges

A strain gauge is a sensor that changes its electrical resistance depending on its shape/deformation. It can be used to measure forces and torques. 
