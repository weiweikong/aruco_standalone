ArUco Marker Detection
======================

**ArUco**

ArUco markers are easy to detect pattern grids that yield up to 1024 different patterns. They were built for augmented reality and later used for camera calibration. Since the grid uniquely orients the square, the detection algorithm can determing the pose of the grid.

**ChArUco**

ArUco markers were improved by interspersing them inside a checkerboard called ChArUco. Checkerboard corner intersectionsa provide more stable corners because the edge location bias on one square is countered by the opposite edge orientation in the connecting square. By interspersing ArUco markers inside the checkerboard, each checkerboard corner gets a label which enables it to be used in complex calibration or pose scenarios where you cannot see all the corners of the checkerboard.

The smallest ChArUco board is 5 checkers and 4 markers called a "Diamond Marker".

Status
=================
- CMakeLists only generate `create_marker.cpp` to create different kinds of tag.
- For example
```
./create_marker -d=16 --id=26 --ms=400 --bb=2
```

Modify CMakelists.txt for Specific OpenCV Version
==================
- Current compile version is based on OpenCV 3.1.0 which should be installed.
- Set `OpenCV_DIR` when there are different OpenCV version. This folder should include `OpenCVConfig.cmake.` 
```
set(OpenCV_DIR "/home/amax/Workspace/12.opencv_contrib/opencv/opencv3.0/share/OpenCV")
```
- Set the exact opencv version.
    - 如果没有准确的3.1.0版本，执行`cmake ..`时会报错
    - 系统会列出来当前找到的OpenCV版本和`OpenCVConfig.cmake`文件所在
```
find_package(OpenCV 3.1.0 EXACT REQUIRED)
```
   
- For `include_directories`，add `${OpenCV_INCLUDE_DIRS}`
```
include_directories(
  ${OpenCV_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
  ${PCL_INCLUDE_DIRS}
)
```
- For `link_directories`, add `${OpenCV_LIBRARY_DIRS}`
```
link_directories(
  ${OpenCV_LIBRARY_DIRS}
  ${PCL_LIBRARY_DIRS}
)
```
- For `target_link_libraries`, add `${OpenCV_LIBRARIES}`
```
target_link_libraries(cloudbased_costmap_generator
  ${OpenCV_LIBRARIES}
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
)
```
- `OpenCVConcifg.cmake` introduce the more standard rules and different variables 
```
#  Usage from an external project:
#    In your CMakeLists.txt, add these lines:
#
#    find_package(OpenCV REQUIRED)
#    include_directories(${OpenCV_INCLUDE_DIRS}) # Not needed for CMake >= 2.8.11
#    target_link_libraries(MY_TARGET_NAME ${OpenCV_LIBS})
#
#    Or you can search for specific OpenCV modules:
#
#    find_package(OpenCV REQUIRED core videoio)
#
#    If the module is found then OPENCV_<MODULE>_FOUND is set to TRUE.
#
#    This file will define the following variables:
#      - OpenCV_LIBS                     : The list of all imported targets for OpenCV modules.
#      - OpenCV_INCLUDE_DIRS             : The OpenCV include directories.
#      - OpenCV_COMPUTE_CAPABILITIES     : The version of compute capability.
#      - OpenCV_ANDROID_NATIVE_API_LEVEL : Minimum required level of Android API.
#      - OpenCV_VERSION                  : The version of this OpenCV build: "3.1.0"
#      - OpenCV_VERSION_MAJOR            : Major version part of OpenCV_VERSION: "3"
#      - OpenCV_VERSION_MINOR            : Minor version part of OpenCV_VERSION: "1"
#      - OpenCV_VERSION_PATCH            : Patch version part of OpenCV_VERSION: "0"
#      - OpenCV_VERSION_STATUS           : Development status of this build: ""
#
#    Advanced variables:
#      - OpenCV_SHARED                   : Use OpenCV as shared library
#      - OpenCV_CONFIG_PATH              : Path to this OpenCVConfig.cmake
#      - OpenCV_INSTALL_PATH             : OpenCV location (not set on Windows)
#      - OpenCV_LIB_COMPONENTS           : Present OpenCV modules list
#      - OpenCV_USE_MANGLED_PATHS        : Mangled OpenCV path flag
#      - OpenCV_MODULES_SUFFIX           : The suffix for OpenCVModules-XXX.cmake file
```

TODO
=============
- Compile Other Application