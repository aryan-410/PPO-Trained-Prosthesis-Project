cmake_minimum_required(VERSION 3.0.2)
project(xacro-test)

find_package(catkin REQUIRED COMPONENTS xacro)

catkin_package()

## manual usage of eval
xacro_add_xacro_file(../include1.xml manual1.xml)
list(APPEND xacro_outputs ${XACRO_OUTPUT_FILE})

xacro_add_xacro_file(../include2.xml manual2.xml OUTPUT MY_OUTPUT_VAR)
list(APPEND xacro_outputs ${MY_OUTPUT_VAR})

add_custom_target(xacro_target ALL DEPENDS ${xacro_outputs})
xacro_install(xacro_target ${xacro_outputs} DESTINATION xml)

## convenience function
xacro_add_files(TARGET xacro test.xacro REMAP bar:=foo foo:=bar INSTALL)
