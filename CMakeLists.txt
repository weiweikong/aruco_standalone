#set(the_description "ArUco Marker Detection")
#ocv_define_module(aruco opencv_core opencv_imgproc opencv_calib3d WRAP python)

cmake_minimum_required(VERSION 2.8)

set(OpenCV_DIR "/home/amax/Workspace/12.opencv_contrib/opencv/opencv3.0/share/OpenCV")
				         
project( ArucoTag )



find_package( OpenCV 3.1.0 EXACT REQUIRED)
#add_executable( DisplayImage DisplayImage.cpp )
#target_link_libraries( DisplayImage ${OpenCV_LIBS} )


set(NAME_SRC
    include/opencv2/aruco.hpp
    include/opencv2/aruco/dictionary.hpp
    src/aruco.cpp
    src/dictionary.cpp
    src/precomp.hpp
    src/predefined_dictionaries.hpp
    samples/create_marker.cpp
)

#add_library(aruco SHARED $(NAME_SRC))

#set(OpenCV_DIR "~/Workspace/12.opencv_contrib/opencv/opencv3.0")

include_directories(include ${OpenCV_INCLUDE_DIRS})
#link_directories(${OpenCV_DIR}/lib)

add_executable(create_marker ${NAME_SRC})

target_link_libraries(create_marker ${OpenCV_LIBS})

MESSAGE ( STATUS "Message Found OpenCV: ${OpenCV_DIR}")
