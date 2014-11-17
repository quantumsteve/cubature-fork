project(cubature)

cmake_minimum_required (VERSION 2.6)
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
set(CMAKE_MACOSX_RPATH FALSE)

set(CUBATURE_VERSION_MAJOR "1")
set(CUBATURE_VERSION_MINOR "0")
set(CUBATURE_VERSION_PATCH "2")
set(CUBATURE_VERSION "${CUBATURE_VERSION_MAJOR}.${CUBATURE_VERSION_MINOR}.${CUBATURE_VERSION_PATCH}")

IF(NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE Release CACHE STRING
      "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel."
      FORCE)
ENDIF(NOT CMAKE_BUILD_TYPE)

option(BUILD_TESTING "Build unit tests" OFF)

if(BUILD_TESTING)
endif(BUILD_TESTING)

set(CUBATURE_SRCS hcubature.c pcubature.c)
SOURCE_GROUP("Source Files" FILES ${CUBATURE_SRCS})

set(CUBATURE_HDRS clencurt.h converged.h cubature.h vwrapper.h)
SOURCE_GROUP("Header Files" FILES ${CUBATURE_HDRS})

include_directories(include)

add_library(cubature SHARED ${CUBATURE_SRCS} ${CUBATURE_HDRS})

install(FILES ${CUBATURE_HDRS} DESTINATION include/cubature)
install(TARGETS cubature LIBRARY DESTINATION lib)

if(BUILD_TESTING)
    enable_testing()
    add_subdirectory(test)
endif (BUILD_TESTING)
