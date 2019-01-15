cmake_minimum_required(VERSION 3.8)
project (hello)

add_executable(hello helloworld.cpp)

project(testingPack)
find_program(OSX_PACKAGE_GENERATOR productbuild)
if (OSX_PACKAGE_GENERATOR)
    message(STATUS "package generator: productbuild")
    set(CPACK_GENERATOR productbuild)
else()
    message(STATUS "!!! Missing package generator")
endif()

set(CPACK_COMPONENT_TS_DISPLAY_NAME "testingPack")
install(PROGRAMS ${CMAKE_BINARY_DIR}/hello
        DESTINATION "/var/local/hello"
        COMPONENT TS
      )

install(PROGRAMS com.hello.world.plist
        DESTINATION "/Library/LaunchDaemons/"
        COMPONENT TS
      )

include(CPack)

add_custom_target(cpack-force-osx ALL
        COMMAND echo 'CPack OSX')
