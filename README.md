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

In-painting
CBF
