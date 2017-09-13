cmake_minimum_required(VERSION 3.1.0)

project(mtcnn-accelerate)

set(Mtcnn_INCLUDE_DIRS "")
set(Mtcnn_LINK_LIBS "")
set(Mtcnn_LINK_DIRS "")
set(Mtcnn_DEFINITIONS "")
set(Mtcnn_COMPILE_OPTIONS "")

# Build options
option(USE_OPENMP      "Set to ON to build use openmp"  ON)
option(FIND_CAFFE_ON_WINDOWS "Set to On to try to find_package(Caffe) on Windows. It will probably fail, then you need to manually set Caffe's environment." ON)

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
	message(SEND_ERROR "Please set CAFFE_DIR, CAFFE_BUILD_DIR and CUDA_DIR in the CMakelist.txt and comment this line.")
	
	set(CAFFE_DIR "/opt/caffe")
	set(CAFFE_BUILD_DIR "${CAFFE_DIR}/build")
	set(CUDA_DIR "/usr/local/cuda-8.0")
	
	set(CUDA_INCLUDE_DIRS "${CUDA_DIR}/include")
	
	message(STATUS "CAFFE_DIR: ${CAFFE_DIR}")
	message(STATUS "CUDA_DIR: ${CUDA_DIR}")
	message(STATUS "CUDA_INCLUDE_DIRS: ${CUDA_INCLUDE_DIRS}")

	message(STATUS "Try to find Caffe package.")
	# find_path(Caffe_INCLUDE_DIRS NAMES caffe/caffe.hpp caffe/common.hpp caffe/net.hpp caffe/proto/caffe.pb.h caffe/util/io.hpp caffe/vision_layers.hpp
	# HINTS ${CAFFE_DIR}/include)
	# list(APPEND Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include)
	set(Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include ${CAFFE_BUILD_DIR}/include)
	
	#message(STATUS "Caffe_INCLUDE_DIRS: ${Caffe_INCLUDE_DIRS}")
	#include_directories(${Caffe_INCLUDE_DIRS})
	
	find_package(Caffe REQUIRED) # This will also include headers and libs of caffe's dependencies
	if (NOT Caffe_FOUND)
		message(SEND_ERROR "Caffe not found. Project will not be built.")
	endif()

	message(STATUS "Caffe_INCLUDE_DIRS: ${Caffe_INCLUDE_DIRS}")
	message(STATUS "Caffe_LIBRARIES: ${Caffe_LIBRARIES}")
	
	list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Caffe_INCLUDE_DIRS} ${CUDA_INCLUDE_DIRS})
	list(APPEND Mtcnn_LINK_LIBS PUBLIC ${Caffe_LIBRARIES})

