# Robot leg guide

## **Intro**
In this quide we wil show you how you can control a leg of any quadruped robot using Spectral micro BLDC drivers. <br />If you can control one of them you can control all the rest! <br />

!!! Tip annotate "Python API and toolbox" 
    This guide leverages [Spectral BLDC python API](https://github.com/PCrnjak/Spectral-BLDC-Python/tree/main) and [Source robotics toolbox](https://github.com/PCrnjak/Source-Robotics-Toolbox)


<p align="left"> <img src="../assets/LEG.jpg" alt="drawing" width="800"/> <br /> </p>

!!! Note annotate "Building the LEG" 
    In this guide we only recommend you the hardware you can use to build the robot you designed. We do not offer already made designs you can build!

This guide will cover:

* How to define the robot leg kinematic chain
* How to control individual motors
* How to execute trajectories with the leg

What you will make a simple 2 DOF leg:

* 2 x spectral micro BLDC 
* Wires to connect everything up: [CAN wires](https://source-robotics.com/products/spectral-micro-can-cable), [Power wires](https://source-robotics.com/products/spectral-micro-power-cable)
* 2 x BLDC motors
* 1 x [CAN adapter](https://source-robotics.com/products/canvas-usb-to-can-adapter)
* 1 x 24V power supply
* A Laptop or raspberry pi

<p align="left"> <img src="../assets/leg_setup.png" alt="drawing" width="800"/> <br /> </p>

The setup will be the same for any kind of qadruped leg. You will need to follow the diagram above to wire everything up.

* First you need to calibrate your Spectral BLDC drivers with the motors you are using. 
* After that change the CAN ids of one of the drivers to CAN 1. You can do it by using UART commands: #CANID 1 and after that #Save
* Now connect CAN adapters CAN bus to one of the drivers and then from that driver connect to the second driver. Make sure that last driver in chain has its CAN termination resistor in "ON" state
* Connect the power to both drivers. (Use daisy chain)

## Leg kinematics

First you will need to assign coordinate frames to your leg model.
We already did it but if you want to learn more on how and why check this [Link](https://automaticaddison.com/how-to-assign-denavit-hartenberg-frames-to-robotic-arms/)<br />

Now we will need to find DH (Denavit-Hartenberg) table values. You can learn more on how and why we did it [Here!](https://automaticaddison.com/how-to-find-denavit-hartenberg-parameter-tables/)

## Controling individual motors

First we will show you a simple joint level trajectories we can execute with our robot leg. Joint level control involves directly controlling the angles or positions of the robot's individual joints. Each joint is treated as an independent actuator, and the control system sends commands to each joint to achieve the desired angles.

## Follow a specific trajectory

For this we will not use joint level control but a different method called Task/Cartesian Level Control.<br />
 Task or cartesian level control focuses on controlling the position and orientation of the robot's end-effector in a Cartesian coordinate system (X, Y, Z coordinates and orientations). In our robot leg case we dont have Z axes and our end-effector is foot (end of our robot leg).

In this example we will follow a circle trajectory i X,Y plane.
We defined that trajectory with our function xx and with parameters:

* 
*
* 
*
<p align="left"> <img src="../assets/circ_2.png" alt="drawing" width="800"/> <br /> </p>

How precise you follow the trajectory depends on the speed you set. With low speeds you can track the circle perflectly. With larger speeds the system cant keep up and overshoots. This is due multiple reaseons like:

* Inertia and Momentum: At higher speeds, the inertia and momentum of the robot leg increase, making it harder to change directions quickly and accurately.
* Centrifugal and Coriolis Forces
* Trajectory Planning and Execution - at higher speeds our trajectory has less points to create a full circle. This is due a fixed rate we send data to our motors eg. every 20ms. 
* Feedforward Control: Lack of proper feedforward control can lead to errors in trajectory tracking, as the controller might not anticipate the required accelerations and decelerations.

You can see that from the example with speed set to 1 and 3.