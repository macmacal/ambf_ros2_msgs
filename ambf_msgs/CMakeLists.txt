cmake_minimum_required(VERSION 3.8)
project(ambf_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)

set(msg_files
  "msg/ActuatorCmd.msg"
  "msg/ActuatorState.msg"
  "msg/CameraCmd.msg"
  "msg/CameraState.msg"
  "msg/LightCmd.msg"
  "msg/LightState.msg"
  "msg/ObjectCmd.msg"
  "msg/ObjectState.msg"
  "msg/RigidBodyCmd.msg"
  "msg/RigidBodyState.msg"
  "msg/SensorCmd.msg"
  "msg/SensorState.msg"
  "msg/SoftBodyCmd.msg"
  "msg/SoftBodyState.msg"
  "msg/VehicleCmd.msg"
  "msg/VehicleState.msg"
  "msg/WorldCmd.msg"
  "msg/WorldState.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  DEPENDENCIES builtin_interfaces geometry_msgs std_msgs
  ADD_LINTER_TESTS
)

install(
  FILES mapping_rules.yaml
  DESTINATION share/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_export_dependencies(rosidl_default_runtime)

ament_package()
