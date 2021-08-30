Steps to start airsim:
0. setup env.
    mkdir -p ~/Downloads/Airsim/ && https://github.com/microsoft/AirSim.git && cd ~/Downloads/Airsim/AirSim && git checkout v1.5.0-linux

    # install airsim with the scripts setup.sh and build.sh manually.

    sudo ln -s  /usr/lib/x86_64-linux-gnu/libstdc++.so.6  /usr/lib/x86_64-linux-gnu/libstdc++.so  # for clang+llvm we need cpplib files end with .so.

    mkdir -p ~/Downloads/Airsim/AirSim/cmake/airsim_sensors && cp ~/GAAS/simulation/src/airsim_sensors/CMakeLists.txt ~/Downloads/Airsim/AirSim/cmake/airsim_sensors/CMakeLists.txt

    cp -r ~/GAAS/simulation/src/airsim_sensors/ ~/Downloads/Airsim/AirSim/

    cd ~/Downloads/Airsim/AirSim && ./build.sh

1. prepare for simulation:

    cp simulation/Airsim/mavros_launch/* /opt/ros/melodic/share/mavros/launch/px4_airsim.launch

    cp ~/GAAS/simulation/Airsim/vehicles/{YOUR_VEHICLE_CONFIG_FILE} ~/Documents/AirSim/settings.json

2. start airsim simulator:

    cd ~/Downloads/Airsim/${MAP_NAME}/LinuxNoEditor && ./${MAP_NAME}.sh

3. start px4 simulation:

    cd ~/Downloads/Airsim/AirSim/PX4/PX4-Autopilot && make px4_sitl_default none_iris

4. start mavros for airsim.

    roslaunch mavros px4_airsim.launch

5. start airsim sensor msgs publisher.

    cd ~/Downloads/Airsim/AirSim/ros && source devel/setup.bash && roslaunch airsim_sensors airsim_sensors.launch

6. (optional) start QGroundControl.




If you wanna use airsim node:

    cd ~/Downloads/Airsim/AirSim/ros && catkin build -DCMAKE_C_COMPILER=gcc-8 -DCMAKE_CXX_COMPILER=g++-8
    roslaunch airsim_ros_pkgs airsim_node.launch 

You can also run:

    ./scripts/run_airsim.sh

and stop it with:

    ./scripts/stop_airsim.sh