# PID Control Project

The aim of this project is to implement a PID ( Propotional Integral and Derivative Controller) to keep a vehicle in the center of the road.This writeup discusses how each point in the project requirements are considered in the project implementation and also how the parameters of the controller is tuned.

### The follwoing steps are involved in designing the PID controller.
1. Identification of System Model
2. Controller Design

## System Identification
In order to design a controller it is important to understand the behaviour of the system. The following picture shows the overview of the control loop for controlling the steering of the vehicle.

![Control Loop](./Pictures/ControlLoop.png)

The PID contorller receives from the simulator the cross track error, which is the distance of the vehicle from the center of the road. Then it should calculate the steering command value and sends back to the simulator which is applied to the car. In order to control the car its behaviour has to be understood i.e. how steering value(input variable) affects the postion of the car(output variable). Ideally a mathematical model to describe the motion of vehicle would be useful to design a controller. There are many ways to get such a mathematical model.One method is to use physical equations to describe the vehicle motion. Another method is to make experiments on the vehicle and estimate the model based on the input and output data which is called black box system identification which is a form of supervised learning. Practically in many cases a mixture of both approach are used to determine the model which is called grey box modeling. One of the common model used for describing the lateral dynamics of vehicle motion is called bicycle model, which reduces the wheels of car into two front and rear wheel. In this project a simplified verision of bicycle model is used to model the vehicle. The following picture shows the properties of the vehicle motion.

![Control Loop](./Pictures/SingleTrackModel.png)
