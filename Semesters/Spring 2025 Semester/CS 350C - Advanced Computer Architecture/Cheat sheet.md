## Robotics Equations Cheat Sheet

This document summarizes key equations from the provided robotics course slides.

### 02 Statics

- **Newton's First Law (Linear & Angular):**
    
    - ∑F=0: The sum of forces acting on a body at rest or moving at a constant velocity is zero.
        
    - ∑τ=0: The sum of torques (moments) acting on a body at rest or rotating at a constant angular velocity is zero.
        
- **Conservation of Momentum:**
    
    - p=m⋅v: Linear momentum (p) is mass (m) times velocity (v).
        
    - L=I⋅ω: Angular momentum (L) is moment of inertia (I) times angular velocity (ω).
        
- **Newton's Second Law (Linear & Angular):**
    
    - F=m⋅a: Force (F) equals mass (m) times acceleration (a).
        
    - τ=I⋅α: Torque (τ) equals moment of inertia (I) times angular acceleration (α).
        
- **Torque from a Force:**
    
    - τ=r×F: Torque (τ) is the cross product of the distance vector (r) from the point of application and the force vector (F).
        
- **Wrench:**
    
    - ω=[F τ​]∈R6: A wrench combines force (F) and torque (τ) into a single 6D vector.
        
- **Coulomb Friction (Dry Friction):**
    
    - Ff​≤μFN​: The friction force (Ff​) is less than or equal to the coefficient of friction (μ) times the normal force (FN​).
        
    - Static Friction (v=0): Ff​=Fstiction​≤μstiction​FN​⋅sign(P), where P is the applied force.
        
    - Kinetic Friction (v=0): Ff​=Fkineticfriction​=μkineticfriction​FN​⋅sign(v).
        
- **Viscous Friction:**
    
    - Ff​=μvf​FN​v: Viscous friction force (Ff​) is proportional to the sliding velocity (v), normal force (FN​), and the viscous friction coefficient (μvf​).
        

### 03 Physics of Materials

- **Friction Cone (Point on Plane Contact with Friction):**
    
    - F=f∣∣∣ftangent​∣∣≤μs​∣∣fnormal​∣∣,fz​≥0: The set of admissible forces (F) where the magnitude of the tangential force (∣∣ftangent​∣∣) is limited by the static friction coefficient (μs​) and the magnitude of the normal force (∣∣fnormal​∣∣), and the normal force (fz​) must be non-negative.
        
    - Cone Angle: β=tan−1μs​.
        
- **Soft-Finger Contact:**
    
    - F=(f,τnormal​)∣∣∣ftangent​∣∣≤μs​∣∣fnormal​∣∣,fz​≥0,∣τnormal​∣≤γfz​: Similar to the friction cone, but also includes the transmission of normal torque (τnormal​) limited by a torsional friction coefficient (γ) and the normal force (fz​).
        
- **Hooke's Law (Spring):**
    
    - −mg+kδ=0: In equilibrium, the force due to gravity (-mg) is balanced by the spring force (kδ), where k is the spring constant and δ is the displacement.
        
- **Stress (**σ**):**
    
    - σ=F/A0​: Normal stress is the applied force (F) divided by the original cross-sectional area (A0​).
        
- **Strain (**ϵ**):**
    
    - ϵ=Δl/l0​: Normal strain is the change in length (Δl) divided by the original length (l0​).
        
- **Hooke's Law (Material):**
    
    - σ=Eϵ: Stress is linearly proportional to strain within the elastic region, where E is Young's Modulus (the slope).
        

### 04 Joints

- **Grübler's Formula:**
    
    - M=k(n−1)−∑i=1j​(k−fi​)=k(n−1−j)+∑i=1j​fi​: Calculates the degrees of freedom (M) of a mechanism, where k is the DOF of a link (3 for planar, 6 for spatial), n is the number of links (including ground), j is the number of joints, and fi​ is the degrees of freedom allowed by joint i.
        
