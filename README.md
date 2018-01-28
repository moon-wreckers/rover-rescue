# Dependencies

Install Ubuntu 14.04
Install ROS Indigo
Setup catkin workspace, and go through tutorials if needed 

`sudo apt-get install libusb-dev libspnav-dev libbluetooth-dev libcwiid-dev`

# Installation
Enter into your catkin_ws/src directory and recursively clone this repository. Note the period at the end of this command, which clones all submodules directly into the src/ directory without a top-level folder.

`git clone --recursive -j8 https://github.com/moon-wreckers/rover-rescue.git .`


Make catkin workspace with `catkin_make`

# Setting up Aliases

`gedit ~/.bashrc`

Add the following lines to the bottom of your .bashrc file, they source the proper setup files for your ROS system and add the aliases to quickly change the ROS_MASTER_URI to the proper IP, since in step 12 we are changing our IP to the one the rover is looking to listen to. Save the file and close.

```
alias sim="export ROS_MASTER_URI=http://localhost:11311; export ROS_IP=127.0.0.1"
alias houston="export ROS_MASTER_URI=http://192.168.1.2:11311; export ROS_IP=192.168.1.2"
alias ak1="export ROS_MASTER_URI=http://192.168.1.11:11311;"
alias ak2="export ROS_MASTER_URI=http://192.168.1.12:11311;"

source /opt/ros/indigo/setup.bash
source ~/catkin_ws/devel/setup.bash
```
 
Use sim - (an alias/ command shortcut that you set in the last step)  to set your ROS_MASTER_URI back to normal operation.

Look at the light on the AutoKrawler's wifi adapter. If it's blinking then it's connected to a wifi network. Connect to the network that the AutoKrawlers are on, and you can ping them with `ping 192.168.1.11` or `ping 192.168.1.12`.


# Running the AutoKrawler
Set your ip address to 192.168.1.2 (the ip that the AutoKrawlers use as ROS_MASTER_URI by default).
`sudo ifconfig wlan0 192.168.1.2 netmask 255.255.255.0`
If this command doesn't work try `ifconfig` to ensure you're using the correct network interface like `wlan0`.

Run `roscore` on your machine.

Open new terminal and SSH into the rover.

`ssh odroid@192.168.1.11`

It's recommended you use `screen` to start a screen session. This starts a kind of virtual terminal that you can reconnect to if you get disconnected. If you get disconnected just ssh back in and type `screen -r` to reconnect to your screen session. To disconnect from a screen session hold the `ctrl` key and press the `a` then the `d` key.

`roslaunch autokrawler ak1_autocontrol.launch`

Now the rover should listen to both teleoperated commands or planned path commands. To teleoperate, turn on the corresponding PS4 controller, hold the R1 bumper button, and drive with the joysticks.



Dependency:

sudo apt-get install libusb-dev libspnav-dev libbluetooth-dev libcwiid-dev


https://github.com/ros-planning/navigation
https://github.com/MASKOR/maskor_navigation



Using the DualShock4 (PS4) Gamepad
If you plug in the adapter and turn on the gamepad with the PlayStation button and see a solid blue light, then the gamepad is connected and you can move on to start the ROS node.

Pairing Instructions
Plug in a PS4 Wireless USB Adapter, notice the blue light on the tip. 
Push the adapter in towards the computer until the blue light starts flashing.
On the DuaShock4 Controller simultaneously press and hold the PlayStation button in the middle, and the SHARE button on the top right. It should blink in a heartbeat pattern, then quickly turn solid blue when connected with the adapter.

ROS Instructions
Once roscore is run on the master, ensure that ROS_IP and ROS_MASTER_URI are set then plug the USB dongle into your computer or the krawler and run roslaunch autokrawler teleop_gamepad.launch
If that fails to publish to /ak1/cmd_vel then ensure that your controller is registered as /dev/input/js0 .

Driving Instructions
The top right bumper is the deadman switch, hold that down while driving. 
Use the two joysticks to turn and drive.
Use the right trigger as a boost mode, left trigger as a granny mode. 

