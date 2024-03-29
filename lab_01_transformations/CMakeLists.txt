cmake_minimum_required( VERSION 3.5.1 )

project(lab_01_transformations)
set(exe_name lab_01_transformations)

# Find libraries
find_package(Eigen3 REQUIRED)
find_package(OpenCV 4 REQUIRED)

add_executable(${exe_name}
  main.cpp
  )

if (NOT OpenCV_LIBS)
  set(OpenCV_LIBS "opencv::opencv")
endif()

target_link_libraries(${exe_name}
  ${OpenCV_LIBS}
  Eigen3::Eigen
  )

set_target_properties(${exe_name} PROPERTIES
  CXX_STANDARD_REQUIRED ON
  CXX_STANDARD 17
  )
 
file(COPY img_grid.png
  DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/
)

set(gcc_like_cxx "$<COMPILE_LANG_AND_ID:CXX,ARMClang,AppleClang,Clang,GNU,LCC>")
set(msvc_cxx "$<COMPILE_LANG_AND_ID:CXX,MSVC>")

target_compile_options(${exe_name} PRIVATE
  "$<${gcc_like_cxx}:$<BUILD_INTERFACE:-Wall;-Wextra;-Wpedantic;-Wshadow;-Wformat=2>>"
  "$<${msvc_cxx}:$<BUILD_INTERFACE:-W4>>"
  )

target_compile_definitions(${exe_name} PUBLIC
  "$<${msvc_cxx}:-D_USE_MATH_DEFINES>"
  )
