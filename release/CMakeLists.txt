cmake_minimum_required(VERSION 3.12)
project(IFoo)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR OR EXISTS "${CMAKE_BINARY_DIR}/CMakeLists.txt")
  message(FATAL_ERROR "In-source builds are not allowed.")
endif()

if(NOT WIN32)
  message(FATAL_ERROR "This project targets Windows.")
endif()

execute_process(
  COMMAND midl IFoo.idl
  WORKING_DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/src"
)

file(REMOVE "${CMAKE_CURRENT_LIST_DIR}/src/dlldata.c")
file(GLOB HEADERS "${CMAKE_CURRENT_LIST_DIR}/src/*.h")

foreach(HEADER ${HEADERS})
  file(COPY "${HEADER}" DESTINATION "${CMAKE_CURRENT_LIST_DIR}/include/IFoo")
endforeach()

add_subdirectory(src)
