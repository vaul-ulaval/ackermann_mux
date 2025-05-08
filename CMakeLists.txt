cmake_minimum_required(VERSION 3.5)

project(ackermann_mux)

if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake_auto REQUIRED)

ament_auto_find_build_dependencies()

include_directories(include)

ament_auto_add_library(${PROJECT_NAME} SHARED
  src/ackermann_mux.cpp
  src/ackermann_mux_diagnostics.cpp
)

rclcpp_components_register_node(${PROJECT_NAME}
  PLUGIN ackermann_mux::AckermannMux
  EXECUTABLE ackermann_mux_node
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_export_include_directories(include)

ament_auto_package( 
  INSTALL_TO_SHARE
    launch
    config
)