- **System Dynamics:**
    
    - q¨​=f(q,q˙​,u,t): Represents the dynamics of a system, where q¨​ is the acceleration, q is the position, q˙​ is the velocity, u is the control input, and t is time. (Note: Slide 18 used q˙​ for acceleration, common notation uses q¨​).
        

### 05 Analog Electronics

- **Current (i):**
    
    - i(t)=dtdq(t)​≈ΔtΔq​: Current is the rate of change of charge (q) with respect to time (t).
        
- **Ohm's Law:**
    
    - V=iR: Voltage (V) across a resistor equals the current (i) through it times its resistance (R).
        
- **Resistance (R):**
    
    - R=Aρl​: Resistance of a conductor depends on its resistivity (ρ), length (l), and cross-sectional area (A).
        
- **Capacitor Current:**
    
    - i=Cdtdv​: Current (i) through a capacitor is equal to its capacitance (C) times the rate of change of voltage (v) across it.
        
- **Inductor Voltage:**
    
    - vL​(t)=Ldtdi​: Voltage (vL​) across an inductor equals its inductance (L) times the rate of change of current (i) through it.
        
- **Resistors in Series:**
    
    - Req​=R1​+R2​+R3​+...: The equivalent resistance is the sum of individual resistances.
        
- **Resistors in Parallel:**
    
    - Req​=1/(1/R1​+1/R2​+1/R3​+...): The reciprocal of the equivalent resistance is the sum of the reciprocals of individual resistances.
        
- **RC Circuit Discharge:**
    
    - Vc​(t)=Vi​⋅e−t/RC: Voltage across a discharging capacitor (Vc​) decreases exponentially from an initial voltage (Vi​) with a time constant τ=RC.
        
- **RC Circuit Charge:**
    
    - Vc​(t)=Vs​(1−e−t/RC): Voltage across a charging capacitor (Vc​) increases exponentially towards the source voltage (Vs​) with a time constant τ=RC.
        
- **RL Circuit (Charging/Current):**
    
    - i(t)=RVs​​(1−e−Rt/L): Current through an inductor (i) increases exponentially towards its steady-state value (Vs​/R) with a time constant τ=L/R.
        
- **RL Circuit (Charging/Voltage across L):**
    
    - v(t)=Vs​e−Rt/L: Voltage across the inductor (v) decreases exponentially from the source voltage (Vs​) with a time constant τ=L/R.
        
- **RLC Circuit Steady State (DC):**
    
    - Capacitor acts as an open circuit (iC​=0).
        
    - Inductor acts as a short circuit (VL​=0).
        
- **Differential Amplifier:**
    
    - Vout​=A(V+−V−): Output voltage (Vout​) is the gain (A) multiplied by the difference between the non-inverting (V+) and inverting (V−) inputs.
        
- **Power (P):**
    
    - P=VI: Power is voltage (V) times current (I), measured in Watts.
        

### 06 Digital Electronics

- **Boolean Algebra (NOT):**
    
    - A=A: Double negation returns the original value.
        
- **Boolean Algebra (AND):**
    
    - A⋅A=A  
        
    - A⋅1=A  
        
    - A⋅0=0  
        
    - A⋅A=0 (Contradiction)
        
    - A⋅B=B⋅A (Commutative)
        
    - A⋅(B⋅C)=(A⋅B)⋅C=ABC (Associative)
        
- **Boolean Algebra (OR):**
    
    - A+0=A  
        
    - A+1=1  
        
    - A+A=1 (Tautology)
        
    - A+A=A  
        
    - (A+B)+C=A+(B+C)=A+B+C (Associative)
        
- **Boolean Algebra (Distributive):**
    
    - A⋅(B+C)=A⋅B+A⋅C  
        
- **Boolean Algebra Properties Summary:** (Includes Laws like Commutative, Associative, Distributive, Absorption, etc. listed on slide 33)
    
