project(usServiceEventListener)

cmake_minimum_required(VERSION 3.0)

set(BII_LIB_SRC ServiceEventListenerActivator.cpp)
SET(BII_LIB_DEPS ${BII_LIB_DEPS} azriel_cppmicroservices)
set(BII_test_main_SRC test/main.cpp)

usFunctionGenerateModuleInit(BII_LIB_SRC MODULE_NAME usServiceEventListener)

# Actually create targets: executables and libraries.
ADD_BIICODE_TARGETS()

set_property(TARGET ${BII_LIB_TARGET} APPEND PROPERTY COMPILE_DEFINITIONS US_MODULE_NAME=usServiceEventListener)

if(NOT BUILD_SHARED_LIBS)
  target_compile_definitions(${BII_LIB_TARGET} PRIVATE US_STATIC_MODULE)
endif()

if(NOT ${BII_IS_DEP})
  add_subdirectory(test)
endif()
