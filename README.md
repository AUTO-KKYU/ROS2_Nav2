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








