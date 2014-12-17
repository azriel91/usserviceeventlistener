# This CMakeLists.txt file helps defining your block building and compiling
# Include the main biicode macros and functions
# To learn more about the CMake use with biicode, visit http://docs.biicode.com/c++/building.html

project(usServiceEventListener)

cmake_minimum_required(VERSION 2.8)

include(${CMAKE_HOME_DIRECTORY}/biicode.cmake)

# Initializes block variables
INIT_BIICODE_BLOCK()

set(BII_CREATE_LIB True)
set(BII_LIB_TYPE SHARED)
set(BII_LIB_SRC ServiceEventListenerActivator.cpp)
set(BII_LIB_DEPS azriel_cppmicroservices)

usFunctionGenerateModuleInit(BII_LIB_SRC MODULE_NAME usServiceEventListener)

# Actually create targets: EXEcutables and libraries.
ADD_BIICODE_TARGETS()

set_property(TARGET azriel_usserviceeventlistener APPEND PROPERTY COMPILE_DEFINITIONS US_MODULE_NAME=usServiceEventListener)

# link libraries for the CppMicroServices lib
set(US_LINK_LIBRARIES )
if(UNIX)
  list(APPEND US_LINK_LIBRARIES dl)
endif()

if(US_LINK_LIBRARIES)
  target_link_libraries(${BII_test_main_TARGET} ${US_LINK_LIBRARIES})
endif()

add_subdirectory(test)
