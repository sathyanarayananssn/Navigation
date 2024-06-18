## Navigation of Ground Vehicle  
Install ROS2 humble from the source: https://docs.ros.org/en/humble/Installation.html
# Create Colcon Package
mkdir -p ~/bot_1/src
cd ~/bot_1/src
git clone https://github.com/sathyanarayananssn/Navigation.git
# Build colcon workspace
cd ~/bot_1/
colcon build
source install/setup.bash
# Launch the vehicle on gazebo
ros2 launch bot_one launch_sim.launch.py
# To move the vehicle
You can either move through joystick or keyboard.
For joystick make sure channel 6 and channel 7 are ON.
For Keyboard: Run the ros package in new tab.
ros2 run teleop_twist_keyboard teleop_twist_keyboard

# Rviz 
Open the new tab
cd ~/bot_1/
rviz2 -d src/config/main.rviz
# For mapping
In mapper_params_online_async.yaml
change scan_topic: /scan
mode: mapping
uncomment map_file_name
uncomment map_start_at_dock:true
open the terminal
ros2 launch slam_toolbox online_asyn_launch.py params_file:=./src/<file_name>/config/mapper_params_online_async.yaml use_sim_time:true

In rviz make the following changes
Click on add 
Map
change the topic /map
Update topic /map_updates
Global options: 
Fixed Frame map
Drive the robot in the enviroment in creates 2d Map arrou
To save
Click on pannel add slam toolbox
save map <map_name>
serialize map <serial_map_name>
Click save
# For navigation
In mapper_params_online_async.yaml
change scan_topic: /scan
mode: localization
map_file_name: <map_name>
map_start_at_dock:true

open the terminal
ros2 launch slam_toolbox online_asyn_launch.py params_file:=./src/<file_name>/config/mapper_params_online_async.yaml use_sim_time:true
new terminal
ros2 launch nav2_bringup navigation_launch.py
in rviz
add map
topic: /global_costmap/costmap
update topic: /global_costmap/costmap_updates
color scheme: costmap
in rviz on right hand side there you will see 2D Goal pose
Click on 2D Goal Pose and click on the map u can see gazebo moves to that point while avoiding the obstacle.


