# Robot leg guide


## **Intro**
In this quide we wil show you how you can control a leg of any quadruped robot using Spectral micro BLDC drivers. <br />If you can control one of them you can control all the rest! <br />

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
* 1 x CAN adapter
* 1 x 24V power supply
* A Laptop or raspberry pi

<p align="left"> <img src="../assets/leg_setup.png" alt="drawing" width="800"/> <br /> </p>

The setup will be the same for any kind of mobile robot. You will need to follow the  diagram above to wire everything up.

* Firstly you need to calibrate your Spectral BLDC drivers with the motors you are using. 
* After that change the CAN ids of one of the drivers to CAN 1. You can do it by using UART commands: #CANID 1 and after that #Save
* Now connect CAN adapters CAN bus to one of the drivers and then from that driver connect to the second driver. Make sure that last driver in chain has its CAN termination resistor in "ON" state
* Connect the power to both drivers. (Use daisy chain)
