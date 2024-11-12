# diffusion_policy_for_STL

## Install ros2-humble
Reference:
https://getiot.tech/ros2/ros2-installation-on-ubuntu/
```
sudo apt install software-properties-common
sudo add-apt-repository universe

sudo apt update && sudo apt install curl
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
May have some connection errors, but can proceed to run:
```
sudo apt install ros-humble-desktop
sudo apt install ros-humble-ros-base
sudo apt install ros-dev-tools
```
## Install isaac
Reference:
https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html
```
sudo snap install --classic cmake
sudo apt install build-essential
```
Then follow the instructions in the Nvidia official document.

## Integrate moveIt with isaac
Reference: 
https://www.youtube.com/watch?v=pGje2slp6-s

```
sudo apt install ros-humble-ros2-control
sudo apt install ros-humble-ros2-controllers
sudo apt install ros-humble-gripper-controllers
sudo apt install ros-humble-moveit-py
```

If encounter:
```
E: Unable to locate package ros-humble-moveit-py
```
Remember to run 
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
## Configure moveIt 
```
source /opt/ros/humble/setup.bash # Enable ros2
cd moveit2_UR5/
colcon build
source install/setup.bash # Add the robot_description into ros path

ros2 launch moveit_setup_assistant setup_assistant.launch.py # Run moveit assistant
```

If encounter:
```
[moveit_setup_assistant-1] [rviz_rendering:error] RenderingAPIException: Unable to create a suitable GLXContext in GLXContext::GLXContext at ./.obj-x86_64-linux-gnu/ogre-v1.12.1-prefix/src/ogre-v1.12.1/RenderSystems/GLSupport/src/GLX/OgreGLXContext.cpp (line 60), at ./src/rviz_rendering/ogre_logging.cpp:70
[moveit_setup_assistant-1] [rviz_rendering:error] rviz::RenderSystem: error creating render window: RenderingAPIException: Unable to create a suitable GLXContext in GLXContext::GLXContext at ./.obj-x86_64-linux-gnu/ogre-v1.12.1-prefix/src/ogre-v1.12.1/RenderSystems/GLSupport/src/GLX/OgreGLXContext.cpp (line 60), at ./src/rviz_rendering/render_system.cpp:576
[moveit_setup_assistant-1] [rviz_rendering:error] Unable to create the rendering window after 100 tries, at ./src/rviz_rendering/render_system.cpp:530
[moveit_setup_assistant-1] terminate called after throwing an instance of 'std::runtime_error'
[moveit_setup_assistant-1]   what():  Unable to create the rendering window after 100 tries
[ERROR] [moveit_setup_assistant-1]: process has died [pid 983204, exit code -6, cmd '/opt/ros/humble/lib/moveit_setup_assistant/moveit_setup_assistant --ros-args'].
```

This means the OpenGL is not configured properly.
Try to install the basic OpenGL development packages:
```
sudo apt-get update
sudo apt-get install -y \
    libgl1-mesa-dev \
    libglu1-mesa-dev \
    freeglut3-dev \
    mesa-common-dev
```

Need to install `topic-based-ros2-control` [repo](https://github.com/PickNikRobotics/topic_based_ros2_control/blob/main/doc/installation.md)
```
sudo apt-get install ros-humble-topic-based-ros2-control
```
If encounter 
```
E: Unable to locate package topic-based-ros2-control
```
or 
```
Err:8 http://packages.ros.org/ros2/ubuntu jammy InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY F42ED6FBAB17C654
Reading package lists... Done
W: GPG error: http://packages.ros.org/ros2/ubuntu jammy InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY F42ED6FBAB17C654
E: The repository 'http://packages.ros.org/ros2/ubuntu jammy InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

when run `sudo apt update`, this is probably because of the key is not well installed.

In my case, it's because I declared to use the key under `/usr/share/keyrings/` in `/etc/apt/sources.list.d/ros2.list`, but actually the key is installed in other place. 

Try: 
```
# Download and dearmor the key to place it in the keyrings folder
curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo gpg --dearmor -o /usr/share/keyrings/ros-archive-keyring.gpg
```
and make sure the content in `etc/apt/sources.list.d/ros2.list` is:
```
deb [signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main
```

In-painting
CBF
