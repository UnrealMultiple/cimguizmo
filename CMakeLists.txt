cmake_minimum_required(VERSION 3.1)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../cimgui ./cimgui)

project(cimguizmo)

#general settings
file(GLOB IMGUI_SOURCES
    ../cimgui/cimgui.h
    ../cimgui/imgui/imgui.h
    cimguizmo.h
	cimguizmo.cpp
    ImGuizmo/GraphEditor.h
    ImGuizmo/ImCurveEdit.h
    ImGuizmo/ImGradient.h
    ImGuizmo/ImGuizmo.h
    ImGuizmo/ImSequencer.h
    ImGuizmo/ImZoomSlider.h
    ImGuizmo/GraphEditor.cpp
    ImGuizmo/ImCurveEdit.cpp
    ImGuizmo/ImGradient.cpp
    ImGuizmo/ImGuizmo.cpp
    ImGuizmo/ImSequencer.cpp
)

set(IMGUI_STATIC "no" CACHE STRING "Build as a static library")
set(CMAKE_CXX_STANDARD 11)

#add library and link
if (IMGUI_STATIC)
    add_library(cimguizmo STATIC ${IMGUI_SOURCES})
else (IMGUI_STATIC)
    add_library(cimguizmo SHARED ${IMGUI_SOURCES})
endif (IMGUI_STATIC)

add_definitions("-DIMGUI_USER_CONFIG=\"../cimconfig.h\"")
target_compile_definitions(cimguizmo PUBLIC IMGUI_DISABLE_OBSOLETE_FUNCTIONS=1)


target_include_directories(cimguizmo PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/ImGuizmo)
target_include_directories(cimguizmo PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../cimgui/imgui)
target_include_directories(cimguizmo PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/../cimgui)
target_link_libraries(cimguizmo PRIVATE cimgui)
set_target_properties(cimguizmo PROPERTIES PREFIX "")

#install
install(TARGETS cimguizmo
    RUNTIME DESTINATION  .
    LIBRARY DESTINATION  .
    ARCHIVE DESTINATION  .
)

