cmake_minimum_required (VERSION 2.8)

set (ag_SRCS ignore.c log.c options.c print.c scandir.c decompress.c lang.c search.c util.c main.c)

include_directories (${CMAKE_SOURCE_DIR})

add_library (ag STATIC ${ag_SRCS})
add_executable (ag_executable main.c)

target_link_libraries (ag_executable pthread ag ${LIBS})

set_property (TARGET ag_executable PROPERTY OUTPUT_NAME "ag")

install (TARGETS ag_executable DESTINATION bin)

