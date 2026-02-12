# Ubuntu22.04-ROS2-Installation-based-on-Virtual-Machine

## I. Download Ubuntu 20.04
Download Ubuntu Desktop from the official web site (https://ubuntu.com/download/desktop).

First, go to the official web site and click **'check out our alternative downloads'**.

![Image text](Image/Ubuntu22.04-1.png)

Then, go down and click **'Ubuntu 22.04 LTS (Jammy Jellyfish)'**.

![Image text](Image/Ubuntu22.04-2.png)

Finally, download **64-bit PC (AMD64) desktop image**.

![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/Ubuntu20.04-4.png)


## II. Download VirtualBox
### Why VirtualBox?
When using a traditional you need to install the operating system on a physical machine for evaluating software that cannot be installed on your current operating system. Oracle VirtualBox is what you need in this case, instead of reinstalling software on your physical machine. VirtualBox is designed to run virtual machines on your physical machine without reinstalling your OS that is running on a physical machine. One more VirtualBox advantage is that this product can be installed for free.

A virtual machine (VM) works much like a physical one. An OS and applications installed inside a VM “think” that they are running on a regular physical machine since emulated hardware is used for running VMs on VirtualBox. Virtual machines are isolated from each other and from the host operating system. Thus, you can perform your tests in isolated virtual machines without any concerns of damaging your host operating system or other virtual machines.

VirtualBox supports a long list of host and guest operating systems. A host OS is the operating system installed on a physical machine, on which VirtualBox is installed. A guest OS is an operating system installed on a virtual machine running inside VirtualBox. VirtualBox can be installed on Windows, Linux, macOS, Solaris, and FreeBSD. On VirtualBox you can run VMs with Windows, Linux, macOS, Solaris, FreeBSD, Novell Netware, and other operating systems.

Go to the official web site (Link: https://www.virtualbox.org/wiki/Downloads) to download the VirtualBox installer for your operating system. See in the figure below:

![Image text](https://github.com/cyiwen316/Virtual-Machine-Installation/blob/main/Image/VirtualBox.png)

### Run the installer and define the installation options

1. Run the VirtualBox installer. The installation wizard that has a GUI (graphical user interface) should appear.
   
2. Select the manner in which you want features to be installed, clicking on the installation directory and installed components—you can leave the default values. Then tick the checkboxes near shortcut options and file associations.

3. Confirm installation of VirtualBox network interfaces (click Yes).

4. On the Ready to Install Screen, hit Install to start the installation process.

5. After finishing installation, you can tick the checkbox for starting VirtualBox after installation.

### Deploying a New VM
Once you have installed VirtualBox, open the application. You can see the graphical user interface of VirtualBox which is unified for all supported host operating systems. You can also use the command line interface and VBoxManage if needed. In the current example VirtualBox is set up on Windows.

### Creating a Virtual Machine
Click **Machine** > **New** or hit the icon with the blue star to create a new virtual machine in VirtualBox GUI.

![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/How-to-setup-VirtualBox-%E2%80%93-Creating-a-new-VM-1.webp)

Specify name, Machine Folder (to save),Type and version for your virtual machine  and click on **Next**.

![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/5-12.png)

Here, we have to choose the base memory based on your host system RAM size. It is highly recommended to not choose less than 1GB (if possibly choose more than _25GB_).specify RAM _2048_ and click on **Next**.

![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/6-12.png)

> [!NOTE]
> Ubuntu recommends at least 25GB of free storage for smooth running.

Click on **settings** to see the system information of your virtual machine.

![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/11-9.png)

Load Ubuntu ISO Image file to your virtual machine:

Go to storage section and click on Empty then load your ubuntu 20.04 iso image from your local machine as shown below.
![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/12-10.png)

select **ubuntu 20.04 iso image** and click on **open**.
![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/13-7.png)

The Ubuntu 20.4 iso image has been loaded successfully to your virtual machine and click on **ok**.
![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/14-7.png)


Install Ubuntu 20.04.1 LTS in Virtual Machine: Click on Start to start the installing ubuntu.
![Image text](https://github.com/cyiwen316/ROS-Installation-based-on-Virtual-Machine/blob/main/Image/15-8.png)

> [!TIP]
> Full screen: Devices ->Insert Guest Additions CD image. And reboot Virtual System.

## III. Install ROS1

See http://wiki.ros.org/noetic/Installation/Ubuntu.

3.1 Setup your computer to accept software from packages.ros.org.
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

3.2 Set up your keys
```
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

3.3 Installation
First, make sure your Debian package index is up-to-date:
```
sudo apt update
```
Now pick how much of ROS you would like to install.
**Desktop-Full Install: (Recommended)** : Everything in **Desktop** plus 2D/3D simulators and 2D/3D perception packages
```
sudo apt install ros-noetic-desktop-full
```

3.4 Environment setup

You must source this script in every **bash** terminal you use ROS in.
```
source /opt/ros/noetic/setup.bash
```
It can be convenient to automatically source this script every time a new shell is launched. These commands will do that for you.

**Bash**
> [!CAUTION]
> If you have more than one ROS distribution installed, ~/.bashrc must only source the setup.bash for the version you are currently using.

```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

3.5 Dependencies for building packages

Up to now you have installed what you need to run the core ROS packages. To create and manage your own ROS workspaces, there are various tools and requirements that are distributed separately. For example, rosinstall is a frequently used command-line tool that enables you to easily download many source trees for ROS packages with one command.

To install this tool and other dependencies for building ROS packages, run:
```
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

Before you can use many ROS tools, you will need to initialize rosdep. rosdep enables you to easily install system dependencies for source you want to compile and is required to run some core components in ROS. If you have not yet installed **rosdep**, do so as follows.
```
sudo apt install python3-rosdep
```

With the following, you can initialize rosdep.
```
sudo rosdep init
rosdep update
```

## IV. Create a ROS Workspace
Let's create and build a catkin workspace:
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```

## V. Install gazebo_ros_pkgs
The gazebo_ros_pkgs packages are available in:

ROS Noetic:
```
sudo apt-get install ros-noetic-gazebo-ros-pkgs ros-noetic-gazebo-ros-control
```
### Setup A Catkin Workspace
These instructions require the use of the catkin build system.

If you do not have a catkin workspace setup, try the following commands:
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make
```
Then add to your **.bashrc** file a source to the setup scripts:
```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```

## VI. Install Gazabo_robotino
Install gazebo on your computer :
```
sudo apt install ros-noetic-gazebo-ros ros-noetic-gazebo-plugins gazebo11 
```

Make sure git is installed on your Ubuntu machine:
```
sudo apt-get install git
```

Open a new terminal :
```
cd ~
git clone https://github.com/cyiwen316/Gazebo_UPHF.git
echo 'export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:$HOME/Gazebo_UPHF/models' >> ~/.bashrc
source ~/.bashrc
```

```
cd ~/catkin_ws/src
git clone https://github.com/cyiwen316/gazebo_robotino_ros_pkg.git
cd ~/catkin_ws
catkin_make
```

```
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

How to use the simulator

To launch the simulator :

Open a terminal :
```
roslaunch gazebo_robotino_ros_pkg env_global.launch
```
You can launch the 3D frontend of gazebo by launching in a another terminal :
```
gzclient
```

There is a top camera on the simulation to see the robot and the terrain, you can see it by using rqt_image_view and looking the topic /gazebo/camera/top_camera/image_raw. You can run it in a new terminal :
```
rqt_image_view /gazebo/camera/top_camera/image_raw
```





> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.







