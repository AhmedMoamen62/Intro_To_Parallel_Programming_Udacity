############################################################################
# <summary> CMakeLists.txt for OpenCV and CUDA. </summary>
# <date>    2012-02-07          </date>
# <author>  Quan Tran Minh. edit by Johannes Kast, Michael Sarahan </author>
# <email>   quantm@unist.ac.kr  kast.jo@googlemail.com msarahan@gmail.com</email>
############################################################################

cmake_minimum_required(VERSION 3.1)
project(Intro_To_Parallel_Programming_Udacity LANGUAGES CXX CUDA)

find_package(OpenCV REQUIRED)
find_package(CUDA REQUIRED)

link_directories(${CMAKE_BINARY_DIR}/bin)
target_link_libraries(Intro_To_Parallel_Programming_Udacity ${OpenCV_LIBS})

set (EXECUTABLE_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/bin/")

if(CUDA_FOUND)
  # compared to class settings, we let NVidia's FindCUDA CMake detect 
  # whether to build x64.  We tell it to support most devices, though, 
  # to make sure more people can easily run class code without knowing 
  # about this compiler argument
  set(CUDA_NVCC_FLAGS "
    -gencode;arch=compute_52,code=sm_52;")


  # add debugging to CUDA NVCC flags.  For NVidia's NSight tools.
  set(CUDA_NVCC_FLAGS_DEBUG ${CUDA_NVCC_FLAGS_DEBUG} "-G")

  add_subdirectory (ProblemSet1-RGB2Gray)
  add_subdirectory (ProblemSet2-Blur)
  add_subdirectory (ProblemSet3-ToneMapping)
  add_subdirectory (ProblemSet4-RedEyeRemoval)
  add_subdirectory (ProblemSet5-OptimizedHistogram)
  add_subdirectory (ProblemSet6-SeamlessImageCloning)
else(CUDA_FOUND)
  message("CUDA is not installed on this system.")
endif()
