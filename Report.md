Arjun Raja ar6841 

Project 1 

Reinforcement learning and optimal control Arjun Raja – ar6841 

**Part 1** 

1. To discretize the system, we find the derivative of the state ˙ From Euler’s approximation we have: 

+1 −

˙ ≈

Δ

+1 = + Δ 

+ Δ

\+

- Δ ( 1 2) sin⁡
+ Δ

+1 = ( , ) = 1 + 2

+ Δ [( ) cos⁡ − ]
+ Δ

[ + Δ ![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.001.png)( 1 − 2) ]

2. Starting from an arbitrary position  (0)= 0,  (0)= 0 and  (0)=0. And we have, =0, =0, =0 

Thus to stay at rest forever,  +1 =⁡ . This leads to equations from the system dynamics,  

- 0
- 0
- 0

1 + 2 =

1 − 2 = 0 1 = 2 = 2![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.002.png)

3. It is not possible to *change* the x direction while keeping  =0 as⁡ = 0 (sin0 = 0) The drone will either hold the same x position or if there was a velocity before it will move in the x direction with constant velocity.
3. When  =![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.003.png) = − So the y position and velocity cannot be controlled as there is 2

a constant acceleration in y direction. Thus, the system cannot be at rest.

**Part 2** 

\1.  About some point ( ∗, ∗), from the first order Taylor series expansion:  +1 = ( ∗, ∗) + | ( − ∗) + | ( − ∗)⁡ ![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.004.png)![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.005.png)

∗, ∗ ∗, ∗

+1 = +

Where, 

2 
Arjun Raja ar6841 

1 Δ 0 0 0 1 0 0

0 0 1 Δ

\=

0 0 0 1

0 0 0 0 [0 0 0 0

0

- + ∗

−Δ ( 1 2) cos⁡ ∗ 0

−Δ ( 1∗ + 2∗) sin⁡ ∗

1 0

0

1 Δ 0 0 0 0

0 ∗ + ∗

0 1 0 0 −Δ ( 1 2) 0

0 ⁡= 0 0 1 Δ 0 

0 ⁡ 0  0 0 0 1 0 0 

0 0 0 0 1 Δ

Δ [0 0 0 0 0 1 ]

1 ]


Arjun Raja ar6841 

0 0

−Δt⁡sin⁡ ∗ −Δ ⁡sin⁡ ∗ 0 0

0 0

0 0

0 0 Δt⁡ Δt⁡

- Δt⁡cos⁡ ∗ Δt⁡cos⁡ ∗ =  ⁡ 

0 0

0 0 Δt⁡r Δt⁡r Δt⁡r Δt⁡r

- [ − ]

[ ]

1. The controller follows the equation:
- ( − ∗) + ∗
2. The cost function used is :

∞

∑ ( + ) 

=0

The LQR solution for infinite horizon is :  

- ⁡ ∶⁡ = ( − ∗) + ∗

48.4474     − 48.4474 58.2126     − 58.2126

- −24.0417     − 24.0417  −24.4604     − 24.4604  −102.5956     102.5956 [−9.1299     9.1299 ]
- + − ( + )−1( )
  - −( + )−1

Where  is the converged feedback gain obtained after solving the Riccati recursion 1000 times, We solve the equations :

- −( + )−1

+1 +1

- + +1 + +1

Till convergence of 

And the cost matrix, 

600 0 0 0 0 0

0 600 0 0 0 0

=⁡ 0 0 600 0 0 0  ⁡ ⁡ = [0.1 0  

]

0 0 0 600 0 0 0 0.1

0 0 0 0 1 0

[ 0 0 0 0 0 1]

This was made to punish the deviation from  = 0 of the x,  , , terms of the system more than the  , ⁡ as we need to deviate from  = 0, = 0 to control x position. Also, the R matrix is <1 so that control is not punished. The system can handle perturbations very well. 

Plots (Disturbance is False): 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.006.jpeg)

Plots (Disturbance is true):  

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.007.jpeg)

**Part 3** 

1. We must now linearize about each new set of ( ∗, ∗)⁡along the trajectory points. The linearization of the dynamics will take the form : 

+1 = +

- − ∗⁡ ⁡ = − ∗⁡ 

