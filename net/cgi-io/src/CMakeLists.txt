cmake_minimum_required(VERSION 2.6)

PROJECT(cgi-io C)

INCLUDE(CheckFunctionExists)

FIND_PATH(ubus_include_dir libubus.h)
FIND_LIBRARY(ubox NAMES ubox)
FIND_LIBRARY(ubus NAMES ubus)
INCLUDE_DIRECTORIES(${ubus_include_dir})

ADD_DEFINITIONS(-Os -Wall -Werror -Wextra --std=gnu99 -g3)
ADD_DEFINITIONS(-Wno-unused-parameter -Wmissing-declarations)

SET(CMAKE_SHARED_LIBRARY_LINK_C_FLAGS "")

IF(APPLE)
  INCLUDE_DIRECTORIES(/opt/local/include)
  LINK_DIRECTORIES(/opt/local/lib)
ENDIF()

ADD_EXECUTABLE(cgi-io main.c multipart_parser.c)
TARGET_LINK_LIBRARIES(cgi-io ${ubox} ${ubus})

INSTALL(TARGETS cgi-io RUNTIME DESTINATION sbin)
