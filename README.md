# Optimal control of a drone using the iterative Linear-Quadratic Regulator algorithm
<br> The goal of this project is to control a 2D quadrotor to perform acrobatic moves.

# 2D quadrotor

The quadrotor is depicted in the following figure <br>
<img src='outputs/quadrotor.png' width="300">
<br> The quadrotor dynamics is written as <br>

$$ \dot{x}  =v_x $$

$$m \dot{v}_x  =-\left(u_1+u_2\right) \sin \theta $$

$$ \dot{y}  =v_y $$

$$ m \dot{v}_y  =\left(u_1+u_2\right) \cos \theta-m g $$

$$ \dot{\theta}  =\omega $$

$$ I \dot{\omega}  =r\left(u_1-u_2\right)$$


where $x$ is the horizontal and $y$ the vertical positions of the quadrotor and $\theta$ is its orientation with respect to the horizontal plane. $v_x$ and $v_y$ are the linear velocities and $\omega$ is the angular velocity of the robot. $u_1$ and $u_2$ are the forces produced by the rotors (our control inputs). $m$ is the quadrotor mass, $I$ its moment of inertia (a scalar), $r$ is the distance from the center of the robot frame to the propellers and $g$ is the gravity constant. To denote the entire state, we will write $z = [x, v_x, y, v_y, \theta, \omega]^T$ - we will also write $u = [u_1, u_2]^T$.

The module ```quadrotor.py``` defines useful constants (mass, length, gravity, etc) and functions to simulate and animate the quadrotor as shown below.

For a more thorough and detailed explaination of the equations and derivations, refer to the report :
[Report.pdf](https://github.com/ar6841/Quadcopter_optimal_control_using_iLQR/blob/main/Drone_controller/Report.pdf)


## Jupyter notebooks
There are four simulations in total
Each Jupyter notebook is a simulation of the quadrotor performing a different task.

### Drone_at_origin : LQR to stay in place

A simple LQR controller that ensures that the robot stays in place at a predefined position even when pushed around by random disturbances (e.g. due to the wind).
<br> 
![](https://github.com/ar6841/Quadcopter_optimal_control_using_iLQR/blob/main/outputs/stable.gif)

### Circular_trajectory_drone: following a trajectory using linearized dynamics

A tracking controller (using an LQ design with linear approximations) to follow a circular trajectory under wind disturbances.
<br> 
![](https://github.com/ar6841/Quadcopter_optimal_control_using_iLQR/blob/main/outputs/Circular.gif)

### Drone_vertical : Drone reaching a vertical orientation

In this case, there is no prescribed trajectory but we would like to compute a locally optimal trajectory while we optimize the controller. We will use the *iterative LQR* algorithm to solve this problem.

Controller that makes the robot reach a vertical orientation $\theta = \frac{\pi}{2}$ at the location $x=3$ and $y=3$ at time $t=5$ starting from $z_0=0$. During the rest of the motion, the robot trys to stay close to the origin. It also trys to keep its control $u$ close to the control needed to keep the robot at rest.


<br>![](https://github.com/ar6841/Quadcopter_optimal_control_using_iLQR/blob/main/outputs/vertical.gif)

### Drone_flip : Drone doing a full flip

Controller that makes the robot do a full flip, trying to reach the upside-down state $x=1.5$, $y=3$ and $\theta = \pi$ at $t=5$ and upright state $x=3$, $y=0$ and $\theta = 2\pi$ at $T=10$.

<br>![](https://github.com/ar6841/Quadcopter_optimal_control_using_iLQR/blob/main/outputs/flip.gif)

### Drone_controller_full: Combination of all the jupyter notebooks

This is a combination off all notebooks for ease of use

