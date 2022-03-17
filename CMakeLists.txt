cmake_minimum_required(VERSION 3.5)
project(detect_test)
set(CMAKE_CXX_STANDARD 11)
add_executable(${PROJECT_NAME} main.cpp)


# fmt
find_package(fmt REQUIRED)
target_link_libraries(${PROJECT_NAME} 
                        PRIVATE 
                        fmt::fmt
                        )
#opencv
find_package(OpenCV REQUIRED)
target_link_libraries(${PROJECT_NAME}  
                        PRIVATE 
                        ${OpenCV_LIBS}
                        )
#Camera
add_library(MVSDK SHARED IMPORTED)
add_library(Camera devices/camera/mv_video_capture.cpp)
set(MIMDVISION_SDK_LIBRARY /lib/libMVSDK.so)
set_property(TARGET MVSDK PROPERTY IMPORTED_LOCATION ${MIMDVISION_SDK_LIBRARY})
target_link_libraries(${PROJECT_NAME}  
                                PRIVATE 
                                Camera 
                                MVSDK
                                )
