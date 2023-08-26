
cmake_minimum_required(VERSION 3.12)
project(wuvorbis_krkrsdl2)

include(FetchContent)

FetchContent_Declare(
	krkrsdl2-tp_stub
	URL https://github.com/krkrsdl2/krkrsdl2/releases/download/latest/krkrsdl2-tp_stub.tar.gz
)

FetchContent_MakeAvailable(krkrsdl2-tp_stub)

set(WUVORBIS_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(STRINGS ${WUVORBIS_SRC_DIR}/src_list/sources.txt WUVORBIS_SRC)
file(STRINGS ${WUVORBIS_SRC_DIR}/src_list/sources_module.txt WUVORBIS_MODULE_SRC)
file(STRINGS ${WUVORBIS_SRC_DIR}/src_list/includes.txt WUVORBIS_INCLUDES)
file(STRINGS ${WUVORBIS_SRC_DIR}/src_list/includes_module.txt WUVORBIS_MODULE_INCLUDES)
list(APPEND WUVORBIS_SRC ${WUVORBIS_MODULE_SRC})
list(TRANSFORM WUVORBIS_SRC PREPEND ${WUVORBIS_SRC_DIR}/)
list(APPEND WUVORBIS_INCLUDES ${WUVORBIS_MODULE_INCLUDES})
list(TRANSFORM WUVORBIS_INCLUDES PREPEND ${WUVORBIS_SRC_DIR}/)

add_library(wuvorbis MODULE)
set_target_properties(wuvorbis PROPERTIES CXX_STANDARD 11)
set_target_properties(wuvorbis PROPERTIES PREFIX "")
target_sources(wuvorbis PRIVATE ${WUVORBIS_SRC})
target_include_directories(wuvorbis PRIVATE ${WUVORBIS_INCLUDES})
target_link_libraries(wuvorbis tp_stub)
