cmake_minimum_required (VERSION 2.8)

include (CheckFunctionExists)
include (CheckStructHasMember)

project (the_silver_searcher)
set (PROJECT_VERSION "0.21.1")

set (PACKAGE "${PROJECT_NAME}")
set (VERSION "${PROJECT_VERSION}")
set (PACKAGE_BUGREPORT "https://github.com/ggreer/the_silver_searcher/issues")
set (PACKAGE_URL "https://github.com/ggreer/the_silver_searcher")
set (PACKAGE_NAME "${PACKAGE}")
set (PACKAGE_TARNAME "${PACKAGE}")
set (PACKAGE_VERSION "${VERSION}")
set (PACKAGE_STRING "${PACKAGE} ${VERSION}")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR})
find_package(PCRE REQUIRED)
find_package(ZLIB REQUIRED)
find_package(LZMA)
if (LZMA_FOUND)
	set(HAVE_LZMA_H)
endif(LZMA_FOUND)

include_directories(${PCRE_INCLUDE_DIRS} ${ZLIB_INCLUDE_DIRS} ${LZMA_INCLUDE_DIRS})
set(LIBS ${LIBS} ${PCRE_LIBRARIES} ${ZLIB_LIBRARIES} ${LZMA_LIBRARIES})

check_function_exists (asprintf HAVE_ASPRINTF)
check_function_exists (fgetln HAVE_FGETLN)
check_function_exists (getline HAVE_GETLINE)
check_function_exists (strndup HAVE_STRNDUP)
check_function_exists (realpath HAVE_REALPATH)

check_struct_has_member ("struct dirent" d_type dirent.h HAVE_DIRENT_DTYPE)

message ("-- Configuring src/config.h")
configure_file (${CMAKE_SOURCE_DIR}/config.h.in ${CMAKE_SOURCE_DIR}/src/config.h)

add_subdirectory (src)
add_subdirectory (doc)

