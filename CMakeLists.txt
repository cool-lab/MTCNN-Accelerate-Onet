cmake_minimum_required(VERSION 3.1.0)

project(mtcnn-accelerate)

set(Mtcnn_LINKER_LIBS "")
set(Mtcnn_LINK_DIRS "")
set(Mtcnn_INCLUDE_DIRS "")
set(Mtcnn_DEFINITIONS "")
set(Mtcnn_COMPILE_OPTIONS "")

# Build options
option(USE_OPENMP      "Set to ON to build use openmp"  ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")

# Use C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
message(STATUS "C++11 support has been enabled by default.")

# Use OpenMP
if (USE_OPENMP)
    find_package(OpenMP QUIET)
    if (OPENMP_FOUND)
        message(STATUS "Use OpenMP")
        add_definitions(-DUSE_OPENMP)
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
        set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
    endif()
endif()


# set src_files
set(src_files mtcnn.cpp)

# try to find opencv
message(STATUS "Try to find OpenCV package.")
find_package(OpenCV REQUIRED)

if (NOT OpenCV_FOUND)
    message(SEND_ERROR "OpenCV not found. Project will not be built.")
endif()

if (NOT CMAKE_HOST_WIN32)
	message(STATUS "Try to find Caffe package.")
	message(SEND_ERROR "Please set CAFFE_DIR in the CMakelist.txt and comment this line.")
	set(CAFFE_DIR "/opt/caffe")
	message(STATUS "CAFFE_DIR: ${CAFFE_DIR}")
	find_path(Caffe_INCLUDE_DIRS NAMES caffe/caffe.hpp caffe/common.hpp caffe/net.hpp caffe/proto/caffe.pb.h caffe/util/io.hpp caffe/vision_layers.hpp
	HINTS ${CAFFE_DIR}/include)
	list(APPEND Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include)
	list(APPEND Caffe_INCLUDE_DIRS "/usr/local/cuda-8.0/include")
	message(STATUS "Caffe_INCLUDE_DIRS: ${Caffe_INCLUDE_DIRS}")
	include_directories(${Caffe_INCLUDE_DIRS})
	
	find_package(Caffe REQUIRED)
	if (NOT Caffe_FOUND)
		message(SEND_ERROR "Caffe not found. Project will not be built.")
	endif()
	list(APPEND Mtcnn_LINKER_LIBS PUBLIC ${Caffe_LIBRARIES})

else()
	# set Caffe dirs
	set(Caffe_DEP_INCLUDE_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/include")
	set(Caffe_DEP_LIB_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/lib")
	set(Caffe_DEP_LIBS "")
	#link_directories(${Caffe_DEP_LIB_DIRS})

	set(Caffe_INCLUDE_DIRS "C:/zyf/github/caffe/include; C:/zyf/github/caffe/build/include")
	set(Caffe_LIB_DIRS "C:/zyf/github/caffe/build/lib/Release")
	set(Caffe_LIBS "caffe.lib")
	#link_directories(${Caffe_LIB_DIRS})

	set(CUDA_INCLUDE_DIRS "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v8.0/include")

	list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Caffe_INCLUDE_DIRS} ${Caffe_DEP_INCLUDE_DIRS} ${CUDA_INCLUDE_DIRS})
	list(APPEND Mtcnn_LINK_DIRS PUBLIC ${Caffe_DEP_LIB_DIRS} ${Caffe_LIB_DIRS})
	list(APPEND Mtcnn_LINKER_LIBS PUBLIC ${Caffe_LIBRARIES} ${Caffe_DEP_LIBS})
	endif()

# # try to find boost
if (CMAKE_HOST_WIN32)
	set(Boost_INCLUDE_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/include/boost-1_61")
	set(Boost_LIB_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/lib")
	set(Boost_LIBRARIES "")
endif()

# else()
# message(STATUS "Try to find boost package.")
# #find_package(boost)
# find_package(Boost REQUIRED COMPONENTS system thread filesystem)

# if (NOT boost_FOUND)
    # message(SEND_ERROR "boost not found. Project will not be built.")
# endif()
# endif()

list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Boost_INCLUDE_DIRS})
list(APPEND Mtcnn_LINK_DIRS PUBLIC ${Boost_LIB_DIRS})
list(APPEND Mtcnn_DEFINITIONS -DBOOST_ALL_NO_LIB)
list(APPEND Mtcnn_LINKER_LIBS PUBLIC ${Boost_LIBRARIES})

include_directories(${Mtcnn_INCLUDE_DIRS})
link_directories(${Mtcnn_LINK_DIRS})
add_definitions(${Mtcnn_DEFINITIONS})

add_executable(mtcnn ${src_files})
target_link_libraries(mtcnn ${Mtcnn_LINKER_LIBS})
