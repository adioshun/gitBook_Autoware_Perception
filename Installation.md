## 1. 설치 

### 1.1 [도커 ](https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/Generic-x86-Docker)

Autoware newer than 1.6.0 is supported in Docker


    [요구사항]
    Ubuntu 16.04 / 18.04
    Generic amd64 (64-bit x86) Docker
    

#### A. Case 1: Using Pre-built Autoware Docker Images




#### B. Case 2: Creating a Custom Autoware Docker Image

```
$ git clone https://gitlab.com/autowarefoundation/autoware.ai/docker.git
$ cd docker/generic
$ ./build.sh
```


### 1.2 소스 코드 

https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/Source-Build


---

## 2. Quick Start : The operations of main functionalities 

> [Quick Start : youtube](https://www.youtube.com/watch?v=NDNcy0C-Has)

### 2.1 replay of demo data
- Replay the rosbag demo data downloaded from Nagoya University.
    1. Setup of demo data
    2. Launch Autoware
    3. Prepare to play rosbag
    4. Localization
    5. Mission planning
    6. Motion following
    

#### A. Setup of demo data : [ROSBAG Demo](https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/ROSBAG-Demo)


- 데이터셋 준비 

```
cd ~
mkdir .autoware
cd ~/.autoware


# A script for generating a demo launch file:
wget http://db3.ertl.jp/autoware/sample_data/my_launch.sh

#Map/calibration/path data (Moriyama area, 175MB):
wget http://db3.ertl.jp/autoware/sample_data/sample_moriyama_data.tar.gz

#rosbag data (3GB):
wget http://db3.ertl.jp/autoware/sample_data/sample_moriyama_150324.tar.gz
# Note that this ROSBAG data do not contain the video data. Therefore the object detection is not supported

# Unpack the demo data as follows.
tar xfz sample_moriyama_data.tar.gz
tar xfz sample_moriyama_150324.tar.gz
```

- Run my_launch.sh

```
# Run the following script to generate launch files.
sh my_launch.sh

# my_launch/폴더에 아래 파일들 생성 확인
my_map.launch		　　　　　# Load PointClouds and vector maps
my_sensing.launch	　        # Load device drivers
my_localization.launch	　        # Localozation
my_detection.launch	　        # Object detection
my_mission_planning.launch	　# Path planning
my_motion_planning.launch	　# Path following


```

#### B. Launch Autoware

```
/src/Autoware/ros
bash ./run
```

### 2.2 Autoware on a real vehicle
Drive a real vehicle with Autoware autonomously.





### 2.3 rosbag replay
Replay the data corrected on the procedure on left.

---

# Autoware

[Github](https://github.com/CPFL/Autoware), [Homepage](https://www.autoware.ai/)

## 1. 설치

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

sudo apt-get update
```

### 1.1 Indigo \(Ubuntu 14.04\)

```
sudo apt-get install ros-indigo-desktop-full ros-indigo-nmea-msgs ros-indigo-nmea-navsat-driver ros-indigo-sound-play ros-indigo-jsk-visualization ros-indigo-grid-map ros-indigo-gps-common

sudo apt-get install ros-indigo-controller-manager ros-indigo-ros-control ros-indigo-ros-controllers ros-indigo-gazebo-ros-control ros-indigo-sicktoolbox ros-indigo-sicktoolbox-wrapper ros-indigo-joystick-drivers ros-indigo-novatel-span-driver

sudo apt-get install libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu libgl1-mesa-dev libglew-dev software-properties-common libyaml-cpp-dev python-flask python-requests

sudo add-apt-repository ppa:mosquitto-dev/mosquitto-ppa; apt-get update

sudo apt-get install libmosquitto-dev
```

NOTE: Please **do not** install `ros-indigo-velodyne-pointcloud` package. Please uninstall it if you already installed.

### 1.1 Kinetic \(Ubuntu 16.4\)

```
sudo apt-get install ros-kinetic-desktop-full ros-kinetic-nmea-msgs ros-kinetic-nmea-navsat-driver ros-kinetic-sound-play ros-kinetic-jsk-visualization ros-kinetic-grid-map ros-kinetic-gps-common ros-kinetic-controller-manager ros-kinetic-ros-control ros-kinetic-ros-controllers ros-kinetic-gazebo-ros-control ros-kinetic-joystick-drivers libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu libgl1-mesa-dev libglew-dev python-wxgtk3.0 software-properties-common libmosquitto-dev libyaml-cpp-dev python-flask python-requests libcanberra-gtk-module

sudo rosdep init

rosdep update

# ENVIRONMENT SETUP
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

### 1.1 소스 설치

PCL소스 설치 후 진행  

OR PCL 패키지 설치 후 libopenni2-dev, VTK 설치 필요 


```python


$ cd $HOME
$ git clone https://github.com/CPFL/Autoware.git --recurse-submodules
$ cd ~/Autoware/ros/src
$ catkin_init_workspace
$ cd ../
$ rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO
$ ./catkin_make_release

$ cd $HOME/Autoware/ros
$ ./run
```


| Error Code | Solution |
| --- | --- |
| Could NOT find GLEW | `sudo apt-get install libglew-dev` |
| gconf\_value\_free: assertion 'value != NULL' failed | `ssh -X localhost`, `./run` |

### 1.2 Docker 설치

```
docker pull autoware/autoware:1.7.0-kinetic
docker pull kunfengchen/u14-indigo-autoware 
docker pull nownicked/autoware-x11running7
```

## 2. 실행

### 2.1 소스설치시

### 2.2 Docker 설치시

* xmanager - 연결 설정 - Connection/SSH/Tunneling/X11 Forwarding 체크, xManager체크

* 도커 실생   `docker run -it --rm --net host --env="DISPLAY" --privileged -v /tmp/.X11-unix:/tmp/.X11-unix --volume "$HOME/.Xauthority:/root/.Xauthority:rw" --name "x11" adioshun/ubuntu16:Open3D /bin/bash`

* 도커 내에서 `cd /src/Autoware/ros/ && ./run`


---

Error 

Process Manager
./run: line 49: --geometry=50x10+0+0: command not found
./run: line 52: --geometry=50x10+500+0: command not found


```python

#!/bin/bash
# get where I am
MY_PATH=$(readlink -f  $(dirname $0))

# what type of terminal
OPTION_WORKING_DIR='--working-directory'
OPTION_CORE_GEOMETRY='--geometry=50x10+0+0'
OPTION_RM_GEOMETRY='--geometry=50x10+500+0'
OPTION_COMMAND='--command'


MASTER_DISPLAY_OPTION="${OPTION_CORE_GEOMETRY} ${OPTION_TITLE}\=\"roscore\""
RUNMGR_DISPLAY_OPTION="${OPTION_RM_GEOMETRY} ${OPTION_TITLE}\=\"runtime_manager\""

if [ $(which gnome-terminal) ]; then
    TERMINAL=gnome-terminal
    GNOME_VERSION=$(gnome-terminal --version | cut -d '.' -f 2)
    if [ ${GNOME_VERSION} -ge 14 ]; then
        MASTER_DISPLAY_OPTION=''
        RUNMGR_DISPLAY_OPTION=''
    fi
elif [ $(which mate-terminal) ]; then
    TERMINAL=mate-terminal
elif [ $(which xfce4-terminal) ]; then
    TERMINAL=xfce4-terminal
elif [ $(which lxterminal) ]; then
    TERMINAL=lxterminal
elif [ $(which konsole) ]; then
    TERMINAL=konsole
    OPTION_WORKING_DIR='--workdir'
    OPTION_CORE_GEOMETRY=''
    OPTION_RM_GEOMETRY=''
    OPTION_PM_GEOMETRY=''
    OPTION_COMMAND='-e'
    OPTION_TITLE='-T'
fi

echo "Process Manager"

gksudo --message "Please input password for launching process manager" \
       -- $MY_PATH/run_proc_manager &

ADDR=$($MY_PATH/src/.config/rviz/subnet_chk.py -)
if [ "$?" == "0" ]; then
  export ROS_IP=$ADDR
fi

# boot ros-master
#${TERMINAL} ${MASTER_DISPLAY_OPTION} ${OPTION_WORKING_DIR}=${MY_PATH} ${OPTION_COMMAND}="bash -c 'source ./devel/setup.bash; roscore'"&

# boot runtime_manager
#${TERMINAL} ${RUNMGR_DISPLAY_OPTION} ${OPTION_WORKING_DIR}=${MY_PATH} ${OPTION_COMMAND}="bash -c 'source ./devel/setup.bash; rosrun runtime_manager runtime_manager_dialog.py'"


if [ $(TERMINAL) ]; then
 ${TERMINAL} ${OPTION_CORE_GEOMETRY} ${OPTION_TITLE}="roscore" --${OPTION_WORKING_DIR}=${MY_PATH} ${OPTION_COMMAND}="bash -c 'source ./devel/setup.bash; roscore'"&
 
 # boot runtime_manager
 ${TERMINAL} ${OPTION_RM_GEOMETRY} ${OPTION_TITLE}="runtime_manager" --${OPTION_WORKING_DIR}=${MY_PATH} ${OPTION_COMMAND}="bash -c 'source ./devel/setup.bash; rosrun runtime_manager runtime_manager_dialog.py'"

else
     bash -c 'source ./devel/setup.bash; roscore'&
     bash -c 'source ./devel/setup.bash; rosrun runtime_manager runtime_manager_dialog.py'
fi


```