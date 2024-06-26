cmake_minimum_required(VERSION 3.10)
project(Finalysis)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g -O0")

# Add include directories
include_directories(include include/json include/dlib include/cpprest include/cpp-httplib)

# Add executable
add_executable(Finalysis
    src/main.cpp
    src/base64.cpp
    src/base64.h
    src/common_utils.cpp
    src/common_utils.h
    src/data_fetcher.cpp
    src/data_fetcher.h
    src/data_processor.cpp
    src/data_processor.h
    src/trend_analyzer.cpp
    src/trend_analyzer.h
    src/risk_assessor.cpp
    src/risk_assessor.h
    src/aylien_data.cpp
    src/aylien_data.h
    src/httplib.h
)

# Set OpenMP flags
set(OpenMP_C_FLAGS "-Xpreprocessor -fopenmp")
set(OpenMP_CXX_FLAGS "-Xpreprocessor -fopenmp")
set(OpenMP_C_LIB_NAMES "omp")
set(OpenMP_CXX_LIB_NAMES "omp")
set(OpenMP_omp_LIBRARY "/opt/homebrew/opt/llvm/lib/libomp.dylib")

# Find OpenMP
find_package(OpenMP REQUIRED)
if (OpenMP_CXX_FOUND)
    target_link_libraries(Finalysis OpenMP::OpenMP_CXX)
endif()

# Link required libraries
find_package(CURL REQUIRED)
target_link_libraries(Finalysis CURL::libcurl)

# Find and link Dlib
find_package(dlib REQUIRED)
target_link_libraries(Finalysis dlib::dlib)