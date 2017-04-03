cmake_minimum_required(VERSION 3.2)
project(clpathtracer)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (CMAKE_CXX_COMPILER_ID STREQUAL "AppleClang")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated-declarations")
endif()

include(FindPkgConfig)

find_package(OpenGL)
find_package(OpenCL REQUIRED)
find_package(GLUT)
find_package(GLEW REQUIRED)

include_directories(${GLEW_INCLUDE_DIRS}
    ${OPENCL_INCLUDE_DIRS}
)

add_executable(clpathtracer
    gl_interop.h
    main.cpp
    )

target_link_libraries(clpathtracer
    ${GLEW_LIBRARIES}
    ${GLUT_LIBRARIES}
    ${OpenCL_LIBRARIES}
    ${OPENGL_gl_LIBRARY}
    ${OPENGL_glu_LIBRARY}
    )

set_target_properties(clpathtracer PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY_DEBUG   ${CMAKE_CURRENT_BINARY_DIR}
    RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_CURRENT_BINARY_DIR}
 )
