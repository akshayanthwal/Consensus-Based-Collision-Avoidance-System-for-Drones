# Pre-requiites:

ROS 1 Noetic - Follow ROS installation tutorial at wiki.ros.org

MAVROS - Follow Installation tutorial at https://ardupilot.org/dev/docs/ros-install.html

UTM Library - pip install utm

PyGeodesy Library - pip install PyGeodesy

Python Dependencies - sudo apt install python-matplotlib python-serial python-wxgtk3.0 python-wxtools python-lxml python-scipy python-opencv ccache gawk python-pip python-pexpect

Catkin Tools - sudo apt-get install python3-catkin-tools

MAVProxy - sudo pip install future pymavlink MAVProxy



# Workspace Setup:

Clone the GitHub repo - git clone https://github.com/akshayanthwal/Consensus-Based-Collision-Avoidance-System-for-Drones.git

Extract the contents of CAS.zip and place the contents in the directory /home/<username>

Install ArduPilot Dependencies - 
cd ardupilot
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH

Setup Catkin workspace - 
cd cas_ws
catkin build
echo 'source ~/cas_ws/devel/setup.bash' >> ~/.bashrc

Setup ardupilot-gazebo plugin -
mkdir build
cd build
cmake ..
make -j4
sudo make install
echo 'export GAZEBO_RESOURCE_PATH=~/ardupilot_gazebo/worlds:${GAZEBO_RESOURCE_PATH}' >> ~/.bashrc
echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
echo 'export GAZEBO_MODEL_PATH=~/ardupilot_gazebo/models' >> ~/.bashrc
echo 'export GAZEBO_RESOURCE_PATH=~/ardupilot_gazebo/worlds:${GAZEBO_RESOURCE_PATH}' >> ~/.bashrc
source ~/.bashrc

How to Run the simulation:
Make sure that the directories mentioned in collision.sh, collision_control_drone1.py and collision_control_drone2.py (both inside collision_avoidance package of cas_ws) are according to your system.

Initialize the gazebo world-
./simulation.sh

Once you see 2 XTerm windows - 
roslaunch collision_avoidance 2_apm.launch

Once you see "mission received" - 
roslaunch collision_avoidance col_takeoff.launch

If the drones fail to takeoff - 
rosclean purge

To record the trajectories of the drones -
rosrun collision_avoidance gcs.py