- **Example Combinatorial Logic Expression:**
    
    - Q=(A⋅B)​⋅(A+B)​⋅C: Example Boolean expression for a specific logic circuit.
        
- **Serial Adder Logic:**
    
    - Y=ab+ay+by: Next state (carry-out) equation for a serial adder.
        
    - s=a⊕b⊕y: Output (sum) equation for a serial adder (XOR operation).
        

### 07 Actuators

- **Torque-Speed Relationship (Linear Approximation):**
    
    - τ=−k1​ω+k2​ or ω=−k1′​τ+k2′​: Describes the inverse linear relationship between motor torque (τ) and speed (ω).
        
- **Power (Output):**
    
    - P=τ⋅ω: Mechanical output power is torque times angular velocity.
        
- **Efficiency (**η**):**
    
    - η=Input PowerOutput Power​: Ratio of mechanical output power to electrical input power.
        
- **Motor Circuit Model (Simplified):**
    
    - Ldtdi​=−Ri−Ke​ω+v(t): Electrical equation relating voltage (v(t)), current (i), resistance (R), inductance (L), back EMF constant (Ke​), and speed (ω).
        
    - Iα=Kt​i−cω: Mechanical equation relating inertia (I), angular acceleration (α), torque constant (Kt​), current (i), damping (c), and speed (ω).
        
- **Gear Train Mechanical Advantage (Simple Spur):**
    
    - Mechanical Advantage=ω2​ω1​​=r1​r2​​=N1​N2​​=T1​T2​​: Ratio of output to input speed (ω), radius (r), number of teeth (N), or torque (T).
        
- **Compound Gear Train Ratio:**
    
    - Ndriven​Ndriver​​=Product of teeth on driver gearsProduct of teeth on driven gears​ (Generalized from examples like N6​N1​​=N1​N3​N5​N2​N4​N6​​ or N4​N1​​=N1​N3​N2​N4​​).
        

### 08 States and Behaviors

- **Finite State Machine (FSM) Transition Function:**
    
    - S×Σ→S: Defines how the current state (S) and an input from the alphabet (Σ) determine the next state (S).
        
- **Markov Property:**
    
    - p(st+1​∣st​,st−1​,st−2​,...)=p(st+1​∣st​): The probability of the next state (st+1​) depends only on the current state (st​).
        

### 09 Introduction to Control

- **General State-Space Model (Continuous):**
    
    - z˙=F(t,z,u): State derivative (z˙) is a function of time (t), state (z), and input (u).
        
    - y=G(t,z,u): Output (y) is a function of time (t), state (z), and input (u).
        
- **Linear Time-Invariant (LTI) State-Space Model (Continuous):**
    
    - dtdz​=Az+Bu: State derivative is a linear combination of state (z) and input (u).
        
    - y=Cz+Du: Output (y) is a linear combination of state (z) and input (u).
        
- **General State-Space Model (Discrete):**
    
    - zt+1​=F(zt​,ut​): Next state (zt+1​) is a function of the current state (zt​) and current input (ut​).
        
    - yt​=G(zt​): Current output (yt​) is a function of the current state (zt​).
        
- **LTI State-Space Model (Discrete):**
    
    - zt+1​=Azt​+But​: Next state is a linear combination of the current state and input.
        
    - yt​=Czt​: Current output is a linear combination of the current state.
        
- **Control Error (e):**
    
    - e=x−xd​ or e=xd​−x: The difference between the actual state/output (x) and the desired state/setpoint (xd​).
        

### 10 PID Control Strategies

- **Cruise Control Model (Simplified):**
    
    - mv˙=−bv+fhill​+fengine​: Equation of motion for car velocity (v) considering mass (m), damping (b), hill force (fhill​), and engine force (fengine​).
        
- **Proportional Control Law (Simple):**
    
    - fengine​=k(vdesired​−v): Engine force is proportional (gain k) to the velocity error.
        
