NOVUS SPARTIAT
====

This repository provides information pertaining to the robot NOVUS SPARTIAT, a self-driving car designed and programmed by the team Novus Spartans, made for the Philippine Robotics Olympiad 2024 – Future Engineers Category. 

## Content

* `Team Photos` contains 2 photos of the team (an official one and one funny photo with all team members)
* `Vehicle Photos` contains 6 photos of the vehicle (from every side, from top and bottom)
* `Video Performance` contains the video.md file with the link to a video where driving demonstration exists
* `schemes` contains one or several schematic diagrams in form of JPEG, PNG or PDF of the electromechanical components illustrating all the elements (electronic components and motors) used in the vehicle and how they connect to each other.
* `src` contains code of control software for all components which were programmed to participate in the competition
* `models` is for the files for models used by 3D printers, laser cutting machines and CNC machines to produce the vehicle elements. If there is nothing to add to this location, the directory can be removed.
* `other` is for other files which can be used to understand how to prepare the vehicle for the competition. It may include documentation how to connect to a SBC/SBM and upload files there, datasets, hardware specifications, communication protocols descriptions etc. If there is nothing to add to this location, the directory can be removed.

## 1. Mobility Management

Motor selection is a crucial part of building the robot since its maneuverability highly depends on it. LEGO® Education SPIKE™ Prime Set has two (2) available motors: Medium Angluar Motor and Large Angular Motor, which can be referenced as Medium Motor and Large Motor respectively. These motors have a lot in common performance-wise and only differ in speed and torque. Based on tests performed with a provision of 7.2V power supply, here are the results: 

    Medium Motor                    Large Motor
     Speed: 135 RPM to 185 RPM       Speed: 135 RPM to 175 RPM
     Torque: 3.5 Ncm to 18 Ncm       Torque: 8 Ncm to 25 Ncm

    RPM – rotations per minute, Ncm – newton centimeter

The Medium Motor was shown to be negligibly faster than the Large Motor. However, the Large Motor was able to provide a substantial amount of power compared to its counterpart. With these pieces of  information, the team had chosen to use the Large Motor for both driving and steering management. The robot uses three (3) Large Motors, one each for driving and steering, while the other one will be discussed in the last part of Sense Management.

The robot is propelled by a rear-wheel drive transmission, where power from the rear motor drives the rear wheels, propelling the robot forward or backward. The large motors in the front are centralized on focusing for steering the entire robot, allowing for a range of motion from 90 degrees to -90 degrees. This transmission setup was chosen by the team because it is commonly used in the Future Engineers Category. Additionally, it is found that RWD (rear-wheel drive) systems offer better handling compared to the front-wheel drives, which were tested by the team.

## 2. Sense Management

Self-driving cars are highly dependent on their sensors in order to drive autonomously. That is why the robot consists of different sensors to properly execute its movements with regards to its position on the game field and obstacles surrounding it. Here are the components of the robot related to its sense management:

### 2.1.   SPIKE™ Color Sensor 
The SPIKE™ Color Sensor has the capacity to measure color RGB/HSV, reflection intensity, and ambient intensity. It has a sample rate of 100 Hz and an optimal reading distance of 16 mm. It has three (3) LEDs that can be turned on and off individually at different power levels, making it a possible light output. The team selected this color sensor due to its excellent performance in color detection, far better than the other color sensors the team have.

This color sensor is positioned on the front of the robot where it is facing downwards the game field. It is primarily used to read the colored lines on the game field, thus determining the driving direction of the robot. If it has detected the orange line first, the robot would know that the driving direction is clockwise, else if the first detected line was blue, the driving direction is counterclockwise. Additionally, the robot is able to know its position on some parts of the field that have a clear line to be read by the color sensor.

