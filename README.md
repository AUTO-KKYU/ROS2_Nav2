# ROS2_Nav2

## Install Nav2 for ROS2
```sh
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install ros-humble-navigation2 ros-humble-nav2-bringup ros-humble-turtlebot3*
```

### Make Robot Move int the Environment
- bashrc 들어가서 다음과 같은 코드 작성
    - gedit ~/.bashrc
    - subl ~/.bashrc
    - code ~/.bashrc
    - nano ~/.bashrc
```sh
export TURTLEBOT3_MODEL=waffle
source /opt/ros/humble/setup.bash
# 수정 후 밖으로 나와서
$ source ~/.bashrc
```
- 명령어로 확인
```sh
$ printenv | grep TURTLE
```

### 현재 Gazebo 프로세스가 실행중일 때
1. 현재 실행 중인 Gazebo 프로세스 찾기
```sh
$ ps aux | grep gazebo
# 찾은 후, gzserver or ros2 launch 프로세스 종료하기
$ kill -9 [PID]
# 최소 예제 실행 테스트
$ gazebo --verbose /opt/ros/humble/share/turtlebot3_gazebo/worlds/turtlebot3_world.world
### 결과는 아래와 같다
```
<img src= "https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/07d21176-6950-4945-b0a5-5c95dbc48b15">

### Turtlebot in Gazebo
```sh
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
<img src= "https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/64ead10e-8266-404f-a7a0-57cc51ca53bc">

**- Move Turtlebot3**
- w : 선속도 증가
- x : 선속도 감소
- a : 각속도 증가
- d : 각속도 감소

```sh
$ ros2 run turtlebot3_teleop teleop_keyboard
```
- rqt_graph
<img src= "https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/cfee1aed-2c92-4239-985e-c77a86fa7842">

https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/933cfb8d-0b64-453b-88ec-7dacaeab1f85

---
## Generate a map with SLAM
- Prepare 3 terminals
```sh
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
- SLAM feature
```sh
$ ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```
- movement check
```sh
$ ros2 run turtlebot3_teleop teleop_keyboard
```

https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/7e9fe6a9-678e-4829-94b3-63b39fe8a4ad

**- SAVE the map information**
```sh
$ mkdir maps
$ ros2 run nav2_map_server map_saver_cli -f maps/my_map
```
<img src= "https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/7bec6f63-8973-4c73-af54-160338f4edac">

---
## Make the robot navigate using the map
- gazebo로 turtlebot3 불러오기
```sh
$ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```
- 저장한 맵을 rviz에 띄우기 
```sh
$ ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=maps/my_map.yaml
```

- 2D Pose estimate로 로봇 위치 조정하기
<img src= "https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/02911ae2-0ea6-4317-9955-5f164f5de56e">

- Nav2 Goal 설정 : 목표 지점까지 로봇이 움직임
  
https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/00a4a9b1-d354-4090-b557-ef1c94f13abc

- waypoint follower : goal로 설정한 지점들을 이동하여 원하는 중간 중간 거쳐갈 수 있음
    - Waypoint / Nav Through Poses Mode 버튼을 누른 후 Nav2 Goal을 맵에 임의로 지정한 다음에 Start Waypoint Following 버튼 클릭하면 지정한 waypoint대로 로봇이 움직인다

https://github.com/AUTO-KKYU/ROS2_Nav2/assets/118419026/3231d9af-8517-4a54-8f59-7d00e6f99cad



