<h1 align="center">ROCK, PAPER, SCISSORS ROBOT</h1>
<p align="center">
  See it on my portfolio: https://codynichoson.com/rockpaperscissors.html
</p>
  
<p align="center">
  <img src="https://user-images.githubusercontent.com/62906322/158316359-afae747c-502e-4fc8-93f2-b7ab63d12bdf.png" alt="Rock Paper Scissors Hand" width="700"/>
</p>

In this solo project, I set out to create a rock, paper, scissors robotic partner that would allow a user to play in a similar fashion as they would another human. Meeting this requirement meant that some creative computer vision techniques were necessary to facilitate gameplay using natural gestures. The project made use of the Wonik Allegro Robotic Hand, OpenCV computer vision library, and MediaPipe machine learning library in order to create the final result.

### Hardware
* Wonik Allegro Robotic Hand Version 4.0 (http://wiki.wonikrobotics.com/AllegroHandWiki/index.php/Allegro_Hand_v4.0)
* PCAN-USB Adapter (https://www.peak-system.com/PCAN-USB.199.0.html?&L=1)
  * Allegro code is written for PCAN devices 

### Software
* Robot Operating System (ROS)
* MediaPipe Machine Learning Library
* BHand Library (http://wiki.wonikrobotics.com/AllegroHandWiki/index.php/BHand_library)

### Software Setup (Some of this is from Wonik Robotics' website)
1. Install necessary packages
```
sudo apt-get install cmake gcc g++ libpopt-dev
```
2. Install MediaPipe
```
pip install mediapipe
```
3. Download, build, and install PCAN-USB driver for Linux (http://www.peak-system.com/fileadmin/media/linux/index.htm#download)
```
tar -xzvf peak-linux-driver-x.x.tar.gz
cd peak-linux-driver-x.x
make NET=NO
sudo make install
sudo modprobe pcan
```
4. Create a `catkin_ws/src` for the necessary packages, then `cd` into the `src` directory:
```
mkdir catkin_ws/src
cd catkin_ws/src
```
6. Download my fork of the `allegro_hand_ros_v4` package into `catkin_ws/src` directory:
```
git clone git@github.com:codynichoson/allegro_hand_ros_v4.git
```
6. Download this package into `catkin_ws/src` directory:
```
git clone git@github.com:codynichoson/RockPaperScissorsRobot.git
```
7. Return to the base of the workspace, make, and source:
```
cd ..
catkin_make
source devel/setup.bash
```

### Hardware Setup
1. Plug the power/CAN connector into the Allegro hand.
2. Plug the USB/PEAK-CAN connector into your computer.
3. Turn the hand on using the toggle switch on the side. You should hear an audible beep and see the red light flash.

### Operating Instructions
1. To play rock, paper, scissors, run:
```
roslaunch rockpaperscissors rockpaperscissors.launch
```
2. A video window should open using your default camera.
3. Hold your hand clearly in frame, and move it up and down to "countdown" in order to begin the game. You should choose a rock, paper, scissors pose when the timer hits '4'. The Allegro hand will also choose a pose, and the score will be updated accordingly.

### Package
#### Launchfiles
`rockpaperscissors.launch`
#### Nodes
`perception`

This node opens the default camera on your computer and uses the MediaPipe machine learning library to identify hand gestures in frame. These gestures are then used to play and score the game of rock, paper, scissors.

`control`

This node takes in gesture commands from the perception node after the game begins and sets the Allegro hand to a specific configuration of joint states.
