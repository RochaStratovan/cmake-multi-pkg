cmake_minimum_required(VERSION 3.23)


include(CMakePackageConfigHelpers)


set(TARGET bar)

project(${TARGET} LANGUAGES CXX)

add_library(${TARGET})

set(SRC bar1.cpp bar2.cpp)
set(HDR bar1.h   bar2.h)

target_sources(${TARGET}
    PRIVATE ${SRC}

    PUBLIC
    FILE_SET HEADERS
    FILES ${HDR}
    )


set(CMAKE_FILE_BASE "bar")
set(TARGET_CMAKE "${CMAKE_FILE_BASE}Targets.cmake")
set(TARGET_CONFIG "${CMAKE_FILE_BASE}Config.cmake")
    
configure_package_config_file(
    "pkg.cmake.in"
    "${PROJECT_BINARY_DIR}/${TARGET_CONFIG}"
    INSTALL_DESTINATION cmake
    )

install(TARGETS bar
    EXPORT bar_Targets
    LIBRARY DESTINATION  "INSTALL/bar/bin"
    ARCHIVE DESTINATION  "INSTALL/bar/lib"
    RUNTIME DESTINATION  "INSTALL/bar/bin"
    FILE_SET HEADERS DESTINATION "INSTALL/bar/include"
    INCLUDES DESTINATION "INSTALL/bar/include"
    )

install(EXPORT ${TARGET}_Targets
    FILE "${TARGET_CMAKE}"
    DESTINATION "INSTALL/${TARGET}/cmake"
    )

install(EXPORT ${TARGET}_Targets FILE "${TARGET_CMAKE}"
    DESTINATION "INSTALL/${TARGET}/cmake")

install(FILES "${PROJECT_BINARY_DIR}/${TARGET_CONFIG}"
    DESTINATION "INSTALL/${TARGET}/cmake")
