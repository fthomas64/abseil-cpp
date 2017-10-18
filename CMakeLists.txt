PROJECT (abseil-cpp)

cmake_minimum_required(VERSION 2.8.12)
set(CMAKE_CXX_STANDARD 11)

add_subdirectory(absl/base)
add_subdirectory(absl/meta)
add_subdirectory(absl/memory)
add_subdirectory(absl/algorithm)
add_subdirectory(absl/container)
add_subdirectory(absl/numeric)
add_subdirectory(absl/strings)
add_subdirectory(absl/utility)


add_subdirectory(examples/string)
