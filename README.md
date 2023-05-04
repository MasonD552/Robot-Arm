# Robot Arm
This repository will actually serve as a aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts)


## Table of Contents
* [Baseball_Throwing_Robot](#Baseball_Throwing_Robot)


---

## Baseball_Throwing_Robot
### What is this Project? 
Build a robot arm that can do a task.

### Requirements For Project 
-Your robot arm can pick something up or hold something, and move it around.  This is very general, and should be made more specific, based on the particular problem that you're attempting to solve.

-Your robot arm's motion should have 3-6 servos Micro or standard. 

-This robot arm is controlled with Arduino or CircuitPython, your choice.  The controller should run off either power coming from USB or a rechargeable 9V battery or battery pack.

-Like all of your prior projects, there should be an easy way to switch off the power, an easy way to change batteries, and some obvious indication when power is on.

-Knock out your design in CAD before you start constructing anything.  Use SolidWorks to do a motion and/or stress analysis of your robot arm or some part of the arm. 

### Project planning doccument:
Source for Project Planning:
https://docs.google.com/document/d/15Tew-MtXxxcetKLdX3Wt4Nufw6axhEezAe_4fcUIpyI/edit#heading=h.ukbi0a75zb46 

### Our goal/ Vision:
What we wanted to do as a team is create a solution to our problem. Our problem being how can we get extra practice when we dont have other people who want to come out and get extra practice. Our solition: create a robot arm that can be used as a multi-purpouse tool and can be there when the person is not.This is why we chose to make a robot arm that can throw baseballs and give you infeild repetitions when you need. Making this will eliminate the need for another person to be there and will help give you the perfect reps every time.

### Onshape documents 
![image](https://user-images.githubusercontent.com/113116205/228252030-547f0788-dd24-46d4-897a-e9394a541afd.png)
This is what we based our whole project off of it is called a jai alai scooper it holds the ball and throwis it at almost 90 degree angle and can whip the ball out of the jai alai pretty fast and was very essential in our project.

- this is a video of what the jai ali is actually capable of: https://www.youtube.com/watch?v=wk4-fuGAwjY
- here is another video:


https://user-images.githubusercontent.com/91158978/228271775-c3338992-b1db-4201-a7a4-3339b8b70e48.mp4
- here is another video of robot engineers in Philly who created a robot that through the first pitch

https://user-images.githubusercontent.com/91158978/228272692-2c9db49b-105a-4e4e-b5eb-860517c765e6.mp4







![image](https://user-images.githubusercontent.com/113116205/228253333-abcd3984-5490-450f-a9f3-8cc0a87c59f8.png)
![image](https://user-images.githubusercontent.com/113116205/228253504-3adfd3d6-4590-47cb-87a2-462effc2bb48.png)

- This is what we called our connector peice its used to conect the jai alai to the actual metal peice so we can throw the ball. How it works is we put the jai alai threw the open hole (friction fitted) and then screw in a peice that is connected to the botton to an L shaped base peice.

![image](https://user-images.githubusercontent.com/113116205/228255034-a1f2eb2d-ef10-4b09-9f2b-514ce2137940.png)

- This is on of the variations we used to build our desighns we knew we were going to lift it into the air and they had to be strapped to a platform so we used these( called l shape screw holders) to change the level because we lifted it of of the ground and then pushed them against the elevated surface and screwed them to the platform so it is stable.

![image](https://user-images.githubusercontent.com/113116205/228258049-55a11193-5c70-4fb2-8930-6919004440f8.png)
![image](https://user-images.githubusercontent.com/113116205/228258162-3137ef31-c18f-4a48-8ee1-6aedd0001f3f.png)
![image](https://user-images.githubusercontent.com/113116205/228258294-2da5d978-8b1b-469a-9ef8-278d7af61137.png)
![image](https://user-images.githubusercontent.com/113116205/228258455-16e856e2-5c4f-42de-82e5-58dae5b6e186.png)
![image](https://user-images.githubusercontent.com/113116205/228258660-affc144c-b90f-4056-8be8-3a65e897cd77.png)
![image](https://user-images.githubusercontent.com/113116205/228258746-dd44368d-8829-4be7-8636-70b526c16bc0.png)

- These are pictures of our final onshape doccument assembly with the walls and the arm being able to be able to turn 360 degrees.We change stuff to use less material in our actuall one but this is the final onshape doccument. 

### Onshape Doccument 
- https://cvilleschools.onshape.com/documents/356c56ca499f7db8076fcbc8/w/f6d4ab2399876fcf0f8c09f6/e/9266c3aeabd5a4af2e413943

### Photos Of Final Project
![IMG-2209](https://user-images.githubusercontent.com/91158978/228259502-d665096a-e785-485d-af83-426343239fdc.jpg)
![image_50445057](https://user-images.githubusercontent.com/91158978/228259522-ee10264c-3d3c-477f-a468-ec29ad1d4b8e.JPG)
![image_50403329](https://user-images.githubusercontent.com/91158978/228259537-6af1d40e-7f32-4f0e-8347-183dfa58d45a.JPG)

### Commented Code
```python
# Import necessary libraries
import time
from time import sleep
import board
from digitalio import DigitalInOut, Direction, Pull
from pwmio import PWMOut
from adafruit_motor import motor as Motor

# Set up DRV6612 motor driver inputs and outputs
drv6612_ain1 = PWMOut(board.D5, frequency=50)
drv6612_ain2 = PWMOut(board.D4, frequency=50)
drv6612_sleep = DigitalInOut(board.D0)

# Set up button and switch inputs
button_a = DigitalInOut(board.D13)
button_a.direction = Direction.INPUT
button_a.pull = Pull.DOWN
switch = DigitalInOut(board.D10)
switch.direction = Direction.INPUT
switch.pull = Pull.UP

# Set up motor using DRV6612 inputs
motor_a = Motor.DCMotor(drv6612_ain1, drv6612_ain2)
timeStop = 0.0
currentTime = time.monotonic()

# Define function to print motor status


def print_motor_status(motor):


if (motor == motor_a):
motor_name = "A"
else:
motor_name = "Unknown"
print(f"Motor {motor_name} throttle is set to {motor.throttle}.")

# Main loop
drv6612_sleep.direction = Direction.OUTPUT
drv6612_sleep.value = True  # enable (turn on) the motor driver
while True:
    # If button and switch are both pressed
if (button_a.value == 1 & switch.value == 1):
    # Drive forward at full throttle for 5 seconds
motor_a.throttle = 1.0
timeStop = (time.monotonic() + 5)

# If switch is turned off
if (switch.value == 0):
    # Brake to a stop
    motor_a.throttle = None

# If timeStop has elapsed
if (timeStop < time.monotonic()):
    # Brake to a stop
    motor_a.throttle = None

# Print button and switch values, timeStop, current time, and motor throttle
print((button_a.value, switch.value, timeStop, time.monotonic(), motor_a.throttle))

# Use conditional variables to determine which "state" you want to be in
# If button is hit
#  tStop  = current time + 5s
#  goStop = 1
#
# If switch.val == 0
#   goStop = 0
#
# If tStop < current time
#   goStop = 0
#
# If goStop = 1
#   motor throttle = 1
# Else
#   motor throttle = 0
```
# Videos from Project

https://user-images.githubusercontent.com/91158978/228269459-0703f06c-6a79-47bb-87a3-f3d1d6f57633.mp4


https://user-images.githubusercontent.com/91158978/228269484-28800e23-5790-4bf4-9498-d971a8ff5251.mp4



https://user-images.githubusercontent.com/91158978/228269600-a4db18a1-2ca0-43e0-84d3-42527a54ff74.MOV



https://user-images.githubusercontent.com/91158978/228269615-9e9cc8d4-0779-400c-96f6-061e618b7958.MOV



### Reflection
This project taught us a lot about robotics and problem-solving. We had to come up with a solution for the problem of not having enough people to practice with, and we decided to create a robot arm that could throw baseballs and give infield repetitions. We learned how to design and build a robot arm that could move and pick up objects with the help of servos and an Arduino controller. The CAD design was especially useful in creating a motion and stress analysis of the robot arm.

One of the most challenging parts of the project was getting the arm to move in the right way to throw the baseballs accurately. We had to experiment with different designs and angles to get the throwing motion just right. We also had to figure out how to make the arm stable and secure, so it wouldn't wobble or move while throwing the ball. Another challenge was making sure the controller was working correctly and that we could easily switch off the power or change batteries.

Our main goal was to create a multi-purpose tool that could help people get extra practice without needing another person there. We wanted to eliminate the need for someone to throw the ball and give people the perfect reps every time. The jai alai scooper was a crucial component of our design, and we based the whole project on it. The connector piece was also essential in connecting the jai alai to the actual metal piece and throwing the ball accurately.

Overall, this project was a great learning experience, and we were able to develop new skills in robotics and problem-solving. It was a challenging but rewarding project, and we're proud of the final result.

