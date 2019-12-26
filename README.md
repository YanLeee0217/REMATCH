# REMATCH <a name="rematch"></a>
A 3.007-Introduction to Design Project featuring Pong game with pulling ropes# 3.007 F05 DESIGN TEAM 7

Authors:
 - Kevin Ma Yuchen
 - Lui Yan Le 
 - Hazel Xing Yunqing
 - Princeton Poh Jin Heng 
 - Jordan Chan 

## Table of Contents <a name="table-of-contents"></a>
- [REMATCH](#rematch)
    - [Table of Contents](#table-of-contents)
    - [Repo Content](#repo-content)
    - [Introduction](#introduction)
        - [Poster](#poster)
        - [Video](#video)
    - [How to use](#how-to-use)
    - [Components](#components)
        - [System Diagram](#system-diagram)
        - [Electronics](#electronics)
        - [Mechanical](#mechanical)
        - [Software](#software)
    - [Trouble Shooting & FAQ](trouble-shooting-&-faq)
    - [Future improvements](#future-improvements)

## Repo Content <a name="repo-content"></a>
- `ball.py`: ball class in pygame
- `paddle.py`: paddle class in pygame
- `main.py`: The main game script. You can run it both on a normal computer or the arcade console we made
- `i2c_encoder`: Arduino code for encoders using i2c
- `past_codes`: Things that we have have tried before but are no longer used

## Introduction <a name="introduction"></a>
REMATCH is a 3.007-Introduction to Design Project by Cohort 5 Team 7 of SUTD Class of 2022. It is a arcade game console that enables people to play the classic game Pong with the motion of pulling ropes.



### Design Conception <a name="Design Conception"></a>

The theme of 2019's 3.007 Intro to Design was "Play 2.0" - to design experiences that were sparked by the act of playing, 

| REMATCH                                                      |
| ------------------------------------------------------------ |
| “Stay Up Till Dawn” is SUTD life in a nutshell. Students actively participate in numerous projects in addition to the rigorous curriculum. Still, they are expected to maintain focus throughout long lessons and project meetings. <br/><br/>We wanted a way to break the monotony, to recharge the mind and regain focus between lessons. Our idea is an adaptation of a typical gym equipment, mapping its physical movements to popular games. Sharing a laugh with your friends as you play the game; doing some exercise to get the blood flowing are some of the best ways to get you through the tough days. Refresh. Refocus. Recharge. REMATCH. |

The team developed REMATCH, an interactive installation that combines classical arcade games such as pong, with physical exertion through a rope pulley. With the intension to be placed in classrooms, it would serve as an effective game that would allow students to recharge. 
The product included several design considerations, a few of which are listed below:

- Social aspect of a game machine
  - Consideration were made to allow the play to be a full social experience with a crowd surrounding players
- Competitiveness of games
- Short gestation period - Games of <5min
- Accessibility to a wide range of fitness levels 
  - Tension in pulley system is configurable.
  - Accommodates both male and female players



### Poster <a name="poster"></a>
find the poster in `assets`
### Video <a name="video"></a>
https://youtu.be/wE_V6qiuwjU

## How to use <a name="how-to-use"></a>
1. Clone this repository to the computer/RPi
2. In the terminal, run`$ pip3 install pygame`
3. Make sure all the connections are stable if you are using an RPi
4. Check your i2c connection by the command `$ i2cdetect -y 1`, You should be able to see 04 and 05 appear in the second line among a lot of dashes
5. Go to the root directory of this repository, and run `$ python3 main.py`
6. Quite the game by closing the window or pressing "x" on your keyboard

## Components <a name="components"></a>

### System Diagram <a name="system-diagram"></a>
to be updated

### Electronics <a name="electronics"></a>

#### Raspberry Pi 4B

- To set up an RPi 4, follow this tutorial: https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up 
  note that when preparing your sd card, download the version that supports **offline installation** as you might not be able to connect to school wifi when installing.


- To connect to school wifi (PEAP-Enterprise) or school ethernet (IEEE 802.1X), follow this tutorial compiled by **Kevinskwk**:
https://github.com/Kevinskwk/Misc/blob/master/RaspberryPi/RPi4_Wifi_Configuration.md 

#### Encoders
- Due to limited budget, we used ir sensor modules as encoders. there are 12 sectors in black and white on the pulley. The two ir sensors are placed at an angle of 165 degrees, creating a 90 degree phase difference of the ir sensors' signals. With the phase difference, the encoders can detect the direction of rotation, and the precition is doubled.
- The STL file can be found in the `assets` folder.

#### Arduino Nano
- We used one Arduino Nano for each encoder, two in total.
- The encoders are connected to digital pins 2 and 3 that support the function `attachInterrupt()`
- The Arduinos are connected to the RPi via i2c. The code for the Arduinos can be found in the folder `i2c_encoder`

### Mechanical <a name="mechanical"></a>
Mechanical design consisted 3 main components - frame base, rope pulley system, UX components





#### Frame base

The frame was modified from a home pullup bar rack bought off Carousell (S$40). Constructed out of steel square tubing, with adjustable height. This provided a sturdy base in which to construct our mechanism (rope pulley)

#### Rope Pulley

The key to the product was a rope pulley system - which was a medium for user input that incorporated physical exertion. We were inspired by ropes used in gyms, specifically battle ropes and rope machines 

![img](https://video-images.vice.com/articles/5a467ddd3037102f25c4b02e/lede/1514572181564-Screen-Shot-2017-06-15-at-31634-PM-1-696x652.png?crop=1xw:0.6004601226993865xh;center,center&resize=300:*)

<img src="https://www.americanfitness.net/images/products/detail/oryxropeclimber.jpg" alt="img" style="zoom:25%;" />



Hence the design considerations were namely:

- Continuous loop for the rope, such that the pulley can be wound infinitely
- Variable tension - both for ease of installation and for different groups of users
- Sufficiently high resistance - to provide the physical exertion



Recalling the basic concept of a 2 pulley system - one can increase the resistance on the pulley (Force Applied) in 2 ways. Namely, 

1. Static friction applied onto the pulley wheels
2. Rotational Inertia (or similar)

Our product uses [1. Static Friction] to increase resistance. Based on initial testing, we set a target tension force applied onto the rope at 4.0kg.

In addition, the following engineering considerations would also be key

1. Elasticity of rope
2. Size of pulley wheel (contact surface area)
3. Distance between 2 pulley wheels



![img](final pulley system)

The rope pulley system is a simple 2 pulley system that uses static friction to generate the resistance. This is done by increasing the distance between the 2 pulleys and generating tension within the rope. 

- The top pulley wheel is fixed, acting as a convinient place to install our sensors
  - Overall internal diameter of XXXXmm
- The bottom pulley varies in height, which allows us to vary the tension
  - This is accomplished by installing the pulley on a set of M8 threaded rods (cut to length)
  - Held in by wing nuts to facilitate easy variation of height/tension
  - ![img](diagram pulley system)
- The rope was a 1" diameter marine polyester rope
  - Large size to ensure sufficient contact area with pulley



  





### Software <a name="software"></a>

#### Prerequisites
- Make sure you have `Pygame` installed
- On RPi, make sure you have the libraries `smbus` and `RPi`. Then make sure the buttons and LEDs connected properly. Make sure the i2c connection from the Arduinos to the RPi is stable.

#### Pygame
- The game is writen in Python, using Pygame library.
- The files `ball.py` and `paddle.py` contain the ball and paddle classes respectively
- The main game programme is in `main.py`. You can run it on our arcade console with encoders and buttons to achieve best experience. Alternatively, you can directly run it on any computer with the prerequesites installed. Do run from the terminal in the direction of this repo to avoid any error.

## Trouble Shooting & FAQ <a name="trouble-shooting-&-faq"></a>
to be updated

## Future improvements <a name="future-improvements"></a>
- Change into proper encoders
- Make a physical Pong game without a monitor (if we have money and time!)
- MORE LEDS