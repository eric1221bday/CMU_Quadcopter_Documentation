# CMU Quadcopter System Overview

## Hardware

* Tarot Ironman 650 Frame
* Sunnysky Brushless Motor x 4
* HobbyKing ESC x 4
* Pixhawk Flight Controller
* RPLidar A2
* 11x47 Propellers x 4
* Odroid XU4
* Teraranger One

## Software

* PX4 Flight Stack
* ROS Kinetic
* Ubuntu 16.04
* MAVROS
* Cartographer

![Quad!](https://github.com/eric1221bday/CMU_Quadcopter_Documentation/raw/master/img/A0223.jpg)

## System Diagram

![System!](https://github.com/eric1221bday/CMU_Quadcopter_Documentation/raw/master/img/quad_system_top_level.png)

### Breakdown

#### Teraranger One

![Range!](http://www.teraranger.com/wp-content/uploads/2014/03/TeraRanger-One-close-side-view.jpg)  
[Product Page](http://www.teraranger.com/products/teraranger-one/)  
Accurate and fast distance sensor, uses IR time of flight to capture distance.

#### RPLidar A2

![Laser!](http://www.robotshop.com/media/files/images3/rplidar-a2-1.png)  
[Product Page](http://www.robotshop.com/en/rplidar-a2-360-laser-scanner.html)  
Cheap and effective LIDAR

#### Odroid XU4

#### Pixhawk

## Operating Procedure

1. Power on System by plugging in LIPO
2. Check Odroid power up by status LED (blue light flashing)
3. Disable safety by pressing the red safety button until LED turns from flashing to solid red
4. Open Terminal or Terminal Emulator and SSH into Odroid via following

```bash
# NOTE: Both Odroid and client must be on CMU or CMU-SECURE network
ssh odroid@efang_odroid.wv.cc.cmu.edu
# Password if prompted is: odroid
```

5. Once SSH session started, source workspace

```bash
cd sandbox/quadcopter
source devel/setup.bash
```

6. Repeat steps 3 & 4 for a new terminal window, else use TMUX to open a new window (guide [here](http://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/))
7. In one terminal, start MAVROS and preparatory ROS nodes

```bash
roslaunch hallway_navigator cartographer_mavros.launch
```

8. In the other terminal, start cartographer and associated ROS nodes

```bash
roslaunch hallway_navigator cartographer_slam.launch
```

9. Arm the drone and perform liftoff in MANUAL mode
10. switch to POSITION mode