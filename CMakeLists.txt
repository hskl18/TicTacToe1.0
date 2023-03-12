cmake_minimum_required(VERSION 3.24)
project(ttt)

#. . . . . . . . . . . . . . . . . . . .
include(GNUInstallDirs)
if(MSVC)
    add_compile_options(/W4)
    add_link_options(/W4)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin)
else()
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
endif()


# place binaries and libraries according to GNU standards
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})



if(CMAKE_CXX_COMPILER_ID MATCHES GNU)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fprofile-arcs -ftest-coverage")
endif()
#. . . . . . . . . . . . . . . . . . . .

# ------------------------------------

set(CMAKE_CXX_STANDARD 17)

set(SOURCE_FILES main.cpp)
add_executable(ttt
        main.cpp
        includes/config/config.cpp
        includes/config/config.h
        includes/button/button.cpp
        includes/button/button.h)

include_directories(/usr/local/include)

find_package(SFML 2.5 COMPONENTS system window graphics network audio REQUIRED)

include_directories(${SFML_INCLUDE_DIRS})

target_link_libraries(ttt sfml-system sfml-window sfml-graphics sfml-audio sfml-network)