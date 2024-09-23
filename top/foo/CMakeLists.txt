cmake_minimum_required(VERSION 3.23)


include(CMakePackageConfigHelpers)


set(TARGET foo)

project(${TARGET} LANGUAGES CXX)

add_library(${TARGET})

set(SRC foo1.cpp foo2.cpp)
set(HDR foo1.h   foo2.h)

target_sources(${TARGET}
    PRIVATE ${SRC}

    PUBLIC
    FILE_SET HEADERS
    FILES ${HDR}
    )


# Logic for generating the relocatable package file using 
set(CMAKE_FILE_BASE "foo")
set(TARGET_CMAKE "${CMAKE_FILE_BASE}Targets.cmake")
set(TARGET_CONFIG "${CMAKE_FILE_BASE}Config.cmake")
    
configure_package_config_file(
    "pkg.cmake.in"
    "${PROJECT_BINARY_DIR}/${TARGET_CONFIG}"
    INSTALL_DESTINATION cmake
    )

install(TARGETS foo
    EXPORT foo_Targets
    LIBRARY DESTINATION  "INSTALL/foo/bin"
    ARCHIVE DESTINATION  "INSTALL/foo/lib"
    RUNTIME DESTINATION  "INSTALL/foo/bin"
    FILE_SET HEADERS DESTINATION "INSTALL/foo/include"
    INCLUDES DESTINATION "INSTALL/foo/include"
    )

install(EXPORT ${TARGET}_Targets
    FILE "${TARGET_CMAKE}"
    DESTINATION "INSTALL/${TARGET}/cmake"
    )

install(EXPORT ${TARGET}_Targets FILE "${TARGET_CMAKE}"
    DESTINATION "INSTALL/${TARGET}/cmake")

install(FILES "${PROJECT_BINARY_DIR}/${TARGET_CONFIG}"
    DESTINATION "INSTALL/${TARGET}/cmake")