### 2.2.   SPIKE™ Distance Sensor
The SPIKE™ Distance Sensor has the ability to measure the distance to a surface in front of it with the use of ultrasonic technology. It has a sample rate of 100 Hz and a distance sensing range of 5 cm to 200 cm +/- 2 cm. It has an entrance angle of +/- 35° and has four (4) LEDs that can be turned on and off individually at different power levels, making it a possible light output. It sends inaudible high frequency sound waves from one “eye” while the other “eye” will measure how long it takes the sound waves to reflect through it.

This distance sensor is placed on the front of the robot, which is used to determine the position of the robot in respect to the wall in front of the sensor. This allows the robot to navigate safely within the game field, continuously checking if the robot is near the outer boundary wall in Open Challenge Rounds since the robot may not touch the said wall. In addition to that, it is also used to identify the position of the randomly placed parking boundaries and check if there is an obstacle in front of the robot in Obstacle Challenge Rounds.

### 2.3.   SPIKE™ Gyro Sensor
The built-in SPIKE™ Gyro Sensor can keep track of the angle the hub is currently facing. It consists of a three-axis accelerometer and three-axis gyroscope. The gyroscope part records the change of rotation of the hub and measures the total angle of rotation in degrees, enabling it to return the hub’s exact rotation angle around a given axis. Combined with the accelerometer, it allows the hub to determine its orientation and acceleration along a given axis. 

The robot relies on this gyro sensor for most of its movements, facilitating its accurate navigation across the whole game field. It enables the robot to follow a specific angle when moving, thus making it drive straight and turn into a particular angle efficiently.

### 2.4.   AISTEAM Roof Vision Module
The AISTEAM Roof Vision Module is capable of utilizing artificial intelligence (AI) algorithms to analyze and interpret visual data from the camera. It has a working voltage of 5V and a viewing angle of 72°. Additionally, it can achieve a maximum resolution of 320x240 pixels and supports a maximum code rate of 30 mbps. Its structure supports height and pitch angle adjustment, allowing it to face in different ways; and its shell is somewhat compatible with the LEGO construction system. It can perform various tasks such as tracking of multiple color blocks (up to 4 simultaneously), and processing of visual custom data.Due to this, it offers a broad range of AI vision applications, including LAB threshold debugging, template matching, visual line inspection, and visual range operations. It has the capability to identify and locate specific objects within an image and measure their exact position. 

The team chose this camera to specifically detect traffic signs and their color in Obstacle Challenge Rounds. This allows the robot to keep itself to the right side of the track  if a red pillar is detected and to the left side of the track if it is a green pillar. In addition to that, this camera is also used to detect the parking lot boundaries, making sure that the robot must not touch these randomly placed parking lot limitations. 

### 2.5.   Additional Information
Both the SPIKE™ Distance Sensor and AISTEAM Roof Vision Module are mounted to a SPIKE™ Large Motor. This enables these two sensors to rotate from a range of angle of 0° to 180°, covering a wide part of the surrounding area of the robot. The team has done this since the limited ports of the SPIKE™ Large Hub cannot provide more room for sensors around the robot. This motor serves as a helpful tool in the detection of the walls, obstacles, and overall surroundings of the robot while it is in the game field.

Another SPIKE™ Color Sensor is placed inside the shell of the robot. It is used to transfer and evaluate all of the essential data from the camera to the primary controller of the robot. It is mostly used in Obstacle Challenge Rounds, to detect the obstacles and the parking lot boundaries within the field.

## 3. Power Management

### 3.1.   SPIKE™ Large Hub
The SPIKE™ Large Hub is the programmable control unit for the LEGO® sensors and motors. It serves as the location for the robot's main program and is integrated with MicroPython as the operating system. The hub features six LPF2 input/output ports and a built-in six-axis gyro sensor, which includes a three-axis accelerometer and three-axis gyroscope. Additionally, it has a built-in speaker with a maximum sound quality of 12-bit 16 KHz and can connect to devices via Bluetooth or USB Cable. The team selected this hub as the primary controller for the robot due to its comprehensive capabilities, having six (6) ports for SPIKE™ excellent motors and sensors.

