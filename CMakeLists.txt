cmake_minimum_required(VERSION 3.14)
set(CMAKE_CXX_STANDARD 17)

include(FetchContent)
FetchContent_Declare(
  magnum
  GIT_REPOSITORY https://github.com/mosra/magnum.git
  GIT_TAG        v2020.06
)
FetchContent_Declare(
  corrade
  GIT_REPOSITORY https://github.com/mosra/corrade.git
  GIT_TAG        v2020.06
)
FetchContent_Declare(
    GLFW
  GIT_REPOSITORY https://github.com/glfw/glfw.git
  GIT_TAG        3.3.3
)
set(WITH_GLFWAPPLICATION ON CACHE BOOL "" FORCE) # enable what you need
set(WITH_ANYIMAGEIMPORTER ON CACHE BOOL "" FORCE) # enable what you need

FetchContent_MakeAvailable(GLFW corrade magnum )

project(ArcBallExample)
list(APPEND CMAKE_PREFIX_PATH ${magnum_SOURCE_DIR}/modules ${corrade_SOURCE_DIR}/modules)

find_package(Magnum REQUIRED
    DebugTools
    GL
    MeshTools
    Primitives
    SceneGraph
    Shaders
    GlfwApplication)
add_executable(magnum-arcball WIN32
    ArcBall.cpp
    ArcBallExample.cpp)
target_link_libraries(magnum-arcball PRIVATE
    Corrade::Main
    Magnum::Application
    Magnum::DebugTools
    Magnum::GL
    Magnum::Magnum
    Magnum::MeshTools
    Magnum::Primitives
    Magnum::SceneGraph
    Magnum::Shaders)
