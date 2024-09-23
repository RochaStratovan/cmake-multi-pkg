cmake_minimum_required(VERSION 3.23)


set(TARGET test)
project(${TARGET} LANGUAGES CXX)

add_executable(${TARGET})

set(SRC test.cpp)

target_sources(${TARGET} PRIVATE  ${SRC})

target_include_directories(${TARGET}
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
    $<INSTALL_INTERFACE:include>
    )


set(PACKAGE_HINT_PATH "${CMAKE_CURRENT_LIST_DIR}/../INSTALL/foo")
list(APPEND  CMAKE_PREFIX_PATH "${PACKAGE_HINT_PATH}")
find_package(foo REQUIRED)

target_link_libraries(${TARGET} PRIVATE foo)


set(PACKAGE_HINT_PATH "${CMAKE_CURRENT_LIST_DIR}/../INSTALL/bar")
list(APPEND  CMAKE_PREFIX_PATH "${PACKAGE_HINT_PATH}")
find_package(bar REQUIRED)

target_link_libraries(${TARGET} PRIVATE bar)
