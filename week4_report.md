## Preapare the navigation package
1. Create a navigation pkg to contain all the necessary configuration files and launch files

   Command: `catkin_create_pkg my_robot_name_2dnav move_base my_tf_configuration_dep my_odom_configuration_dep my_sensor_configuration_dep `
2. Create the launch folder in this workspace to store all launch files. The first launch file to be created is the startup configuration file of the machine, including sensor, odom, tf, etc. node startup.
3. Configure the cost map, which contains three configuration items: common, global, and local.
   
   Common configuration items are the common configuration part of the cost map, and these configurations are usually used in both global and local cost maps. It mainly includes some basic Settings, such as robot frame, update frequency, map resolution, etc.
   The configuration in Turtlebot burger is:
   
