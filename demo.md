# Project Demo

Date, Time & Place
* 2018/12/6 15:05-18:20 (7-8 & 9-10)
* CS Faculty Meeting Room (W8E-10F)

## Program

1. Pong Game (team: "\>\<script\>alert(1);)
2. IoT Roast Beef (team: Suzuki)
3. Chat Bot Watch (team: narahara)
4. Remote DC Motor Monitoring and Controlling System (team: noob)
5. Ωt4𝑘𝜇0 𝑅𝑜𝑏𝑜 (team: IQ1)
6. “The Game” (team: “Team name”)
7. Simple M5 Stack Maze Game (team: 810)
8. M5 Pet (team: Nine)
9. Alarm clock prevent from despair awake (team: non-sugar-cocoa)
10. POS Defender (team: Kilimanjaro)

Each team has 15 minutes
* 2 min for setup
* 10 min for presentation and demo
* 3 min for Q&A

-----
## Pong Game

### Team: "\>\<script\>alert(1);
* Yamaguchi Kazuki
  - implement WiFi server and client
* Amatsu Takeru
  - implement WiFi server and use RTOS function
* Gotoh Tsukasa
  - implement Pong game

### Project Summary
We made the "Pong Game"[1]. Pong is one of the earliest arcade video games. It is a table tennis sports game featuring simple two-dimensional graphics. The player controls a paddle by moving it horizontally across the top or bottom of the screen. They can compete against another player controlling a second paddle on the opposing side. Players use the paddles to hit a ball left and right.
We use the three features of M5Stack environments: sensors, WiFi modules, and RTOS functions. 
First, the acceleration sensor in M5Stack tells us its slope. We use the slope for game input. For example, when you tilt the M5stack to the left and right, the paddle in the display also moves left and right.
Second, these M5stacks communicate with each other. They tell the ball and their paddle locations on display. The WiFi Library provides simple APIs for establishing a TCP connection so we can easily implement the communication protocol. This approach allows us to play the game at a distance.
Third, we use RTOS functions to combine these features. The xTaskCreate function creates a new task and adds it to the list of tasks that are ready to run. We make two tasks. One task reads the sensor's value and stores these value to the global variable. The other task communicates with the corresponding task in the other device. The xTimerCreate function creates a new software timer instance. The xTimerStart function the timer callback function invokes periodically. The periodic timer ensures the display redrawn at a constant rate. It is helpful to you for smooth playing. 

[1]: https://en.wikipedia.org/wiki/Pong

-----
## IoT Roast Beef

### Team: Suzuki
* Atsushi Suzuki
  - Project management and Hardware(Base for sensor and M5Stack)
* Kosei Noda
  - IoT system(Online visualizer via using wifi)
* Yuki Teduka
  - Temperature observation and send it via wireless
* Shumpei Tokuda
  - Reading image from camera module for online visualizer
* Haruto Yano
  - Hacking IH heater physically and controlling the temperature

### Project Summary

In our project, we will propose an IoT solution for low temperature cooking for roast beef. Low temperature cooking is a cooking method in which a lump of beef is put in hot water for some several hours. This method realizes well-heated and soft roast beef. The important points in low temperature cooking are the temperature and the time: it is said that 60 °C and almost 3 hours is good for roast beef.

This method makes it possible to produce tasty roast beef, but it is costly in terms of temperature management and cooking time. In order to solve this problem, we will construct IoT Roast Beef system which provides automatic control of temperature and online monitoring.

### Hardware
Our proposal system consists of an IH heater, an IH compatible pan, a base for sensor and M5Stack, two M5Stacks, a temperature sensor and a camera.

The IH heater is inexpensive one, we hacked the control circuit and made it possible to change the output directly from a M5Stack. It can also be used as a IH heater for general purposes. Base for sensor and M5Stack is made with aluminum and 3D-printed ABS.

### Software
This system consists of two part of software system: the control system part and the IoT system part. Both of the parts are processed with M5Stacks only.

Control system part maintains the temperature of water. This system is a networked control system that a M5Stack for temperature observation and a M5Stack for control are connected via wireless. The M5Stack for control is directly connected to the control circuit of IH heater and send filtered PWM signals to IH heater to change output of IH heater.

IoT system part provides the user with a monitoring environment. The measured temperature of water and pictures of the pot with beef taken from a camera attached to the base for sensor and M5Stack.

Each M5Stack is equipped with FreeRTOS and it makes it possible to easily perform accurate measurement and control in ms order using the vTaskDelayUntil function. Also, since multiple tasks with different sampling periods are combined, such as temperature measuring, control and taking picture by camera and uploading of monitoring results, multitasking function and communication function between tasks of FreeRTOS make it efficient to implement the system.

-----
## Chat Bot Watch

### Team: narahara
* Osamu Miyazawa

### Project Summary
A smartwatch which we can talk with chatbot by speech recognition, chatbot API, and speech synthesis.

-----
## Remote DC Motor Monitoring and Controlling System

### Team: noob

* LANG, Chen
  - Project Manager
  - Peripheral Hardware Designer
  - Motor Controller Software Developer
* ZHANG, Zhiyang
  - Remote Controller Software Developer
  - Testing
* GAO, Tianyang
  - Remote Controller Software Developer
  - Testing

### Project Summary

<img src="/images/noob.png" style="float: center; margin: 10px;" />

Our project is a DC motor controller with a remote monitoring and controlling functionalities. The DC motor is controlled by the M5Stack device named “Motor Controller”. All the system information, that are voltage, current and temperature, will be collected by “Motor Controller” and sent to the other M5Stack device named “Remote Controller”. The LCD of “Remote Controller” displays all the system information.

Also, “Motor Controller” is responsible for protecting the circuit. If the voltage, current or temperature is abnormal, the controller will cut off the main power supply by controlling the relay via pin G16.

So, there are mainly 3 periodic tasks in “Motor Controller”: communication task, monitoring task, and motor drive task. Since motor drive task needs to generate PWM wave, it has the shortest period and the highest priority. Monitoring task is responsible for protecting the circuit, so it has the second shortest period. Communication task is the least important, so it has the longest period and the lowest priority.

In addition, user can use button to send instructions via the “Remote Controller” to “Motor Controller” and then control the speed and the direction of the DC motor. Besides, these two M5Stack devices communicate via WIFI.

-----
## Ωt4𝑘𝜇0 𝑅𝑜𝑏𝑜

### Team: IQ1
* Yoshitaka Sakurai
  - develop communication between controller and robot
* Arimichi Matsumura
  - develop server
* Mizuho Katayama
  - create robot
* Ryoma Aoki
  - develop client

### Project Summary

* In this project, we develop control system for a biped robot which consists of 17
joints.
* We use three M5stacks. One of them is used to control the biped robot and to
display facial expression and the others are used as remote controllers.
* With clients controllers, we can choose the robot's action and send commands to
server via Wi-Fi UDP communication.
* We prepare multiple motions for biped robot. We send a motion request from
the controllers to the M5stack which is connected to the robot, and make the
robot operate the requested motion.
* For UI responsibility, two threads, the UI thread and the communication thread,
run independently using a Free-RTOS feature.
* The UI thread monitors inputs and fork the communication thread for sending
command.
* Sending command requests are blocked until previous action is completed.
* The M5Stack connected to the robot receives the messages from the controllers
and send commands to the robot.
* We can instruct the robot to perform actions such as bowing and waving hands,
and to change face picture displayed in the server device's LCD display.
*  When the server receives requests to perform actions,the server send commands to the robot, and then the robot invokes corresponding program which is installed in robots and when receives commands to change face, the server
renders corresponding picture in the LCD display.


-----
## “The Game”

### Team: “Team name”
* Aoukar Tarek
  - Software engineer (Web)
  - UI design
* Kyrylchuk Oleksii
  - Project manager
  - Software engineer (State machine, web requests)
* Wang Biyuan
  - Software engineer (State machine, Wi-Fi connection)
* Xu Ruopeng
  - Art director, Software engineer (Name generation)

### Project Summary

We have developed our version of the popular game “Tamagotchi”. In our version, you have your own pet Spiderman that you can care for by feeding it, playing with it or letting him go to sleep. Our device also shows the animation of eating, playing and sleeping. Moreover, the temperature of the environment affects your score as well. If it is too hot or too cold, your Spiderman will die quickly. It is a very high-stakes game, since if you are not careful enough your Spiderman might die! However, if you are mindful of your actions and you care for it properly, you can win the game by turning your Spiderman to a Spider-angel! When the game is over, you will get your own name and score, and the score will be updated on an online board. You can compete with your friend and see who is the master of Spiderman!

#### Technical achievements
* Designed and implemented a state machine for the game
  - Three activity events: Eating, sleeping and playing, which could be selected by
the users freely.
  - Two final states: Win and lose, which depends on when the activity scores or
total points hit the boundary of finishing.
  - Each state is affected by the user's input. State transition is triggered by the change of points.
* Used multithreading to update the score, show the animations and handle button presses simultaneously
  - Three threads were created corresponding to score update, activity event processing and the change of animation.
  - The updateScore thread firstly checks the current state, and then updates the total score.
  - The processEvent thread checks the button press, calculates the points for corresponding activity event and calls the animation update function.
  - The animateIdle thread checks whether the game state is satisfied the end condition or can be continued and calls the corresponding animation update
* Created pixel art Spiderman animations
  - Four different animation types: Eating, playing, sleeping and dead. Each animation has two images which shows alternately.
  - Convert the pixel image to C array and show it on the screen.
* Wrote a website for viewing the scores
* Implemented submission of your score to an online leaderboard
* Temperature detection that influences the game state
  - When the environment temperature is lower or higher than 27 Celsius, the percentage for happiness and sleeping will drop quickly

-----
## Simple M5 Stack Maze Game

### Team: 810
* Qianxiang Ma
  - UI implementation
* Liang Wei
  - Network connection
  - net and server clients
* Kevin Lee
  - Write demo summary
  - design game controls

### Project Summary
For this project, we wanted to create a simple 2D game inspired by Super Mario Bros. that allows the user to navigate through a maze using left, right, and jump controls. The objective of our game is to navigate through the maze and complete it as fast as possible. We utilized the M5 Stack’s LCD screen to display the game as well as the buttons to allow for navigation.

Each attempt will be timed and logged to a simple server, which the M5 Stack will connect to using its wireless wifi capabilities. The completion times will be ranked from fastest to slowest and displayed on the server.

Because of the nature of the game, we must utilize FreeRTOS features to develop it. For instance, we make use of multitasking to allow for simultaneous button input and background display on the M5 Stack.

-----
## M5 Pet

### Team: Nine

* Joshua Manzano

### Project Summary

The project consists of a virtual pet which you interact with through the three buttons that the M5 Stack has. The mechanics work similarly to Tamagotchi (たまごっち, 拓麻歌子), wherein you feed and take care of the virtual pet. The DHT12 Temperature and Humidity sensor from the Proto package will allow the virtual pet to feel the current environment around it, shivering when it is cold and sweating when it is hot. The virtual pet receives a periodical increase of hunger and thirst depending on the temperature and humidity of the environment. Random events may also happen based on a random number generator and the current temperature and humidity. The virtual pet also has the capability to locate open WiFi networks and connect to them, in which the virtual pet can jump to another device and you can interact with it through a webpage (HTTP).

* The periodic tasks are as follows:
  - Increase of hunger, thirst, comfort etc.
  - Movement of the virtual pet
  - Temperature and Humidity measurements
  - WiFi Scanning
  - Generating a random number to check if a random event should happen
* The aperiodic tasks are as follows:
  - Interaction of the user (feeding, comforting, etc.)
  - Connecting to a WiFi network
  - Random event triggered by a random number

-----
## Alarm clock prevent from despair awake

### Team: non-sugar-cocoa
* Ryotaro Onuki
    - Project Management
    - Hardware Design
* Takuma Yoshioka
    - System Design
* Masashi Oyama
    - User Interface Design
* Takeshi Sekihara
    - Software Implementation

### Project summary

We made an alarm clock that we have never seen before.
This product will give you a exciting life!

#### Key Function 1: One job to get up

This function is very effective to prevent users from going back to sleep.
The device will ring a sound when the time set the alarm comes.
However, you cannot stop this alarm by just pressing the button.
In order to stop the sound, you must shake the device again and again.
Such intense exercise help you to wake clearly and have a refreshing morning.
As IMU is installed in M5stack, this function can be implemented.

#### Key Function 2: No worry about oversleep

If you overslept, you do not have to worry about it.
Since this device is connected to the Internet, it can send a message that you will be late.

#### Using M5stack Function

- WiFi communication
- LCD
- Button
- Speaker
- Gyro Sensor

-----
## POS Defender

### Team: Kilimanjaro
* Akihiko Yokoyama (B4, Dept. of Computer Science)
    * Send a signal to another M5Stack via WiFi.
    * Post to Slack via WiFi.
* Shohei Kuroiwa (B4, Dept. of Computer Science)
    * Handle Motion Sensor.
    * Hide web browser on PC.
    * Get a music by YouTube.
* Takahiro Ishihara (M1, Dept. of Systems and Control Engineering)
    * Manipulate a robot.
    * Bright a rotating warning light.
    * Play a music.

### Project Summary
POS(Parent Over Shoulder) is big issue for students who live with their parents.
We don't want to reveal our SNS accounts or something to our parents.
Then we develop POS Defender System.

To detect our parent entering our room, we use PIR Motion Sensor.
If M5Stack detects a human, M5Stack sends signals via WiFi.
First, M5Stack post when our parent entered our room to Slack.
Second, M5Stack send a signal to our PC.
If our PC receives a signal, PC kills Xorg/Wayland or do something to hide web browser or game window.
Third, M5Stack send a signal to another M5Stack.
Another M5Stack control a robot.
We equip this robot with a rotating warning light and omni or mechanum wheels.
If another M5Stack receives a signal, this robot start to move somewhere, bright a rotating warning light and play a music in order to attract our parent's attention.
We try to get a music by YouTube.
