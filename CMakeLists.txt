PROJECT (abseil-cpp)

cmake_minimum_required(VERSION 3.1)
set(CMAKE_CXX_STANDARD 11)

add_subdirectory(absl/base)
add_subdirectory(absl/meta)
add_subdirectory(absl/memory)
add_subdirectory(absl/algorithm)
add_subdirectory(absl/container)
