cmake_minimum_required(VERSION 2.6)

project(echo CXX)

set(MUDUO_PATH "./lib")
message(STATUS ${MUDUO_PATH})

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

find_path(Muduo_INCLUDE_DIR muduo "${MUDUO_PATH}/include")
find_path(Muduo_LIBRARY_DIR libmuduo_net.a "${MUDUO_PATH}/lib")
message(STATUS ${Muduo_INCLUDE_DIR})
message(STATUS ${Muduo_LIBRARY_DIR})

include_directories(${Muduo_INCLUDE_DIR})
find_library(muduo_base libmuduo_base.a ${Muduo_LIBRARY_DIR})
find_library(muduo_net libmuduo_net.a ${Muduo_LIBRARY_DIR})
message(STATUS ${muduo_base})
message(STATUS ${muduo_net})

include_directories(${PROJECT_SOURCE_DIR})

add_executable(echo ./src/echo.cc)
target_link_libraries(echo ${muduo_net})
target_link_libraries(echo ${muduo_base})
target_link_libraries(echo pthread rt)


