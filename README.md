# Recycling Sorting System

McMaster ENGINEER 1P13, Jan 2022 – Mar 2022.

Sensor equipped robot that identifies waste by material type and autonomously sorts it into designated bins along a fixed track.

`Python` `Autodesk Inventor` `3D Printing` `Quanser Interactive Labs` `Robotics`

<p align="center">
<img src="Media/Pictures/Full_Physical_Design_with_Hopper.jpg" alt="Physical design" width="550"><br>
<em>Hopper Mechanism Mounted to the Quanser Q-bot, Shown Beside Containers Representing the Waste It Sorts.</em>
</p>

---

## Table of Contents
- [Overview](#overview)
- [Hardware & Software](#hardware--software)
- [System Workflow](#system-workflow)
- [How It Works](#how-it-works)
  - [1. Material Detection](#1-material-detection)
  - [2. Loading](#2-loading)
  - [3. Navigation & Positioning](#3-navigation--positioning)
  - [4. Hopper Tipping Mechanism](#4-hopper-tipping-mechanism)
- [CAD & Physical Mechanism](#cad--physical-mechanism)
- [Results](#results)
- [Full Report](#full-report)

---

## Overview

This project addresses Canada's low recycling rate, where sensor limitations in identifying material type and contamination make large scale sorting difficult, resulting in most plastic waste ending up in landfills. The finished system is a small scale robot that identifies waste dispensed onto a rotary table, loads it onto a hopper, navigates a fixed track, and deposits it into the correct designated bin. Main components include a Quanser Q-bot equipped with ultraviolet, IR, colour, and LDR sensors, a Quanser Q-arm robotic arm, a linear actuator driven hopper mechanism, and a Python program built in Quanser Interactive Labs.

---

## Hardware & Software

### Hardware

| Component | Purpose |
|---|---|
| Quanser Q-bot | Mobile robot base that carries the hopper, follows the fixed track, and positions itself in front of each bin |
| Quanser Q-arm | Robotic arm that loads dispensed containers from the rotary table onto the hopper |
| Ultraviolet Sensor | Assists in identifying material type of each dispensed container |
| IR (Infrared) Sensor | Keeps the robot following its fixed line track |
| Colour Sensor | Detects the colour of each container to help classify material type |
| LDR (Light Dependent Resistor) Sensor | Detects light levels to assist material identification |
| Ultrasonic Sensor | Measures distance to position the robot accurately in front of each bin before disposal |
| Linear Actuator | Drives the hopper tipping mechanism to release waste into the correct bin |
| Rod, Slider, and Pins | Connect the linear actuator to the hopper's baseplate, converting linear actuation into hopper rotation |
| Rotary Table | Dispenses waste containers at random for the robot to identify and load |

### Software

| Tool / Library | Purpose |
|---|---|
| Quanser Interactive Labs (Q-Labs) | Virtual environment simulating the Q-bot, Q-arm, sensors, and recycling facility layout |
| Python | Program controlling detection, loading, navigation, dumping, and return to home position |
| Autodesk Inventor | CAD modelling of the hopper tipping mechanism and its individual components |

---

## System Workflow

| Stage | Component | Output |
|---|---|---|
| Dispensing | Rotary table | Container placed at random with an assigned material id and weight |
| Detection | Quanser Q-bot sensors | Material type identified for each container |
| Loading | Quanser Q-arm | Up to 3 containers loaded onto the hopper, combined weight capped at 90 grams |
| Navigation | IR sensor, fixed line track | Robot follows the track toward the identified bin |
| Positioning | Ultrasonic sensor | Robot stopped at the correct distance from the bin |
| Dumping | Linear actuator, hopper mechanism | Hopper rotates and releases containers into the bin |
| Return | Python program | Robot navigates back to its home position to begin the next cycle |

---

## How It Works

### 1. Material Detection

- Containers are dispensed at random onto the rotary table, each assigned a material id used by the program to determine the correct bin.
- The ultraviolet, colour, and LDR (light dependent resistor) sensors work together to identify the material type of each container before it is loaded.
- The program compares each new container's material id against the previous one to decide whether it can be grouped with containers already loaded on the hopper.

### 2. Loading

- The Quanser Q-arm loads up to three containers from the rotary table onto the hopper per cycle.
- Containers are only added to the same load if their combined weight stays at or below 90 grams.
- If a container's destination bin differs from what is already loaded, or the weight limit would be exceeded, the current load is dumped before the new container is picked up.

### 3. Navigation & Positioning

- An onboard IR (infrared) sensor keeps the Q-bot following its fixed line track by adjusting left and right wheel speeds whenever the sensors lose the line.
- Bin locations are defined using coordinate values within the Quanser Interactive Labs environment, which the program references to navigate the robot toward the correct bin.
- Once close to the target, an ultrasonic sensor measures distance and stops the robot at the correct position in front of the bin before dumping.

### 4. Hopper Tipping Mechanism

- The hopper mechanism is built around a linear actuator, with a rod connecting the actuator to the hopper's baseplate.
- As the actuator extends, the rod pushes against the baseplate, rotating the hopper and releasing its contents into the bin below.
- Pins secure both ends of the rod, with small cylindrical securing pieces holding each pin in place to keep the mechanism stable during operation.
- After dumping, the actuator retracts, resetting the hopper to its closed position before the robot returns home.

<p align="center">
<video src="Media/Videos/Hopper_Mechanism_Demonstration.mp4" controls width="500"></video><br>
<em>Demonstration of the Hopper Mechanism Extending and Tipping to Release Its Contents. No Containers Were Loaded During This Test, but the Motion Confirms the Hopper Tips Far Enough to Fully Empty Its Contents.</em>
</p>

---

## CAD & Physical Mechanism

The hopper mechanism and its components, including the rod, slider, and pins, were modelled in Autodesk Inventor before fabrication and 3D printing.

<p align="center">
  <img src="Media/Pictures/CAD_Home_View.jpg" width="300">
  <img src="Media/Pictures/CAD_Left_Right_View.jpg" width="300">
</p>
<p align="center"><em>CAD Model of the Hopper Mechanism From the Home View (Left) and Side View Showing the Actuated Rotation (Right).</em></p>

<p align="center">
  <img src="Media/Pictures/Rod.jpg" width="300">
  <img src="Media/Pictures/Slider.jpg" width="300">
</p>
<p align="center"><em>CAD Model of the Rod (Left) and Slider (Right) Components of the Hopper Mechanism.</em></p>

<p align="center">
  <img src="Media/Pictures/Pin_Securing_Piece.jpg" width="300">
  <img src="Media/Pictures/Cylindrical_Pin.jpg" width="300">
</p>
<p align="center"><em>CAD Model of the Pin Securing Piece (Left) and Cylindrical Pin (Right) That Hold the Rod in Place.</em></p>

<p align="center">
  <img src="Media/Pictures/Physical_Mechanism.jpg" width="300">
  <img src="Media/Pictures/Physical_Mechanism_Close_Up.jpg" width="300">
</p>
<p align="center"><em>3D Printed Hopper Mechanism Mounted to the Quanser Q-bot (Left), and a Close Up View of the Rod and Pin Assembly (Right).</em></p>

---

## Results

- The system functioned as a fully automated small scale sorting robot, correctly identifying waste by material type before directing it to the appropriate bin.
- The Quanser Q-arm and hopper mechanism successfully loaded, transported, and released waste into its designated bin within the enforced 90 gram weight limit.
- The project illustrated a viable small scale model for automated sorting, supporting the broader goal of increasing recycling efficiency at facilities limited by manual sorting capacity.

---

## Full Report

[Read the Full Project Report](Files/Recycling_Sorting_System_Report.pdf)
