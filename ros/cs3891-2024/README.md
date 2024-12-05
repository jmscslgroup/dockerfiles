# Running Docker with your Generated Code

## Build the Docker Image

```
docker build -t cs3891:barebones .
```

## Visit the source/data folder on your host machine 

```
cd workdir
mkdir -p src
cd src
git clone [your ros repositories]
cd ..
cp ../somewhere/else/somebagfile.bag mytest.bag
```

Some useful repositories are at. Git repositories useful for looking at and using the simulation tools:

* https://github.com/jmscslgroup/cs3891proj2023
* https://github.com/jmscslgroup/subtractor
* https://github.com/jmscslgroup/odometer
* https://github.com/jmscslgroup/profproject
* https://github.com/jmscslgroup/carsimplesimulink

## Launch docker and extract your simulink code

```
docker run --mount type=bind,source=.,target=/ros/catkin_ws -it cs3891:barebones
```

Now, inside of your docker container, compile your Ros catkin workspace. Your cwd should be `/ros/catkin_ws`

```
catkin_make
```

On your computer, extract the .tgz file you received from your generated simulink code in workdir/src. You should have then (on your computer) `workdir/src/simulinkprojectname/(files)`

In your Docker container, you should see `/ros/catkin_ws/simulinkprojectname/(files)`, if your drive mappings worked correctly. My gzipped output file is called `profspacegap.tgz`

Now if you recompile your catkin workspace:

```
catkin_make
[ 87%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/profspacegap_data.cpp.o
[ 87%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/slros_generic_param.cpp.o
[ 87%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/profspacegap.cpp.o
[ 93%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/main.cpp.o
[ 93%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/slros_busmsg_conversion.cpp.o
[ 96%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/rosnodeinterface.cpp.o
[ 96%] Building CXX object profspacegap/CMakeFiles/profspacegap.dir/src/slros_initialize.cpp.o
[100%] Linking CXX executable /ros/catkin_ws/devel/lib/profspacegap/profspacegap
/usr/bin/c++  -O3 -DNDEBUG   CMakeFiles/profspacegap.dir/src/slros_generic_param.cpp.o CMakeFiles/profspacegap.dir/src/main.cpp.o CMakeFiles/profspacegap.dir/src/profspacegap.cpp.o CMakeFiles/profspacegap.dir/src/profspacegap_data.cpp.o CMakeFiles/profspacegap.dir/src/rosnodeinterface.cpp.o CMakeFiles/profspacegap.dir/src/slros_busmsg_conversion.cpp.o CMakeFiles/profspacegap.dir/src/slros_initialize.cpp.o  -o /ros/catkin_ws/devel/lib/profspacegap/profspacegap  -Wl,-rpath,/ros/catkin_ws/install/lib:/opt/ros/noetic/lib /opt/ros/noetic/lib/libroscpp.so /usr/lib/aarch64-linux-gnu/libpthread.so /usr/lib/aarch64-linux-gnu/libboost_chrono.so.1.71.0 /usr/lib/aarch64-linux-gnu/libboost_filesystem.so.1.71.0 /opt/ros/noetic/lib/librosconsole.so /opt/ros/noetic/lib/librosconsole_log4cxx.so /opt/ros/noetic/lib/librosconsole_backend_interface.so /usr/lib/aarch64-linux-gnu/liblog4cxx.so /usr/lib/aarch64-linux-gnu/libboost_regex.so.1.71.0 /opt/ros/noetic/lib/libxmlrpcpp.so /opt/ros/noetic/lib/libroscpp_serialization.so /opt/ros/noetic/lib/librostime.so /usr/lib/aarch64-linux-gnu/libboost_date_time.so.1.71.0 /opt/ros/noetic/lib/libcpp_common.so /usr/lib/aarch64-linux-gnu/libboost_system.so.1.71.0 /usr/lib/aarch64-linux-gnu/libboost_thread.so.1.71.0 /usr/lib/aarch64-linux-gnu/libconsole_bridge.so.0.4 -ldl 
[100%] Built target profspacegap
```

# Create your project package

My project team will be called `cs3891professors`. I'm using the tutorial from http://wiki.ros.org/ROS/Tutorials/CreatingPackage 

In Docker (make sure you are in your `catkin_ws/src` folder)

```
cd /ros/catkin_ws/src
catkin_create_pkg cs3891professors 
```

Inside this folder, create launch/ and then paste in your launchfile:

catkin_make
roslaunch cs3891professors mylaunchfile.launch
