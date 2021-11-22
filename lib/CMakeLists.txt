project(VHACD)
option(NO_OPENCL "NO_OPENCL" ON)
option(NO_OPENMP "NO_OPENMP" ON)

message("NO_OPENCL " ${NO_OPENCL})
message("NO_OPENMP " ${NO_OPENMP})

set(CMAKE_COMMON_INC "${CMAKE_SOURCE_DIR}/lib/scripts/cmake_common.cmake")
add_subdirectory ("${CMAKE_SOURCE_DIR}/lib/VHACD_Lib")

