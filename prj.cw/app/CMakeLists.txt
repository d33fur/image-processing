cmake_minimum_required(VERSION 3.27.7)

project(cw LANGUAGES CXX)

add_executable(${PROJECT_NAME} main.cpp)

find_package(raylib QUIET)
if(NOT raylib_FOUND)
    message("raylib not found")
    message("Trying to download raylib...")
    include(FetchContent)
    FetchContent_Declare(
        raylib
        GIT_REPOSITORY https://github.com/raysan5/raylib.git
        GIT_TAG 5.0
        GIT_SHALLOW 1
    )
    FetchContent_MakeAvailable(raylib)
    message("raylib downloaded")
    target_link_libraries(${PROJECT_NAME} PUBLIC raylib)
else()
  message("raylib found")
  target_link_libraries(${PROJECT_NAME} PUBLIC raylib)
endif()

find_package(a2i REQUIRED)
message("a2i found")
find_package(OpenCV REQUIRED)
message("OpenCV found")

include_directories(${OpenCV_INCLUDE_DIRS})

target_link_libraries(${PROJECT_NAME} PUBLIC 
  raylib
  ${OpenCV_LIBS}
  a2i)
