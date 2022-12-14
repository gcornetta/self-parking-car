# The JavaScript Self Parking Car

## Introduction 
Welcome to **Raspberry Pi Self-Parking car** tutorial. After completing this tutorial you will be able to:
1. write a simple *Electron Node.js* cross platform desktop application to simulate the parking algorithm.
2. implement obstacle detection and distance sensing using a *LIDAR*, *Node.js*, and JavaScript.
3. write the software to control a cheap robot car using *Node.js* and JavaScript running on an inexpensive Raspberry Pi 3B+ board.
4. use *Flutter* and *Dart* programming language to write a cross platform mobile application to control the robot car with your voice using the speech recognition APIs (Application Program Interfeces) of your smartphone.
5. set up a *Peer-to-Peer* Wi-Fi network connection between your smartphone and the Raspberry Pi robot car.

## Tutorial prerequisites
To understand this tutorial is desirable having some programming experience. A basic knowledge of JavaScript is desirable although is not essential since JavaScript has a very fast learning curve. In the future I am planning to add video tutorials to help novice programmers to successfully implement all the steps of this tutorial.

## Bill of Materials
To complete this tutorial you will need the materials and the equipment detailed in the sequel.

|         Item                              |    Price    |                                           Where to buy                                       |
|-------------------------------------------|:-----------:|---------------------------------------------------------------------------------------------:|
| Raspberry Pi 3B+                          |    $48      | [RS-Online](https://uk.rs-online.com/web/p/raspberry-pi/1373331?sra=pmpn)                    |
| 16 GB SD Card.                            |   $14.80    | [Amazon](https://www.amazon.com/Raspberry-Pi-16GB-Preloaded-Noobs/dp/B01H5ZNOYG/)            |                                           
| Spacers                                   |    $9.99    | [Amazon](https://www.amazon.com/HVAZI-270pcs-Female-Standoff-Assortment/dp/B01N1IUTVT/)      |
| Slamtec RP Lidar A1                       |   $99.99    | [Amazon](https://www.amazon.com/Slamtec-RPLIDAR-Scanning-Avoidance-Navigation/dp/B07TJW5SXF) |
| Sunfounder Robot car                      |   $99.99    | [Sunfounder](https://www.sunfounder.com/products/smart-video-car)                            |
| 2x 18650 3.7V rechargeable Li-ion Battery |   $17.99    | [Amazon](https://www.amazon.com/Rechargeable-Batteries-Flashlight-Doorbell-Shipping/dp/B0BCGVNLYX/) |
| 3D printing service                       | approx. $50 | [Treatstock](https://www.treatstock.co.uk)                                                   |

Make sure that the 18650 Li-ion batteries are **button-top** and try to purchase high-capacity batteries (those in the bill of materials are 3200mAh) to have a high operation time before they discharge. You might also want to purcgase a battery charger for the Li-ion batteries. You can find it on  [Amazon](https://www.amazon.com/Intelligent-Charger-Universal-Rechargeable-Batteries/dp/B08GH7RLD1/) for $27.99.

If you don't have a 3D printer, you will need printing services to 3D-print a chassis to place and fasten the Lidar on top of the Robot Car. You don't need tools to assemble the robot car and the chassis since they come out-of-the-box with the Sunfounder kit.

## Parking car simulator
The parking car simulator is an electron application derived from the [self-driving car simulator project](https://www.freecodecamp.org/news/self-driving-car-javascript/) described in **freeCodeCamp**. The code has been modified to work as a cross-platform electron app and to focus on **self parking** rather than self driving. You can find and download the code from my [car simulator GitHub repo](https://github.com/gcornetta/car-simulator). Read carefully the documentation and the prerequisites before downloading it or cloning my repo.

The simulator leverages a simplified *genetic algorithm* to train the neural network and a simple *loss function* to determine the fitness of the model, namely, to establish how well the neural network can park. A population of car is created with random weights and biases. At each iteration only the best car (namely, the one with the lowest losses or the best fitness) is selected. The best car is used as the starting point for the next generation. The process is repeated until it converges to the best possible solution.  

<div align="center">
<img src="https://github.com/gcornetta/self-parking-car/blob/main/screenshots/self-parking.gif" alt="Self parking car simulation" width="70%">
</div>

Simulation is the first step necessary to design a self-parking car. The result is an (hopefully) neural network model that must be included in the embedded software running on the **Pi Robot Car**. The simulator generates a **brain.json** file that contains neuron weights and biases of the best neural network (i.e., the *brain*) of the self-parking car. These weight and biases must be loaded in the **Pi Robot Car** neural network. 

## Getting familiar with the LIDAR
A Lidar (Light Detection and Ranging) is a remote sensing technique that allows finding the distance of an object or a surface using a laser impulse and measuring the time for the reflected light to return to the receiver.

For this activity I will use [Slamtec RP A1](https://www.slamtec.com/en/Lidar/A1). It is a cheap but performant device that can be easily coneected to a Raspberry Pi using either the GPIO or the USB port. You can buy it on [Amazon](https://www.amazon.com/Slamtec-RPLIDAR-Scanning-Avoidance-Navigation/dp/B07TJW5SXF) for less rhan $100.

I have written a vanilla javascript wrapper on top of the `@tsofist/rplidar` driver. You can find and download the code from my [RP Lidar GitHub Repo](https://github.com/gcornetta/RPLidar). Read carefully the documentation and the prerequisites before downloading it or cloning my repo. 

## Getting familiar with server-side JavaScript
We have simulated the parking algorithm and we are now ready to implement on a small prototype. The system is made of a cheap Raspeberry Pi based robotic kit and a smartphone running a simple voice command interface. Raspberry Pi runs a small server that receives commands over a WiFi network and controls the car hardware to perform the parking operation. The Raspberry Pi and Smartphone for a wireless ad hoc network with a P2P (peer to peer) connection. This means that Raspberry Pi and Smartphone can communicate directly, without passing through a router. In this scenario is the Raspberry Pi that has a static IP address and runs a DHCP server to dynamically assign to the client smartphone an IP address into a given range. 

However, we will go through this step by step, decoupling the server logic from the business logic thet controls the car hardware and performs the parking operation. An implementation of the `Node.js` server using the `Fastify` framework can be found [here](https://github.com/gcornetta/rpi-car-test-server). Use it to understand the basic structure of a simple HTTP server and to test the Mobile App by setting up a simple network.

## The mobile app
The mobile app is the client application that connects to the server running of the **Raspberry Pi robot car** The client is written in `Dart` using `Google Flutter`. Flutter is a mobile development framework that allows the development of cross-platformm mobile applications from a unique codebase (in Dart).
<div align="center">
<img src="https://github.com/gcornetta/self-parking-car/blob/main/screenshots/mobile-interface.gif" alt="Self parking mobile interface" width="30%">
</div>

At this stage of the development, the application is very easy. It is a simple speech recognizer application that is triggered by the keywork `Hello Car`. The word after the keyword is considered a command. The application just recognizes two commands: **park** and  **stop**. You can download the Flutter application from [here](https://github.com/gcornetta/self-parking-car-mobile-app).

## Robot car control software
The Raspberry Pi robot car control software is made up of three parts:
1. the device drivers.
2. the car control logic.
3. the server to connect with the client voice app.

The device drivers controls the car hardware, namely the two rear motors and the three servos tocontrol fron rear steering and front camera tilt and pan.
The servos are controlld by a `PCA9685` 16-channel servo driver. You can download the software driver of PCA9685 from [here](https://github.com/gcornetta/PCA9685.git). The robot car has two DC gear rear motors connected to the back wheels and controlled by a motor driver. The motor driver board has inputs to control the motor direction and a PWM input (from the `PCA9685` board) to control motor speed. You can download the motor software driver from [here](https://github.com/gcornetta/rpi-car-motor-driver.git).

## Setting up the P2P network
The mobile app running on the smartphone must be connected to the **Pi Robot Car**. The best option is using the WiFi interfaces of the Raspberry Pi that controls the Robot Car and of the smartphone to create a *Peer-to-Peer* network. To do this, you will learn how to install a DHCP (Dynamic Host Configuration Protocol) server on the Raspberry Pi. The DHCP server will be responsible to dynamically assign an IP address to all those devices that connect to the server network. Once the DHCP server has been configured, the new WiFi network will be visible by the smartphone and can be selected in the `settings`menu.

The steps to follow in order to configure a DHCP server a Raspberry Pi and to create a P2P connection with another device are available [here](https://github.com/gcornetta/self-parking-car/tree/main/docs/p2p.md).

## Assembling the chassis
The .STL (_Standard Tessellation Language_) file for 3D-printing the chassis to mount the Lidar of top of the Raspberry Pi board can be found [here](https://github.com/gcornetta/self-parking-car/blob/main/chassis/slam-head-rpi3-simple-Simple-Chassis_Full.stl). This chassis has been developed in this [YouTube turorial](https://www.youtube.com/watch?v=qNdcXUEF7KU). I still haven't printed it but it should be good for the purpose of this tutorial. In the future I am planning to develop my own chassis using Shapr3D cad and upload a video tutorial.

## Putting all together

## Roadmap
Software:
1. improve the mobile app user interface.
2. add more commands to the voice interface.

3D Printing:
1. improve the chassis.
2. create a 3D printing video tutorial using [Shapr 3D](https://www.shapr3d.com).

Teaching:
1. Create video tutorials.
2. Create course handouts.
