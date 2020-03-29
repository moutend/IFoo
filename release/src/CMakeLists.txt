file(GLOB HEADERS "../include/IFoo/*.h")
source_group("Header Files\\Foo" FILES ${HEADERS})

file(GLOB SOURCES "./*.c")
list(APPEND SOURCES ${HEADERS})

add_library(IFoo ${SOURCES})
target_include_directories(IFoo PUBLIC $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>)
