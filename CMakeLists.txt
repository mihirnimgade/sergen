cmake_minimum_required(VERSION 3.22.1)

project(sergen VERSION 0.1.0 LANGUAGES C)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fdiagnostics-color=always")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Setting C standard
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 99)

# ==== SERGEN TARGET ====

add_executable(sergen)

target_sources(sergen PRIVATE source/sergen.c)
target_include_directories(
  sergen PRIVATE
  include/
  libs/
  libs/libclang
)
target_compile_options(sergen PRIVATE -g)
target_link_libraries(sergen libclang)

set_target_properties(sergen PROPERTIES INSTALL_RPATH "$ORIGIN")

# ==== LIBRARIES ====

set(LIBCLANG_SO_LOCATION "${PROJECT_SOURCE_DIR}/libs/libclang/libclang.so.18.1")

add_library(libclang SHARED IMPORTED)
set_target_properties(libclang PROPERTIES IMPORTED_LOCATION ${LIBCLANG_SO_LOCATION})
set_target_properties(libclang PROPERTIES IMPORTED_SONAME "libclang.so.18.1")

# ==== INSTALLATION ====

set(BINARY_DESTINATION_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

install(TARGETS sergen DESTINATION ${BINARY_DESTINATION_DIRECTORY})
install(PROGRAMS ${LIBCLANG_SO_LOCATION} DESTINATION ${BINARY_DESTINATION_DIRECTORY})