- **Steady State Velocity (Simple Proportional Control):**
    
    - vSS​=b+kk​vdes​+b+k1​fhill​: Steady-state velocity depends on desired velocity, gain, damping, and disturbance.
        
- **Engine Torque Model:**
    
    - Te​=uTm​(1−β(ωm​ω​−1)2): Engine torque (Te​) depends on control input (u), max torque (Tm​), efficiency (β), current speed (ω), and speed at max torque (ωm​).
        
- **Angular Speed to Velocity:**
    
    - ω=rn​v=αn​v: Engine speed (ω) is related to car velocity (v) via gear ratio (n) and wheel radius (r), or combined gain (αn​).
        
- **Force from Engine Torque:**
    
    - F=αn​Te​(αn​,v): Force generated by wheels (F) is engine torque (Te​) multiplied by the gain (αn​).
        
- **Disturbance Forces:**
    
    - Fg​=mgsin(θ): Force due to gravity on a slope (θ).
        
    - Fr​=mgCr​sgn(v): Rolling friction force, dependent on coefficient (Cr​) and direction of velocity (sgn(v)).
        
    - Fa​=21​ρCd​Av2: Aerodynamic drag force, dependent on air density (ρ), drag coefficient (Cd​), frontal area (A), and velocity squared (v2).
        
- **Full Cruise Control Dynamic Model (Nonlinear):**
    
    - mdtdv​=αn​uTm​(1−β(ωm​αn​v​−1)2)−(mgsin(θ)+mgCr​sgn(v)+21​ρCd​Av2): Combines engine force and disturbance forces.
        
- **Proportional (P) Control Law:**
    
    - u(t)=kP​e(t): Control input is proportional to the current error. (Often includes saturation limits and bias/feedforward uff​).
        
- **Proportional-Integral (PI) Control Law:**
    
    - u(t)=kP​e(t)+kI​∫0t​e(τ)dτ: Adds an integral term to eliminate steady-state error.
        
- **Proportional-Derivative (PD) Control Law:**
    
    - u(t)=kP​e(t)+kD​dtde(t)​: Adds a derivative term to improve transient response and damping.
        
- **Proportional-Integral-Derivative (PID) Control Law:**
    
    - u(t)=kP​e(t)+kI​∫0t​e(τ)dτ+kD​dtde(t)​: Combines all three terms.
        
    - Alternative form: u(t)=K(e(t)+Ti​1​∫0t​e(τ)dτ+Td​dtde​) where K=Kp​, Ti​=Kp​/KI​, Td​=KD​/Kp​.
        
- **Homogeneous 2nd Order ODE Solution:**
    
    - q(t)=eαt(Acosωt+Bsinωt): General form of the solution for mq¨​+cq˙​+kq=0.
        
- **Homogeneous 2nd Order Solution with ICs:**
    
    - q(t)=e−ζωn​t[qo​cosωd​t+(ωd​ζωn​​qo​+ωd​1​vo​)sinωd​t]: Solution in terms of initial position (qo​), initial velocity (vo​), natural frequency (ωn​), damping ratio (ζ), and damped frequency (ωd​).
        
- **Natural Frequency (**ωn​**):**
    
    - ωn​=k/m​.
        
- **Damping Ratio (**ζ**):**
    
    - ζ=2km​c​=2mωn​c​.
        
- **Damped Frequency (**ωd​**):**
    
    - ωd​=ωn​1−ζ2​.
        

### 11 PID with State-Space Models

- **1-Compartment Drug Model:**
    
    - Vdtdc​=−qc: Rate of change of concentration (c) depends on volume (V) and outflow rate (q).
        
    - dtdc​=−kc+bd​u: Simplified form with rate constants k and bd​, and input drug flow u.
        
