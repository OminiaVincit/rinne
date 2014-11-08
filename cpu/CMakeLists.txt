cmake_minimum_required (VERSION 3.0)
project (rinne)

IF(NOT ${CMAKE_SYSTEM_NAME} MATCHES "FreeBSD")
  set(LIBS resolv)
ENDIF(NOT ${CMAKE_SYSTEM_NAME} MATCHES "FreeBSD")

set(CMAKE_CXX_FLAGS_DEBUG "-g -O0")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

IF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
  set(CMAKE_CXX_FLAGS "-Wall -framework GLUT -framework OpenGL")
ELSE(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
  set(CMAKE_CXX_FLAGS "-Wall")
  set(LIBS glut GL GLU)
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

set(CMAKE_CXX_FLAGS_DEBUG "-g -O0")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

find_package(Boost COMPONENTS thread system graph REQUIRED)

set(LIBS ${Boost_THREAD_LIBRARY} ${Boost_SYSTEM_LIBRARY} ${Boost_GRAPH_LIBRARY} pcap pthread)

add_executable(rinne rinne.cpp)
target_link_libraries(rinne ${LIBS})