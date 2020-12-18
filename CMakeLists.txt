cmake_minimum_required (VERSION 3.10.0 FATAL_ERROR)
project(Nalu-Wind-Test CXX Fortran)

set(CMAKE_CXX_STANDARD 14)       # Set nalu-wind C++14 standard
set(CMAKE_CXX_EXTENSIONS OFF)    # Do not enable GNU extensions
set(CMAKE_CXX_STANDARD_REQUIRED) # Force error if C++14 standard is not supported

find_package(Nalu-Wind REQUIRED)
find_package(Trilinos REQUIRED)
find_package(MPI REQUIRED)

find_package(YAML-CPP 0.6.2 REQUIRED)

include_directories(${NALU_WIND_INCLUDE_DIRS})

message("DIR ${NALU_WIND_INCLUDE_DIRS}")

set(utest_ex_name test)

add_executable(${utest_ex_name} unit_tests.C)
target_link_libraries(${utest_ex_name} PRIVATE nalu ${Trilinos_LIBRARIES} mpi)
target_link_libraries(${utest_ex_name} PUBLIC yaml-cpp)

target_include_directories(${utest_ex_name} PRIVATE ${NALU_WIND_INCLUDE_DIRS} ${NALU_WIND_INCLUDE_DIRS}/include)
target_include_directories(${utest_ex_name} PRIVATE unit_tests)
add_subdirectory(unit_tests)