- **2-Compartment Drug Model:**
    
    - dtdc1​​=−(k0​+k1​)c1​+k2​c2​+b0​u: Dynamics for compartment 1 concentration (c1​).
        
    - dtdc2​​=k1​c1​−k2​c2​: Dynamics for compartment 2 concentration (c2​).
        
    - State-Space Form: dtdc​=[−(k0​+k1​)​k2​ k1​​−k2​​]c+[b0​ 0​]u.
        
- **State Feedback Control Law:**
    
    - u=−Kc​z+kr​yd​(t): Control input (u) is a linear combination of the negative state vector (z) scaled by gains (Kc​) and the desired output (yd​) scaled by a feedforward gain (kr​).
        
- **Closed-Loop System Dynamics:**
    
    - dtdz​=(A−BKc​)z+Bkr​yd​(t): The dynamics of the system under state feedback control.
        
- **Characteristic Equation for Stability:**
    
    - p(s)=det(sI−(A−BKc​))=0: The roots (eigenvalues λ) of this equation determine stability. For stability, the real part of all eigenvalues must be negative (Re(λi​)<0).
        
- **2nd Order System (Alternative Form):**
    
    - x¨+2ζω0​x˙+ω02​x=0: Standard form using natural frequency (ω0​) and damping ratio (ζ).
        

### 12 Poses and Motion

- **Point Representation:**
    
    - p=[px​ py​ pz​​]∈R3: Represents a point p in 3D space using its coordinates.
        
- **Vector 2-Norm (Magnitude):**
    
    - ∣∣p∣∣2​=[p12​+p22​+...+pn2​]1/2: Calculates the Euclidean length (magnitude) of a vector p.
        
- **Inner (Dot) Product:**
    
    - ⟨p,q⟩=p⋅q=∑i=0n−1​pi​qi​=∣∣p∣∣2​∣∣q∣∣2​cos(θ): Computes the dot product of vectors p and q, related to the angle (θ) between them.
        
- **Angle Between Vectors:**
    
    - cos(θ)=∣∣p∣∣2​∣∣q∣∣2​p⋅q​: Calculates the cosine of the angle between vectors p and q using their dot product and magnitudes.
        
- **Cross Product Magnitude:**
    
    - ∣∣p×q∣∣=∣∣p∣∣∣∣q∣∣sin(θ): The magnitude of the cross product relates to the sine of the angle between vectors p and q.
        
- **Cross Product (3D):**
    
    - p×q=[p2​q3​−p3​q2​ p3​q1​−p1​q3​ p1​q2​−p2​q1​​]: Calculates the cross product vector for 3D vectors p and q.
        
- **Matrix Exponential:**
    
    - eA=I+A+2!A2​+3!A3​+...: Defines the matrix exponential using an infinite series.
        
- **Translation:**
    
    - p′=p+d: A translated point p′ is the original point p plus a displacement vector d.
        
- **Rotation in 2D:**
    
    - [x′ y′​]=[cosθ​−sinθ sinθ​cosθ​][x y​]: Rotates a 2D point (x, y) by angle θ.
        
- **Basic 3D Rotation Matrices:**
    
    - Rx​(θ)=[1​0​0 0​cosθ​−sinθ 0​sinθ​cosθ​]  
        
    - Ry​(θ)=[cosθ​0​sinθ 0​1​0 −sinθ​0​cosθ​]  
        
    - Rz​(θ)=[cosθ​−sinθ​0 sinθ​cosθ​0 0​0​1​]  
        
- **Properties of Rotation Matrices (R ∈ SO(3)):**
    
    - R−1=RT  
        
    - RTR=I  
        
    - det(R)=1  
        
- **Rodrigues' Rotation Formula:**
    
    - x′=n^(n^⋅x)+sinθ(n^×x)−cosθ(n^×(n^×x))  
        
- **Skew-Symmetric Matrix (Cross Product Operator):**
    
    - [n^]×​=[0​−nz​​ny​ nz​​0​−nx​ −ny​​nx​​0​]  
        
