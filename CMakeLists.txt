cmake_minimum_required(VERSION 3.9)
project(stb C)

file(GLOB STB_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c)
file(GLOB STB_INCLUDES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
add_library(stb.stb STATIC ${STB_SOURCES})
target_include_directories(stb.stb PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/stb>)
set_target_properties(stb.stb PROPERTIES OUTPUT_NAME stb EXPORT_NAME stb)
add_library(stb::stb ALIAS stb.stb)

install(
    FILES ${STB_INCLUDES}
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/stb)
install(
    TARGETS stb.stb
    EXPORT stb
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    FRAMEWORK DESTINATION Library/Frameworks)
install(EXPORT stb
    NAMESPACE stb::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/stb
    FILE stb.cmake)
