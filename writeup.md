# PID Control Project

The aim of this project is to implement a PID ( Propotional Integral and Derivative Controller) to keep a vehicle in the center of the road.This writeup discusses how each point in the project requirements are considered in the project implementation and also how the parameters of the controller is tuned.

### The follwoing steps are involved in designing the PID controller.
1. Identification of System Model
2. Controller Design

## System Identification
In order to design a controller it is important to understand the behaviour of the system. The following picture shows the overview of the control loop for controlling the steering of the vehicle.

![Control Loop](./Pictures/ControlLoop.png)

### Vehicle Model

The PID contorller receives from the simulator the cross track error, which is the distance of the vehicle from the center of the road. Then it should calculate the steering command value and sends back to the simulator which is applied to the car. In order to control the car its behaviour has to be understood i.e. how steering value(input variable) affects the postion of the car(output variable). Ideally a mathematical model to describe the motion of vehicle would be useful to design a controller. There are many ways to get such a mathematical model.One method is to use physical equations to describe the vehicle motion. Another method is to make experiments on the vehicle and estimate the model based on the input and output data which is called black box system identification which is a form of supervised learning. One of the common model used for describing the lateral dynamics of vehicle motion is called bicycle model, which reduces the wheels of car into two front and rear wheel. In this project a simplified verision of bicycle model is used to model the vehicle. The following picture shows the properties of the vehicle motion.

![Control Loop](./Pictures/SingleTrackModel.png)

The main assumption of the bicycle model is that the magnitude of the vehicle velocity is constant and the bicycle model can be used to calculate the vehicle position for a given steering angle. In this project instead of indentifying the parameters of physical equations of the bicycle model experimental data is used to estimate the transfer function between steering angle and the vehicle position. This project uses the same simulator used in the term - 1 project "Behaviour Cloning". The term-1 was modified to carry out the necassary experiments for estimating the transfer function. The simulator was modified to log the input and output data. The following table shows the input and output variables logged from the simulator. 

|Name|Type|Symbol|
|:-|:-|:-|
|Steering Angle| Input Variable| $\delta$|
|Speed| Output Variable (Considered constant - controlled by another PID  )| $\lvert V \rvert$|
|Position in X axis | Output Variable | X |
|Position in Y axis | Output Variable | Y |
|Yaw Angle(w.r.t X axis)| Output Variable | $\psi$|
|Angle of Velocity vector (w.r.t X axis)| Output Variable ( derived from X and Y)| $\nu$|
|Time||t|


When a vehicle is moving at a constant velocity giving a steering wheel angle causes the vehicle to yaw and change the direction of vehicle velocity. The position of the vehicle can be determined from the direction and magnitude of the velocity vector using the following equations.

$$\frac{dX}{dt} = |V|\cos\nu$$

$$\frac{dY}{dt} = |V|\sin\nu$$

Experiments are carried out to find the transfer function between the steering angle $\delta$ and the direction of velocity $\nu$ and then the above equations are used to calulate the position of the vehicle.
