cmake_minimum_required(VERSION 3.13)
project(app)
set(CMAKE_CXX_STANDARD 20)

add_executable(app "main.cpp")

set(DAWN_FETCH_DEPENDENCIES ON)
add_subdirectory("dawn" EXCLUDE_FROM_ALL)

if(EMSCRIPTEN)
    set_target_properties(app PROPERTIES SUFFIX ".html")
    target_link_libraries(app PRIVATE emdawnwebgpu_cpp)
    target_link_options(app PRIVATE "-sASYNCIFY=1")
else()
    target_link_libraries(app PRIVATE dawn::webgpu_dawn glfw webgpu_glfw)
endif()