############################################################################
# <summary> CMakeLists.txt for OpenCV and CUDA. </summary>
# <date>    2012-02-07          </date>
# <author>  Quan Tran Minh. edit by Johannes Kast, Michael Sarahan </author>
# <email>   quantm@unist.ac.kr  kast.jo@googlemail.com msarahan@gmail.com</email>
############################################################################

cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(Intro_To_Parallel_Programming_Udacity)

find_package(OpenCV REQUIRED)
find_package(CUDA REQUIRED)

link_libraries(${OpenCV_LIBS})

set (EXECUTABLE_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/bin/")

if(CUDA_FOUND)
  # compared to class settings, we let NVidia's FindCUDA CMake detect 
  # whether to build x64.  We tell it to support most devices, though, 
  # to make sure more people can easily run class code without knowing 
  # about this compiler argument
  set(CUDA_NVCC_FLAGS "
  -gencode;arch=compute_75,code=sm_75;")

  # add debugging to CUDA NVCC flags.  For NVidia's NSight tools.
  set(CUDA_NVCC_FLAGS_DEBUG ${CUDA_NVCC_FLAGS_DEBUG} "-G")

  add_subdirectory(ProblemSet1_RGB2Gray)
  add_subdirectory(ProblemSet2_Blur)
  add_subdirectory(ProblemSet3_ToneMapping)
  add_subdirectory(ProblemSet4_RedEyeRemoval)
  add_subdirectory(ProblemSet5_OptimizedHistogram)
  add_subdirectory(ProblemSet6_SeamlessImageCloning)

else()
  message("CUDA is not installed on this system.")

endif()