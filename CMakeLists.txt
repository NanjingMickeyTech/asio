cmake_minimum_required(VERSION 3.22.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Declares the project name. The project name can be accessed via ${ PROJECT_NAME},
# Since this is the top level CMakeLists.txt, the project name is also accessible
# with ${CMAKE_PROJECT_NAME} (both CMake variables are in-sync within the top level
# build script scope).
project(asio)

add_library(asio STATIC asio/src/asio.cpp)
add_library(asio::asio ALIAS asio)
target_include_directories(
        asio PUBLIC asio/include
)
target_compile_definitions(
        asio PUBLIC -DASIO_STANDALONE -DASIO_SEPARATE_COMPILATION -DASIO_NO_DEPRECATED
)

find_package(Threads)
target_link_libraries(asio PRIVATE Threads::Threads)

