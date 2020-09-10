cmake_minimum_required(VERSION 3.16)

file(GLOB IMGUI_SOURCES
	"${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
	"${CMAKE_CURRENT_SOURCE_DIR}/*.h"
)

if (WIN32)
    file(GLOB IMGUI_PLATFORM_SOURCES
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_dx11.cpp"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_dx11.h"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_win32.cpp"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_win32.h"
	)
elseif (APPLE)
    file(GLOB IMGUI_PLATFORM_SOURCES
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_opengl2.cpp"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_opengl2.h"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_osx.mm"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_osx.h"
	)
elseif (UNIX AND NOT APPLE)
    file(GLOB IMGUI_PLATFORM_SOURCES
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_opengl3.cpp"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_opengl3.h"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_glfw.mm"
    	"${CMAKE_CURRENT_SOURCE_DIR}/examples/imgui_impl_glfw.h"
	)
endif() 

add_library(imgui STATIC ${IMGUI_PLATFORM_SOURCES} ${IMGUI_SOURCES})
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/examples)
target_compile_definitions(imgui PUBLIC IMGUI_IMPL_WIN32_DISABLE_GAMEPAD)