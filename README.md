# Model Predictive Control Project
Self-Driving Car Engineer Nanodegree Program

The objective of this project is to use model predictive control to enable a car to drive around a track in a simulator. The final control performance is shown in video Final_Video.

## The Model
Student describes their model in detail. This includes the state, actuators and update equations.

State [x,y,ψ,v]:
The state can be described using four components:
- x: the x-position
- y: the y-position
- ψ: the vehicle orientation
- v: the velocity

Actuators [δ, a]:
An actuator is a component that controls a system. Here we have two actuators: 
- δ (the steering angle) and 
- a (acceleration, i.e. throttle and brake pedals).

Update equations (Vehicle Dynamics)
x = x + v*cos(ψ)*dt 
y = y + v*sin(psi)*dt
v=v+a*dt
ψ=ψ+(v/L_f)*δ*dt

## Timestep Length and Elapsed Duration (N & dt)
Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

N is the number of timestep that the model predicts ahead. As N increases, the model predicts further ahead, but it will use more computational power.
dt is the length of each timestep. As dt decreases, the model re-evaluates its actuators more frequently. This may give more accurate predictions, but it will use more computational power.
I start with the value of (N=5, dt=0.1), but the fitting performance is not very good because the timestep length is too short, then I increase N to (N=10, dt = 0.1), then the fitting performance looks much better. 

## Polynomial Fitting and MPC Preprocessing
A polynomial is fitted to waypoints. If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.

A 3rd order polynomial is fitted to the waypoints. The waypoints returned by server are given in map’s coordinate system, so a coordination transformation is applied to transform the waypoints into car’s coordinate system as shown in line 99-107 of main.cpp.

## Model Predictive Control with Latency
The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.

The MPC can successfully handle the 100ms actuator latency. As shown in line 116-124 of main.cpp,  we use the kinematic model to predict the state 100ms ahead of time and then feed that predicted state into the MPC solver. 