### 3.2.   SPIKE™ Large Hub Rechargeable Battery
The SPIKE™ Large Hub Rechargeable Battery is a lithium-ion polymer battery designed to power the Technic Large Hub, which in turn powers all Spike motors and sensors. It can be charged inside the Hub using a micro-USB cable and can be removed easily. With a capacity of 2100 mAh and an output of 7.3V, this battery has a lifetime of over 500 cycles, meaning it can handle more than 500 charge-discharge cycles throughout its lifespan.

### 3.3.   AISTEAM Controller
This controller functions as the robot’s sub-controller and is not designed to control the robot’s movements. It receives power from a separate power source, which will be introduced later. The controller is equipped with 17 expansion interfaces and has a main frequency of 72 MHz with its shell compatible with the LEGO build system. It features an on/off button used to run the program and start the camera to do specific actions. This is where the vision and the battery module are connected, and where the program is saved.

### 3.4.   AISTEAM Lithium Battery Module
This battery serves as the power source for the AISTEAM Controller and Vision module. It has an output voltage of 7.4V, a rated capacity of 1100 mAh, maximum discharge rate of 3C, a rated charging voltage of 8.4V, and a rated charging current of 1A. The shell of this battery is compatible with the LEGO building system. Both the input and output ports of this battery are DC, and it can be charged using a dedicated 8.4V 1A charger. The following battery is directly connected to the controller of the robot.

## 4. Additional Components

### 4.1.   AISTEAM Expansion Screen Module
The AISTEAM Expansion Screen Module has the ability to display alphanumeric characters and basic geometric figures such as rectangles and circles. It features a 0.96-inch low-powered OLED module with a resolution of 128x64, a full-view display, and SPI communication. The shell is equipped with a high-transmitting acrylic protection board. This screen module is directly connected to the AISTEAM controller of the robot. This component is specifically used to monitor the pixel number received by the AISTEAM Vision Sensor and is displayed in the screen module. This facilitates easier debugging of unexpected issues encountered by the camera, thereby saving time for the team.

### 4.2.   AISTEAM Full-Color Light Module

The AISTEAM Full-Color Light Module can produce light within a wide range of colors. It has a working voltage of 5V, color range of RGB 0 to 255, and a light-emitting angle of 120°. The shell of this module is compatible with the LEGO building system. This component is used to output the color of the obstacles detected by the camera, making it easier to find errors in the program and debug for the team.

## 5. Obstacle Management
In order to detect the position and negotiate with the color of the obstacles, a specific strategy must be well-planned to possibly finish three (3) laps in Obstacle Challenge Rounds. The team had spent a fair amount of time considering different thoughts and ideas to efficiently manage the obstacles on the game field; always giving space for new yet excellent ideas to be added in the team’s strategy.

The main strategy for the robot involves two (2) major ideas: first is giving the camera and the distance sensor the ability to rotate with the use of a SPIKE™ Large Motor, which wil be referenced as “vision motor” in this documentary. The vision motor can rotate the camera for approximately 90° in both directions starting from the middle. The rotation of the vision motor depends on the position of the robot and the color of the detected obstacles.

The second major idea is programming the robot to follow three (3) possible routes based on the color of the obstacles, the position of the parking lot boundaries, and the defined driving direction of the round. Example: the driving direction is set to be clockwise; refer to the illustration below. If the detected obstacle is GREEN, the robot would follow the green arrow, near the outer wall. If the obstacle is RED, the robot would follow the red arrow, near the inner wall. Lastly, if the robot detected a GREEN obstacle, and the parking lot boundaries are located on that same section, the robot would follow the gray arrow, somewhat in between the outer and inner walls. 

<img src = "https://github.com/user-attachments/assets/22d1a235-6b41-4305-a00a-393fe992f5bb">