- **Rotation Matrix from Axis-Angle:**
    
    - R=I+sinθ[n^]×+(1−cosθ)[n^]×2  
        
- **Quaternion Representation:**
    
    - q=q0​+q1​i+q2​j+q3​k=(s,v)  
        
- **Quaternion Multiplication:**
    
    - qq′=(ss′−v⋅v′,sv′+s′v+v×v′)  
        
- **Quaternion Inverse:**
    
    - q−1=∣∣q∣∣22​(s,−v)​  
        
- **Rotation Matrix from Quaternion:**
    
    - R=[1−2q22​−2q32​​2q1​q2​−2q0​q3​​2q1​q3​+2q0​q2​ 2q1​q2​+2q0​q3​​1−2q12​−2q32​​2q2​q3​−2q0​q1​ 2q1​q3​−2q0​q2​​2q2​q3​+2q0​q1​​1−2q12​−2q22​​]  
        
- **Quaternion from Rotation Matrix:**
    
    - q0​=21​tr(M)+1​, q1​=4q0​m21​−m12​​, q2​=4q0​m02​−m20​​, q3​=4q0​m10​−m01​​  
        
- **Quaternion from Axis-Angle:**
    
    - q=(cos2θ​,asin2θ​)  
        
- **Linear Interpolation (Lerp):**
    
    - Lerp(t,a,b)=(1−t)a+tb  
        
- **Spherical Linear Interpolation (Slerp):**
    
    - Slerp(t,a,b)=sinθsin((1−t)θ)​a+sinθsin(tθ)​b, where θ=cos−1(a⋅b).
        

### 13 Transformations

- **General Displacement:**
    
    - x′=Rx+d  
        
- **Homogeneous Transformation Matrix:**
    
    - T=[R​p 0​1​]∈SE(3)  
        
- **Homogeneous Point:**
    
    - p~​=[p 1​]  
        
- **Applying Transformation:**
    
    - p~​′=Tp~​  
        
- **Transformation Matrix Inverse:**
    
    - T−1=[RT​−RTp 0​1​]  
        
- **Composition of Transformations:**
    
    - ATC​=ATB​BTC​  
        
- **Plücker Coordinates (Line Representation):**
    
    - Line: x(t)=p+tq  
        
    - Plücker coords: (q,q0​) where q0​=p×q  
        
    - Constraint: q⋅q0​=0  
        
- **Spatial Velocity (Twist):**
    
    - V=[ω v​]  
        
- **Adjoint Transformation (for Spatial Velocity):**
    
    - AV=[ARB​​0 [ApBORG​]×​ARB​​ARB​​]BV  
        

### 14 Forward and Inverse Kinematics

- **Forward Kinematics (FK):**
    
    - q∈Rn→x∈Rm  
        
    - Example (2-Link Planar): x=l1​c1​+l2​c12​, y=l1​s1​+l2​s12​ (using c1​=cosθ1​, s12​=sin(θ1​+θ2​), etc.)
        
- **Inverse Kinematics (IK):**
    
    - x∈Rm→q∈Rn  
        
- **Jacobian Matrix (J):**
    
    - x˙=J(q)q˙​  
        
    - Definition: Jij​=∂qj​∂fi​​, where x=f(q).
        
- **Velocity Inverse Kinematics:**
    
    - q˙​=J−1x˙ (if J is square and invertible).
        
    - q˙​=J+x˙ (using pseudo-inverse).
        
- **Condition Number:**
    
    - κ(J)=σmin​σmax​​  
        
- **Jacobian Transpose (Statics):**
    
    - τ=JTF  
        
- **Pseudo-Inverse:**
    
    - J+=JT(JJT)−1 (for m<n)
        
    - J+=(JTJ)−1JT (for n<m)
        
- **Denavit-Hartenberg (DH) Transformation:**
    
    - i−1Ti​=Rot(zi−1​,θi​)Trans(zi−1​,di​)Trans(xi​,ai​)Rot(xi​,αi​)  
        
    - Matrix form provided on slide 24.
        

