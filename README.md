# MoveIt 2 motion planning for Hello Robot Stretch 3 mobile manipulator

This library has been tested on ROS Humble

## Installation
First we install MoveIt 2 and moveitpy. We need to build from source since it doesn't come with Humble prebuilt. This can take about 30 minutes.
```bash
sudo apt remove ros-$ROS_DISTRO-moveit*
mkdir -p ~/moveit2/ws_moveit2/src
cd ~/moveit2/ws_moveit2/src
git clone https://github.com/moveit/moveit2.git -b $ROS_DISTRO
for repo in moveit2/moveit2.repos $(f="moveit2/moveit2_$ROS_DISTRO.repos"; test -r $f && echo $f); do vcs import < "$repo"; done
rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y
cd ~/moveit2/ws_moveit2/
colcon build --event-handlers desktop_notification- status- --cmake-args -DCMAKE_BUILD_TYPE=Release --parallel-workers 1
echo 'source ~/moveit2/ws_moveit2/install/setup.bash' >> ~/.bashrc
source ~/moveit2/ws_moveit2/install/setup.bash
```

Next we will install the packages in this GitHub repo that link MoveIt 2 to Stretch 3.
```bash
mkdir -p ~/moveit2/ws_moveit2_stretch3/src
cd ~/moveit2/ws_moveit2_stretch3/src
git clone https://github.com/Zackory/stretch3_moveit2.git
rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y
cd ~/moveit2/ws_moveit2_stretch3/
colcon build --packages-select stretch_moveit2 stretch_simple_controller_manager
echo 'source ~/moveit2/ws_moveit2_stretch3/install/setup.bash' >> ~/.bashrc
source ~/moveit2/ws_moveit2_stretch3/install/setup.bash
```

## Launch MoveIt 2 in Rviz
```bash
stretch_free_robot_process.py
ros2 launch stretch_moveit2 movegroup_moveit2_stretch3.launch.py
```

