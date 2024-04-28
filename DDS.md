# Quick fix and DDS issue with Nav2

- ROS 2 (ROS Humble 버전) 환경에서 Nav2 패키지를 사용하는 과정에서 DDS(Distributed Data Service)를 위한 설정 변경
- CycloneDDS를 사용함으로써 데이터의 신뢰성과 효율성을 높이고, Navigation2 설정을 변경하여 로봇의 정확한 위치 추정과 경로 계획을 도움

  
```sh
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install ros-humble-rmw-cyclonedds-cpp
```
- bashrc
```sh
$ subl ~/.bashrc
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
$ source ~/.bashrc
```

```sh
$ cd /opt/ros/humble/
$ cd share
$ cd turtlebot3_navigation2/
$ cd param/
$ sudo gedit waffle.yaml
# robot_model_type 수정 후 저장
# 주석 처리하고 한 줄 더 생성하여 "nav2_amcl::DifferentialMotionModel"
$ sudo reboot now 
```
