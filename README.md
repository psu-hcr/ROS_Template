# ROS_Template
A template and instructions for starting your own ROS package


Requirements
-----------

Use of the ROS_Template requires several packages to be installed and a file structure in place:

* [ROS] - The Robot Operating System
* A catkin workspace - Setup a new workspace with these commands
`mkdir chosenname_ws && cd chosenname_ws && mkdir src`
`catkin_init_workspace`

Dependencies
-------------

### Use this repo to start a package

1. **Clone this repository to your workspace**:
	```sh
	cd chosenname_ws
	git clone https://github.com/psu-hcr/ROS_Template.git src/nameofyourpackage```
2. **Stop tracking this repo** (You probably want to track this as your own repo, so let's remove the git stuff): 
```sh
cd src/nameofyourpackage
rm -rf .git
```

3. **Start tracking it as a new repo**: `git init`
4. **Optional**, but strongly recommended: Setup your own repo on Github.

```sh
git remote add origin https://github.com/psu-hcr/nameofyourpackage.git
git branch -M main
git push -u origin main
```
5. **Source your catkin workspace at the begining of every terminal session**. This is done by navigating to the top level of the workspace 
```cd ~/chosenname_ws```. 
Ensure that all your most recent changes have been incorporate by running 
```catkin_make``` 
and running this command 
```source devel/setup.bash```

-------------
### Required Files for your ROS package
#### CMakeLists.txt
- The most basic version of this just has a few lines
```sh
cmake_minimum_required(VERSION 2.8.3)
project(nameofyourpackage)
find_package(catkin REQUIRED)

```
- This repo has a more complex example that include additional dependencies for ARMADILLO, OpenCV, and OpenMP, and Kuka FRI. 
- For nodes written in C++, you need to include a similar syntax in your CMakelist as you would if you were building with CMake outside of ROS. Two examples are included in the CMakeLists.txt file in this repo. These examples assume that you have a folder called src within your repo meaning the full filepath to these cpp files is `~/chosenname_ws/src/nameofyourpackage/src/example1.cpp`. There are two folders in the file structure called **src**.

#### package.xml

- This file mostly contains information about who wrote the package and what it is intended for.
- You can and should also include dependencies here. This helps catkin identify any packages that are not installed.
-------------
### ALMOST Required File Structure
#### src Folder
- There should be an src folder in your package. This is where your python scripts or cpp code that runs each node should be store.
- We have included example1.cpp in this template because git tracks files but not folders. We had to put something in there to track the structure.
- You can embed even more structure in this folder, including additional directories that contain custom header files, etc
#### launch Folder
- Theoretically you could individually call each node that you want to run by opening multiple terminals, but in reality you want to use a launch file, so we have a folder called launch where you can store multiple launch files.
- The various launch files your write can be to startup nodes or your can use a single launch file with multiple arguments. In our example launch file, there are two possible arguments each of which have a default assigned. 
- To use the launch file, you use roslaunch in the terminal and specify the value of the arguments using **:=**
```sh
roslaunch nameofyourpackage nameofyourlaunchfile.launch vis:=true
```

-------------
### Optional, but helpful 
#### An RVIZ file
- RVIZ is a really common way to add a visualization to your ROS package. You will see that the exmaple launch file launches the rviz node. This should come installed with your ROS distribution unless you opted for a really bare bones install
- To run rviz, you need a .rviz file that basically saves the camera angles of your 3D visualization. - - To customize your rviz file
  -- Launch your node with the .rviz file provided in this repo. 
  -- Adjust the view (much the same way you adjust a view in CAD, then use the Save As function in RVIZ to either generate a new .rviz file or overwrite the existing one with your preferred settings.
  
#### Custom ROS message types
- ROS has a huge library of message types similar to the types found in C++, int, float, arrays, structs, but I have often found it helpful to define a custom message type as a way to collect a single synchronized data point
- This repo includes an example that collects the time of a simulated system, the coordinates describing the system state and their derivatives (q, dq,ddq). You can see that it is similar to defining a struct in C++.
#### A README
- Much like you are reading this, future users of your package including future you will be greatful for some instructions that go along with your github repo. Readmes are written in Markdown. It's pretty easy to catch on to the formatting with an example.
- You can use this very README.md file as the starting point for your own README

#### A bash script to record data published to Rostopics
- I've included an example **record.sh**. You can simply change the topics to your desired topics and adjust the naming schemes. 
- The example file records both a rosbag file of all active rostopics and generates several csv files for specific rostopics of interest.
	