1 Δ 0 0 0 0

0 1 0 0 −Δ ( 1∗ + 2) cos⁡ ∗ 0 ∗

0 0 1 Δ 0 0

\=

0 0 0 1 −Δ ( 1∗ 2∗) sin⁡ ∗ 0 +

0 0 0 0 1 Δ

[0 0 0 0 0 1 ]

0 0          −Δt⁡sin⁡ ∗ −Δ ⁡sin⁡ ∗![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.008.png)![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.009.png)

0 0

- Δt⁡cos⁡ ∗ Δt⁡cos⁡ ∗

0 0

Δt⁡r Δt⁡r

[ − ]

Where each  and  must be found along the changing trajectory points. When we are on a circle of radius 1.  Let   denote this angle:  

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.010.jpeg)

Let**  =⁡2 ( )⁡ ℎ t is the current time (in seconds) and T is the total time taken to complete a circle 

The trajectory state points will take the form :  

cos⁡

−2

sin⁡ 

- = sin⁡

`  `2

cos⁡

0

[ 0 ] From the dynamics we can find, 

- =⁡− 4 2 sin⁡ 2
- = 1∗ + 2∗ −
- = 1∗ − 2∗ = 0 

Thus the control points will take the form: 

4 2

( − sin⁡ )

=⁡ 4 22![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.011.png)

- 2

[2 ( − 2 sin⁡ )]![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.012.png)

ℎ ⁡⁡ ⁡ℎ ⁡ ⁡ ⁡( ⁡ )⁡ ⁡ ⁡⁡ ⁡

2. The cost function used is : 

−1

( ∑ ( − ∗) ( − ∗) + ( − ∗) ( − ∗)) + ( − ∗ ) ( − ∗) 

=0

The tracking LQR solutions in this case are: 

- + +⁡ ∗

ℎ ⁡ ⁡ ⁡ ⁡⁡ ⁡ ⁡ ⁡ ⁡ℎ ⁡ ⁡ ⁡ ⁡ 

- − 1⁡ ⁡0 

Initialize ⁡ = ⁡ =

- − ∗

Iterate from  - I to 0 

- −( + +1 )−1 +1
- + +1 + +1
- −( + +1 )−1 +1
- + +1 + +1

The  term takes care of the feedforward required to track  ∗

Similar to part 2 of the project, the cost matrixes are given below. The difference here is that we punish deviation from the control trajectory  ∗ as we want to stay on the circle 

500 0 0 0 0 0

0 500 0 0 0 0

0 0 500 0 0 0 ⁡ ⁡ = [10 0 =⁡ ]

0 0 0 500 0 0 0 10

0 0 0 0 1 0

[ 0 0 0 0 0 1]

3. The  **cannot** be tracked well as we need to move in the x direction to complete the circular trajectory. For this reason, the Q matrix does not punish deviations in  as heavily. 
3. Plots : 

**Disturbance off** 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.013.jpeg)

**Disturbance on**: 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.014.jpeg)The results show that the x, y and velocities are sinusoidal waves as expected. The initial omega is high as the quadrotor spawns at 0,0 and must reach the circle, so the controller changes the  quickly to control the x and y locations. The controller also does a very good job at handling perturbations and returning to the required trajectory, although the x value deviates a bit as theta sharply changes due to wind disturbances. 

The control input also follows sinusoidal waves but initially have to overcompensate to reach the circle. 

Benefits: 

- The controller is able to track the trajectory for x,y very well. 
- Able to handle wind disturbances 

Drawbacks:  

- If the deviation from the trajectory is too large, the linearization does not hold true anymore and the controller will not be able to follow the trajectory 
- So if the radius of the circle was too big, the controller would never reach the circle from 0,0 
- We must solve the backward Riccati equations on every step. This can be slow for bigger states and controls. So if this problem was in 3D then every control step will be very slow. 
- The problem above would be magnified even more if we used an infinite horizon controller for following a trajectory on every step 
5. If we keep  = we will not be able to find a control trajectory from the dynamics, ![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.015.png)4

as there are 3 equations and two unknowns u1 and u2. To satisfy the state trajectory, we need to satisfy all the 3 equations:  

