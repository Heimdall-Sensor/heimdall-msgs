cmake_minimum_required(VERSION 2.8.3)
project(heimdall_msgs)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS message_generation sensor_msgs)

#######################################
## Declare ROS messages and services ##
#######################################

add_message_files(
    FILES
    PolygonArray.msg
    PolygonArrayStamped.msg
    Activity.msg
    ActivityArray.msg
    ActivityArrayStamped.msg
    Masks.msg
)

## Generate services in the 'srv' folder
add_service_files(
    FILES
    CommandSrv.srv
    AddMaskSrv.srv
    GetMaskSrv.srv
    RemoveMaskListSrv.srv
    GetMaskListSrv.srv
    GenerateMovie.srv
)

## Generate added messages and services with any dependencies listed here
generate_messages(
    DEPENDENCIES
    sensor_msgs
    geometry_msgs
)

# Instead of depending on heimdall_msgs, packages that do this must depend on
# heimdall_msgs_gencpp or heimdall_msgs_genpy to do this. This is, of course, weird
# behavior. An attempt to fix this, currently not working:
add_custom_target(${PROJECT_NAME} DEPENDS ${PROJECT_NAME}_gencpp ${PROJECT_NAME}_genpy)

catkin_package(
    CATKIN_DEPENDS message_runtime sensor_msgs
)

