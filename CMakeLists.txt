project(stomp)
cmake_minimum_required(VERSION 3.10)

find_package(Qt6 COMPONENTS Core Widgets  Network Test WebSockets )
add_subdirectory(stomp)
add_subdirectory(stomptests)
