# diffusion_policy_for_STL

## Install ros2-humble
Reference:
https://getiot.tech/ros2/ros2-installation-on-ubuntu/
```
sudo apt install software-properties-common
sudo add-apt-repository universe

sudo apt update && sudo apt install curl
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
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

## Integrate moveit with isaac
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
Then run 
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

In-painting
CBF
