# The contents of this file have been placed into the public domain; see the
# file COPYING for more details.

cmake_minimum_required (VERSION 2.6)
project (CppOtp)

# activate C++11 mode
if(CMAKE_COMPILER_IS_GNUCXX)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
endif(CMAKE_COMPILER_IS_GNUCXX)

# Gauche
option(CPPOTP_BUILD_GAUCHE "Build gauche" OFF)

# CPPOTP Library
add_library(cppotp STATIC
	src/libcppotp/bytes.cpp
	src/libcppotp/bytes.h
	src/libcppotp/otp.cpp
	src/libcppotp/otp.h
	src/libcppotp/sha1.cpp
	src/libcppotp/sha1.h
)

target_include_directories(cppotp PUBLIC src/)

# Binary
if(CPPOTP_BUILD_GAUCHE)
	add_executable(gauche
		src/gauche.cpp
	)
	
	target_link_libraries(gauche
		cppotp
	)
endif()
