# Self-parking-car

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

|         Item         |      Price      |                                  Where to buy                              |
|----------------------|:---------------:|---------------------------------------------------------------------------:|
| Raspberry Pi 3B+     |       $48       | [RS-Online](https://uk.rs-online.com/web/p/raspberry-pi/1373331?sra=pmpn)                    |
| 16 GB SD Card.       |       $14.80    | [Amazon](https://www.amazon.com/Raspberry-Pi-16GB-Preloaded-Noobs/dp/B01H5ZNOYG/)            |                                           
| Spacers              |       $9.99     | [Amazon](https://www.amazon.com/HVAZI-270pcs-Female-Standoff-Assortment/dp/B01N1IUTVT/)      |
| Slamtec RP Lidar A1  |       $99.99    | [Amazon](https://www.amazon.com/Slamtec-RPLIDAR-Scanning-Avoidance-Navigation/dp/B07TJW5SXF) |
| Sunfounder Robot car |       $99.99    | [Sunfounder](https://www.sunfounder.com/products/smart-video-car)                            |
| 3D printing service  |  approx. $50    | [Treatstock](https://www.treatstock.co.uk)                                                   |

If you don't have a 3D printer, you will need printing services to 3D-print a chassis to place and fasten the Lidar on top of the Robot Car. You don't need tools to assemble the robot car and the chassis since they come out-of-the-box with the Sunfounder kit.

## Parking car simulator
The parking car simulator is an electron application derived from the [self-driving car simulator project](https://www.freecodecamp.org/news/self-driving-car-javascript/) described in **freeCodeCamp**. The code has been modified to work as a cross-platform electron app and to focus on **self parking** rather than self driving. You can find and download the code from my [car simulator GitHub repo](https://github.com/gcornetta/car-simulator). Read carefully the documentation and the prerequisites before downloading it or cloning my repo.

![alt self parking car](./screenshots/self-parking.gif "Self parking car simulation")

## Getting familiar with the LIDAR
A Lidar (Light Detection and Ranging) is a remote sensing technique that allows finding the distance of an object or a surface using a laser impulse and measuring the time for the reflected light to return to the receiver.

For this activity I will use [Slamtec RP A1](https://www.slamtec.com/en/Lidar/A1). It is a cheap but performant device that can be easily coneected to a Raspberry Pi using either the GPIO or the USB port. You can buy it on [Amazon](https://www.amazon.com/Slamtec-RPLIDAR-Scanning-Avoidance-Navigation/dp/B07TJW5SXF) for less rhan $100.

I have written a vanilla javascript wrapper on top of the `@tsofist/rplidar` driver. You can find and download the code from my [RP Lidar GitHub Repo](https://github.com/gcornetta/RPLidar). Read carefully the documentation and the prerequisites before downloading it or cloning my repo. 

## Getting familiar with server-side JavaScript

## Robot car control software

## The mobile app

## Setting up the P2P network

## Assembling the chassis

## Putting all together

## Roadmap
Software:
1. improve the car fitness function.
2. improve the car genetic algorithm.
3. improve the `electron` user interface using UI framweworks such as [Photon](http://photonkit.com) or [Svelte](https://svelte.dev).
4. improve the mobile app user interface.
5. add more commands to the voice interface.
6. improve simulator graphics using `three.js`
7. add a Lidar user interface

3D Printing:
1. improve the chassis.
2. create a 3D printing video tutorial using [Shapr 3D](https://www.shapr3d.com).

Teaching:
1. Create video tutorials.
2. Create course handouts.