- −( 1 + 2)sin 
- ( 1 + 2)cos −
  - ( 1 − 2) = 0 

Which **will not be possible**.  

**Part 4** 

**Task 1** 

1. Cost function used to promote such behaviour:

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.016.png)

100 0 0 0 0 0

0 100 0 0 0 0

Where  ⁡ 0 0 100 0 0 0

=⁡

1 0 0 0 100 0 0

0 0 0 0 100 0

[ 0 0 0 0 0 100]

1 0 0 0 0 0 0 1 0 0 0 0

- 0 0 1 0 0 0 
- ⁡100000

2 0 0 0 1 0 0

` `0 0 0 0 1 0 [0 0 0 0 0 1]

1 0 0 0 0 0 0 1 0 0 0 0

- 0 0 1 0 0 0
- ⁡100000

0 0 0 1 0 0 0 0 0 0 1 0

[0 0 0 0 0 1]

- [0.1 0 ] 

0 0.1

3  0 

- 30  

` `2 ![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.017.png)

[0]

2. Quadratic approximation of cost: ( ∗, ∗)⁡ ⁡ ⁡ ⁡ ⁡

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.018.jpeg)**\** 

3. **Initial trajectory:** 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.019.jpeg)

**Final trajectory:** 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.020.jpeg)

Benefits:  

- Able to find a state and control trajectory very quickly 
- Quadrotor reaches the target very well
- We were able to find a locally optimal trajectory from the first guess
- Line search is able to fit a best guess for control

Issues:  

- If the cost function does not promote the behaviour well, the iLQR algorithm does not converge 
- The trajectory found is locally optimal and might not be the best solution. 
- There are sharp changes control and the velocities which might not work in real life 
- Again, if the problem was in 3D, the state and control vectors would be larger. Then  solving  the  backward  Riccati  equations  on  every  step  and  iterating through them would be very computationally expensive

**Task 2** 

New Cost function:  

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.021.png)

Where:  

10 0 0 0 0 0

0  10 0 0 0 0

=⁡ 0 0 10 0 0 0 ⁡⁡ = [0.1 0 ]

1  0 0 0 10 0 0 0 0.1

0 0 0 0 10 0

[ 0 0 0 0 0 10]

1 0 0 0 0 0 0 1 0 0 0 0 0 0 1 0 0 0

- ⁡100000 ∗

2 0 0 0 1 0 0 0 0 0 0 1 0

[0 0 0 0 0 1]

1 0 0 0 0 0

0 1 0 0 0 0

0 0 1 0 0 0 =⁡

3 0 0 0 1 0 0

` `0 0 0 0 10 0 [0 0 0 0 0 10]

1 0 0 0 0 0 0 1 0 0 0 0  0 0 1 0 0 0

- ⁡100000 ∗

0 0 0 1 0 0 0 0 0 0 1 0

[0 0 0 0 0 1]

1.5 3

0 0 =⁡3 ⁡⁡⁡ =⁡ 0

1 0 2 0

` `2 [0 ] [0 ]

Results :  

Initial trajectory:  

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.022.jpeg)

State and control trajectory found: 

![](Aspose.Words.2690dbc8-7969-4577-98ef-2aaaa41a7f0d.023.jpeg)The quadrotor is able to follow a trajectory that makes it do a  full flip. The x, y and theta positions at t=5 are 1.5, 3 and  respectively. This was exactly the target point. The control jumps at t = 5 from positive to negative for u2 and negative to positive for u1 very steeply. As a result, there are sharp changes in omega, vx and vy that make the motion seem a bit jerky. 

Benefits:  

- Able to find a state and control trajectory very quickly
- Quadrotor reaches the target very well
- We have a good approximation of the system

Issues: 

- There are solutions where the control is negative. This is quite clearly not possible in a real quadrotor  
- The cost must be very accurate to generate the required trajectory
- Sometimes with small changes in cost, the iLQR algorithm does not converge. 
- Again, if the problem was in 3D, the  state and control vectors  would be larger. Then solving the backward Riccati equations on every step and iterating through them would be very computationally expensive

We cannot run this controller on a real robot as on a real robot we will have constraints, such as u1 and u2 cannot be negative and cannot change  too quickly.  The real motors cannot handle the control generated by this program.
16 
