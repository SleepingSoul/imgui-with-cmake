project(imgui-with-cmake)

find_package(SDL2 REQUIRED)

find_package(PkgConfig REQUIRED)
pkg_check_modules(DIRECTFB REQUIRED directfb)

add_library(imgui STATIC)

target_sources(imgui
    PRIVATE
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
    imgui.cpp
    backends/imgui_impl_sdlrenderer2.cpp
    backends/imgui_impl_sdl2.cpp)

set(IMGUI_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(IMGUI_HEADERS
  imgui.h
  imconfig.h
  imgui_internal.h
  imstb_rectpack.h
  imstb_textedit.h
  imstb_truetype.h
  backends/imgui_impl_sdlrenderer2.h
  backends/imgui_impl_sdl2.h)

target_include_directories(imgui
    PUBLIC
    ${IMGUI_INCLUDE_DIR}
    ${SDL2_INCLUDE_DIR}
    ${DIRECTFB_INCLUDE_DIRS})

install(TARGETS imgui DESTINATION ${CMAKE_INSTALL_PREFIX}/lib)
install(FILES ${IMGUI_HEADERS} DESTINATION ${CMAKE_INSTALL_PREFIX}/include)
