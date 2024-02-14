# ORB_SLAM3

This repository is a modified version of [ORB_SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3)  

--- 

## Modification
- Succesfully tested in **Ubuntu 22.04** and **ROS2 Humble**(with >OpenCV 4.2)
- Update from C++11 to C++14
- Fixed unexpected <span style="color:red">error</span> when start **STEREO** mode with **Rectified** camera type


## Prerequisitis

### Eigen3

```
sudo apt install libeigen3-dev
```

### Pangolin and configuring dynamic library path

We install Pangolin system wide and configure the dynamic library path so the necessary .so from Pangolin can be found by ros2 package during run time. More info here https://robotics.stackexchange.com/questions/105973/ros2-port-of-orb-slam3-can-copy-libdow2-so-and-libg2o-so-using-cmake-but-gettin

#### Install Pangolin

```
cd ~/Documents
git clone https://github.com/stevenlovegrove/Pangolin
cd Pangolin
./scripts/install_prerequisites.sh --dry-run recommended [Check what recommended softwares needs to be installed]
./scripts/install_prerequisites.sh recommended [Install recommended dependencies]
cmake -B build
cmake --build build -j4
sudo cmake --install build
```

#### Configure dynamic library

Check if ```/usr/lib/local``` is in the LIBRARY PATH

```
echo $LD_LIBRARY_PATH
```

If not, then perform the following 

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/local
sudo ldconfig
```

Then open the ```.bashrc``` file in ```\home``` directory and add these lines at the very end

```
if [[ ":$LD_LIBRARY_PATH:" != *":/usr/local/lib:"* ]]; then
    export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
fi
```

Finally, source ```.bashrc``` file 

```
source ~/.bashrc
```

### OpenCV

Ubuntu 22.04 by default comes with >OpenCV 4.2. Check to make sure you have at least 4.2 installed. Run the following in a terminal

```
python3 -c "import cv2; print(cv2.__version__)" 
```

## Installation
Clone the repository:
```
git clone https://github.com/guyuehome/ORB_SLAM3.git
```

Install same required dependencies as original version. Then,  
Execute:
```
cd ORB_SLAM3
chmod +x build.sh
./build.sh
```
This will create **libORB_SLAM3.so**  at *lib* folder and the executables in *Examples* folder.

## Run

### Dataset
```
cd ORB_SLAM3
wget -c http://robotics.ethz.ch/~asl-datasets/ijrr_euroc_mav_dataset/machine_hall/MH_01_easy/MH_01_easy.zip
unzip MH_01_easy.zip
./Examples/Monocular/mono_euroc ./Vocabulary/ORBvoc.txt ./Examples/Monocular/EuRoC.yaml MH_01_easy ./Examples/Monocular/EuRoC_TimeStamps/MH01.txt dataset-MH01_mono
```


