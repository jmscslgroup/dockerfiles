# Running Docker with your Generated Code

## Pull the Docker Image

```
docker pull sprinkjm/rosempty:latest
```

### Optional: Build the Docker Image
If you prefer to build the Docker image from scratch, use the below commands in the same directory as this Dockerfile

```
docker build -t rosempty:latest .
```

### Docker superuser: 
If you ever want to push a docker image to your dockerhub account, you can do:

```
docker built -d dhusername/rosempty:latest .
docker push dhusername/rosempty
```

## Visit the source/data folder on your *host* machine 

```
cd rossim
mkdir -p src
cd src
```


**FIRST TIME ONLY clone some example repositories that will help**

```
git clone https://github.com/jmscslgroup/subtractor
git clone https://github.com/jmscslgroup/odometer
git clone https://github.com/jmscslgroup/carsimplesimulink
git clone https://github.com/jmscslgroup/projproject
cd ..
```
Download the example test bagfile from Brightspace: it will be called `2023_09_28_16_19_25_2T3MWRFVXLW056972microstrain_record.bag`. Once it is downloaded, copy the file in and call it `mytest.bag` in your `rossim` folder
```
cp ../somewhere/else/somebagfile.bag mytest.bag
```

## Launch docker

```
docker run --mount type=bind,source=.,target=/ros/catkin_ws -it cs3892
```

Now, inside of your docker container, compile your Ros catkin workspace. Your cwd should be `/ros/catkin_ws`

```
catkin_make
```

## Extract simulink code to your machine

On your computer, extract the .tgz file you received from your generated simulink code in workdir/src. You should have then (on your computer) `workdir/src/simulinkprojectname/(files)`

In your Docker container, you should see `/ros/catkin_ws/simulinkprojectname/(files)`, if your drive mappings worked correctly. My gzipped output file is called `profspacegap.tgz`

Now if you recompile your catkin workspace (YMMV on percentages):

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


# Useful git repositories for simulation

Learn about these and other useful repositories using the links below.

* https://github.com/jmscslgroup/cs3891proj2023
* https://github.com/jmscslgroup/subtractor
* https://github.com/jmscslgroup/odometer
* https://github.com/jmscslgroup/profproject
* https://github.com/jmscslgroup/carsimplesimulink

