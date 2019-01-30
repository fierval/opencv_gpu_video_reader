# cmake needs this line
cmake_minimum_required(VERSION 3.8)

set(EXAMPLE_NAME video_reader)
set(EXAMPLE_FILE video_reader.cpp)

file(TO_CMAKE_PATH "${EXAMPLE_FILE}" EXAMPLE_FILE)
message(STATUS "Project: ${EXAMPLE_NAME}")
message(STATUS "File   : ${EXAMPLE_FILE}")

# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)


# Define project name
project(${EXAMPLE_NAME})

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)
find_package(CUDA 9.2 REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS} ${CUDA_INCLUDE_DIRS})

# If the package has been found, several variables will
# be set, you can find the full list with descriptions
# in the OpenCVConfig.cmake file.
# Print some message showing some of them
message(STATUS "OpenCV library status:")
message(STATUS "    config: ${OpenCV_DIR}")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

# Declare the executable target built from your sources
add_executable(${EXAMPLE_NAME} "${EXAMPLE_FILE}" dynlink_nvcuvid.cpp)

# Link your application with OpenCV libraries
target_link_libraries(${EXAMPLE_NAME} ${OpenCV_LIBS} cuda ${CMAKE_DL_LIBS})