### 16 Sensors and Vision

- **Robot Equation of Motion (Lagrangian Formulation):**
    
    - τ=M(q)q¨​+C(q,q˙​)q˙​+G(q)  
        
- **Pinhole Camera Model:**
    
    - x′=fzx​, y′=fzy​  
        
- **Camera Projection with Offset:**
    
    - (x,y,z)→(fzx​+cx​,fzy​+cy​)  
        
- **Homogeneous Coordinates:** (See Slide 12)
    
- **Camera Intrinsic Matrix (K - Homogeneous):**
    
    - K=[fx​​0​cx​​0 0​fy​​cy​​0 0​0​1​0​]  
        
- **Radial and Tangential Distortion Model (Plumb Bob):**
    
    - pc′​=pc​(1+k1​r2+k2​r4+k3​r6)+[2t1​xc​yc​+t2​(r2+2xc2​) t1​(r2+2yc2​)+2t2​xc​yc​​]  
        
- **Camera Projection (Full Model):**
    
    - pc​=K⋅Tcb​⋅pb​  
        
- **Visual Servoing - Image Jacobian:**
    
    - f˙​image​=Lξc​  
        

### 17 Motion Planning

- __A_ Search Heuristic:_*
    
    - F=g+h  
        

### 18 & 19 Machine Learning

- **Linear Regression Model:**
    
    - y=ax+b  
        
- **Sum of Squared Errors (SSE):**
    
    - SSE=∑i=1n​(yi​−y^​i​)2  
        
- **Least Squares Solution (Matrix Form):**
    
    - [∑xi2​​∑xi​ ∑xi​​n​][a b​]=[∑xi​yi​ ∑yi​​]  
        
- **Polynomial Regression Model:**
    
    - y=an​xn+...+a1​x+a0​  
        
- **Least Squares Loss (Polynomial):**
    
    - S=∑i=1N​(yi​−(an​xin​+...+a0​))2  
        
- **Bayes' Rule:**
    
    - P(Si​∣A)=∑j​P(Sj​)P(A∣Sj​)P(Si​)P(A∣Si​)​  
        
- **Naïve Bayes Classifier:**
    
    - p(li​∣F1​,...,Fn​)∝p(F1​∣li​)⋅...⋅p(Fn​∣li​)⋅p(li​)  
        
- **Artificial Neuron Output:**
    
    - o=f(∑i=1n​wi​xi​+b)  
        
- **Softmax Function:**
    
    - y^​i​=∑j​eoj​eoi​​  
        
- **Markov Decision Process (MDP) Definition:**
    
    - M=⟨S,A,P,R,γ⟩  
        
- **Transition Probability:**
    
    - Pss′a=Pr[st+1=s′∣st​=s,at​=a]  
        
- **Reward Function:**
    
    - r(s,a)=E[Rt+1​∣st​=s,at​=a]  
        
- **Policy (**π**):**
    
    - π:S→A or π(a∣s)=Pr[At​=a∣St​=s]  
        
- **Goal (RL):**
    
    - π∗=argmaxπ​E[∑t≥0​γtr(st​,π(st​))]  
        
- **Value Function (**Vπ(s)**):**
    
    - Vπ(s)=E[∑k=0∞​γkRt+k+1​∣St​=s]  
        
- **Action-Value Function (**Qπ(s,a)**):**
    
    - Qπ(s,a)=E[∑k=0∞​γkRt+k+1​∣St​=s,At​=a]  
        
    - Qπ(s,a)=r(s,a)+γ∑s′∈S​P(s′∣s,a)Vπ(s′)  
        
- **Bellman Equation (for V):**
    
    - Vπ(s)=∑a​π(a∣s)∑s′​∑r​p(s′,r∣s,a)[r+γVπ(s′)]  
        

### 20 Introduction to HRI

_(No specific mathematical equations presented in this slide deck)._