else()
	message(STATUS "Try to find Caffe package.")
	message(SEND_ERROR "Please set CAFFE_DIR, CUDA_DIR and Caffe_DEPENDENCIES_DIR in the CMakelist.txt and comment this line.")

	set(CAFFE_DIR "C:/zyf/github/caffe")
	set(CAFFE_BUILD_DIR "${CAFFE_DIR}/build")
	set(CUDA_DIR "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v8.0")
	set(Caffe_DEPENDENCIES_DIR "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries")
	
	include(${Caffe_DEPENDENCIES_DIR}/caffe-builder-config.cmake)
	set(CUDA_INCLUDE_DIRS "${CUDA_DIR}/include")
	
	message(STATUS "CAFFE_DIR: ${CAFFE_DIR}")
	message(STATUS "CUDA_DIR: ${CUDA_DIR}")
	message(STATUS "CUDA_INCLUDE_DIRS: ${CUDA_INCLUDE_DIRS}")

	if (FIND_CAFFE_ON_WINDOWS)
		message(STATUS "Try to find Caffe package. If this failed, please set FIND_CAFFE_ON_WINDOWS off and set Caffe dirs manually.")
		# find_path(Caffe_INCLUDE_DIRS NAMES caffe/caffe.hpp caffe/common.hpp caffe/net.hpp caffe/proto/caffe.pb.h caffe/util/io.hpp caffe/vision_layers.hpp
		# HINTS ${CAFFE_DIR}/include)
		# list(APPEND Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include)
		set(Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include ${CAFFE_BUILD_DIR} ${CAFFE_BUILD_DIR}/include)
		
		#message(STATUS "Caffe_INCLUDE_DIRS: ${Caffe_INCLUDE_DIRS}")
		#include_directories(${Caffe_INCLUDE_DIRS})
		
		find_package(Caffe REQUIRED) # This will also include headers and libs of caffe's dependencies
		if (NOT Caffe_FOUND)
			message(SEND_ERROR "Caffe not found. Project will not be built.")
		endif()

		message(STATUS "Caffe_INCLUDE_DIRS: ${Caffe_INCLUDE_DIRS}")
		message(STATUS "Caffe_LIBRARIES: ${Caffe_LIBRARIES}")
		
		list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Caffe_INCLUDE_DIRS} ${CUDA_INCLUDE_DIRS})
		list(APPEND Mtcnn_LINK_LIBS PUBLIC ${Caffe_LIBRARIES})
				
	else()
		message(SEND_ERROR "Please set {CAFFE, Caffe_DEPENDENCIES, BOOST}_{INCLUDE_DIRS, LIB_DIRS, LIBRARIES} in the CMakelist.txt and comment this line.")
	
		# set Caffe dirs
		set(Caffe_INCLUDE_DIRS ${CAFFE_DIR}/include ${CAFFE_BUILD_DIR} ${CAFFE_BUILD_DIR}/include)
		set(Caffe_LIB_DIRS "${CAFFE_BUILD_DIR}/lib/Release")
		set(Caffe_LIBRARIES "caffe.lib")
		#link_directories(${Caffe_LIB_DIRS})
		
		set(Caffe_DEPENDENCIES_INCLUDE_DIRS "${Caffe_DEPENDENCIES_DIR}/include")
		set(Caffe_DEPENDENCIES_LIB_DIRS "${Caffe_DEPENDENCIES_DIR}/lib")
		set(Caffe_DEPENDENCIES_LIBRARIES "")
		#link_directories(${Caffe_DEPENDENCIES_LIB_DIRS})
		
		list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Caffe_INCLUDE_DIRS} ${Caffe_DEPENDENCIES_INCLUDE_DIRS} ${CUDA_INCLUDE_DIRS})
		list(APPEND Mtcnn_LINK_DIRS PUBLIC ${Caffe_DEPENDENCIES_LIB_DIRS} ${Caffe_LIB_DIRS})
		list(APPEND Mtcnn_LINK_LIBS PUBLIC ${Caffe_LIBRARIES} ${Caffe_DEPENDENCIES_LIBRARIES})
		
		set(Boost_INCLUDE_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/include/boost-1_61")
		set(Boost_LIB_DIRS "C:/Users/zhaoy/.caffe/dependencies/libraries_v140_x64_py27_1.1.0/libraries/lib")
		set(Boost_LIBRARIES "")
		## Boost will be included by find_package(Caffe)
		# message(STATUS "Try to find Boost package.")
		# #find_package(Boost)
		# find_package(Boost REQUIRED COMPONENTS system thread filesystem)

		# if (NOT boost_FOUND)
			# message(SEND_ERROR "boost not found. Project will not be built.")
		# endif()	
		
		list(APPEND Mtcnn_INCLUDE_DIRS PUBLIC ${Boost_INCLUDE_DIRS})
		list(APPEND Mtcnn_LINK_DIRS PUBLIC ${Boost_LIB_DIRS})
		list(APPEND Mtcnn_LINK_LIBS PUBLIC ${Boost_LIBRARIES})
		list(APPEND Mtcnn_DEFINITIONS -DBOOST_ALL_NO_LIB)
	
	endif()
endif()

include_directories(${Mtcnn_INCLUDE_DIRS})
link_directories(${Mtcnn_LINK_DIRS})
add_definitions(${Mtcnn_DEFINITIONS})

add_executable(mtcnn ${src_files})
target_link_libraries(mtcnn ${Mtcnn_LINK_LIBS})
