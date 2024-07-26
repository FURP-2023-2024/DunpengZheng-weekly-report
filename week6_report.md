# Weekly Report

**Date:** 2024-07-22

## Summary

This week, I focused on downloading and using the Unitree quadruped robot SDK, as well as conducting simulations. The report details the steps taken, challenges faced, and the results obtained.

## Tasks Completed

### 1. Downloading Unitree SDK

- **Objective:** Obtain the Unitree SDK for the quadruped robot to explore its functionalities and capabilities.
- **Steps Taken:**
  - Visited the [Unitree Robotics GitHub repository](https://github.com/unitreerobotics).
  - Cloned the SDK repository using the following command:
    ```bash
    git clone https://github.com/unitreerobotics/unitree_ros.git
    ```
  - Navigated to the SDK directory:
    ```bash
    cd unitree_ros
    ```

### 2. Setting Up the Environment

- **Objective:** Ensure that the environment is properly set up to run the SDK and simulations.
- **Steps Taken:**
  - Installed necessary dependencies:
    ```bash
    sudo apt-get update
    sudo apt-get install ros-noetic-desktop-full
    sudo apt-get install ros-noetic-pcl-conversions
    sudo apt-get install libeigen3-dev
    ```
  - Built the SDK:
    ```bash
    catkin_make
    source devel/setup.bash
    ```

### 3. Running Simulations

- **Objective:** Conduct simulations to test the functionalities of the Unitree quadruped robot.
- **Steps Taken:**
  - Launched the simulation environment:
    ```bash
    roslaunch unitree_ros simulation.launch
    ```
  - Executed example control scripts provided in the SDK:
    ```bash
    rosrun unitree_ros example_control_script
    ```

### 4. Adding and Configuring Lidar Sensor

- **Objective:** Integrate a Lidar sensor with the Unitree robot in the simulation.
- **Steps Taken:**
  - Edited the URDF file to include the Lidar sensor:
    ```xml
    <link name="lidar_link">
      <visual>
        <geometry>
          <cylinder length="0.1" radius="0.05"/>
        </geometry>
        <material name="grey"/>
      </visual>
      <origin xyz="0 0 0.1" rpy="0 0 0"/>
    </link>

    <joint name="lidar_joint" type="fixed">
      <parent link="base_link"/>
      <child link="lidar_link"/>
      <origin xyz="0 0 0.2" rpy="0 0 0"/>
    </joint>
    ```
  - Configured the Lidar sensor parameters in the simulation launch file.

## Challenges Faced

- **Dependency Issues:** Encountered issues with missing dependencies during the setup process. Resolved by installing additional packages.
- **URDF Configuration:** Faced difficulties in correctly configuring the URDF file to include the Lidar sensor. Consulted documentation and community forums for solutions.

## Results

- Successfully downloaded and set up the Unitree SDK.
- Conducted initial simulations to test the quadruped robot's functionalities.
