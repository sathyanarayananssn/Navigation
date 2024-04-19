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
For Keyboard: Run the ros package in new tap.
ros2 run teleop_twist_keyboard teleop_twist_keyboard
# Rviz 
Open the new tap
cd ~/bot_1/
rviz2 -d src/config/main.rviz


