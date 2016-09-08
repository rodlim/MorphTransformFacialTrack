# I just guess 2.7 will be enough. I'm using the basic of the basic of cmake
cmake_minimum_required(VERSION 2.7)
project(TG1_Face_Tracker_with_obj)

# c++ 11 for 'auto' keyword
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${TG1_Face_Tracker_with_obj_SOURCE_DIR}/cmake")

include_directories(common-sdl2)

find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS} )

find_package(GLUT REQUIRED)
include_directories(${GLUT_INCLUDE_DIRS})

find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS} )

# Look up SDL2 and add the include directory to our include path
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIR})

find_package(SDL2_image REQUIRED)
include_directories(${SDL2_IMAGE_INCLUDE_DIR})

find_package(SDL2_mixer REQUIRED)
include_directories(${SDLMIXER_INCLUDE_DIR})

find_package(SDL2_ttf REQUIRED)
include_directories(${SDL2_TTF_INCLUDE_DIR})

find_package(SDL2GFX REQUIRED)
include_directories(${SDL2GFX_INCLUDE_DIR})

include_directories(/home/rodrigo/opencv-2.4_location/include)
include_directories(/home/rodrigo/face-analysis-sdk-master/src)
include_directories(/home/rodrigo/face-analysis-sdk-master/build/src)


# path to your build/lib dir instalation of CSIRU face analysis sdk here:
set(FACE_ANALYSIS_LIB /home/rodrigo/face-analysis-sdk-master/build/lib)
# path to your opencv 2.4.13 intalation lib dir here
set(OPENCV24_LIB /home/rodrigo/opencv-2.4_location/lib)

set(SOURCE_FILES main.cpp common-sdl2/shader_utils.cpp)
add_executable(TG1_Face_Tracker_with_obj ${SOURCE_FILES})
# link everything we need from CSIRO libs and opencv 2.4.13 libs
target_link_libraries(TG1_Face_Tracker_with_obj ${FACE_ANALYSIS_LIB}/libutilities.so ${FACE_ANALYSIS_LIB}/libclmTracker.so ${FACE_ANALYSIS_LIB}/libavatarAnim.so ${OPENCV24_LIB}/libopencv_core.so ${OPENCV24_LIB}/libopencv_highgui.so ${OPENCV24_LIB}/libopencv_imgproc.so ${OPENCV24_LIB}/libopencv_objdetect.so ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} ${GLEW_LIBRARIES} ${SDL2_LIBRARY})

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -pedantic -std=c++11 -I/usr/include/SDL2 -D_REENTRANT")
#
## this will help find STL when bulding