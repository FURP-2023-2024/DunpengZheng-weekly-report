## Preapare the navigation package
1. Create a navigation pkg to contain all the necessary configuration files and launch files

   Command: `catkin_create_pkg my_robot_name_2dnav move_base my_tf_configuration_dep my_odom_configuration_dep my_sensor_configuration_dep `
2. Create the launch folder in this workspace to store all launch files. The first launch file to be created is the startup configuration file of the machine, including sensor, odom, tf, etc. node startup.
3. Configure the cost map, which contains three configuration items: common, global, and local.
   
   Common configuration items are the common configuration part of the cost map, and these configurations are usually used in both global and local cost maps. It mainly includes some basic Settings, such as robot frame, update frequency, map resolution, etc.
   The configuration in Turtlebot burger is:
   ```yaml
   obstacle_range: 3.0
   raytrace_range: 3.5

   footprint: [[-0.105, -0.105], [-0.105, 0.105], [0.041, 0.105], [0.041, -0.105]]
   robot_radius: 0.105
   inflation_radius: 1.0
   cost_scaling_factor: 3.0

   map_type: costmap
   observation_sources: scan
   scan: {sensor_frame: base_scan, data_type: LaserScan, topic: scan, marking: true, clearing: true}
Among them, obstacle_range, raytrace_range, and footprint need to be modified when actually applied to quadruped robots.

In the global configuration item, robot_base_frame needs to be changed to the base frame of the quadruped robot, and static_map should be changed to false for dynamic navigation.
Similarly, all these parameters can be adjusted by referring to the official unitree documentation

4. Write a launch file for the application of these parameters to apply these parameters to the robot
   ```xml
   <launch>
   <node pkg="move_base" type="move_base" respawn="false" name="move_base" output="screen" clear_params="true">
    <rosparam file="$(find unitree_move_base)/config/costmap_common_params.yaml" command="load" ns="global_costmap" />
    <rosparam file="$(find unitree_move_base)/config/costmap_common_params.yaml" command="load" ns="local_costmap" />
    <rosparam file="$(find unitree_move_base)/config/local_costmap_params.yaml" command="load" />
    <rosparam file="$(find unitree_move_base)/config/global_costmap_params.yaml" command="load" />
    <rosparam file="$(find unitree_move_base)/config/base_local_planner_params.yaml" command="load" />
   </node>
   </launch>

