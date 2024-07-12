## Apply the autonomous exploration to the turtlebot
### The explore-lite package
explore-lite offers voracious boundary-based exploration. When the node is running, the robot greedily explores its environment until it can't find a boundary, and its move command is sent to the move-base node. explore lite does not create its own cost graph, which makes configuration easier and more efficient (with fewer resources).

1.Install the explore_lite

   Use the command `git clone https://github.com/hrnr/m-explore.git`
   
2. Adjust the launch files

   Adjust the parameters `robot_base_frame`, `costmap_topic` and `costmap_updates_topic`
   ```xml
   <param name="robot_base_frame" value="base_footprint"/>
	  <param name="costmap_topic" value="move_base/global_costmap/costmap"/>
	  <param name="costmap_updates_topic" value="move_base/global_costmap/costmap_updates"/>

3.Create a launch file to simultaneously start the turtlebot and explore-lite
   ```xml
       <launch>
       <include file="$(find turtlebot3_gazebo)/launch/turtlebot3_world.launch"/>
       <include file="$(find turtlebot3_slam)/launch/turtlebot3_slam.launch">
       <arg name="slam_methods" value="cartographer"/>
       </include>
       <include file="/home/dunpeng/el_ws/src/m-explore/explore/launch/explore.launch"/>
       </launch>
```
 4.Result

   Although the terminal did not report any errors during operation, the robot in turtlebot did not respond, and after checking where possible, it successfully ran once and then became inoperable
