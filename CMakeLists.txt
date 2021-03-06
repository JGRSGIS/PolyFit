cmake_minimum_required(VERSION 3.1)

get_filename_component(PROJECT_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(PolyFit)

# One shouldn't generate the BUILD project directly in the SOURCES folder!
if ( ${CMAKE_CURRENT_BINARY_DIR} STREQUAL ${CMAKE_CURRENT_SOURCE_DIR} )
        if ( NOT SAME_BUILD_AND_SOURCE_FOLDER_WARNING_ALREADY_ISSUED )
                message(FATAL_ERROR "It is not advised to BUILD the binaries directly in the SOURCE folder!\n If you want to proceed with this option, just CONFIGURE the project once again" )
                set( SAME_BUILD_AND_SOURCE_FOLDER_WARNING_ALREADY_ISSUED TRUE )
        endif()
endif()

################################################################################

set (CMAKE_CXX_STANDARD 11)

################################################################################

# Detects whether this is a top-level project
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
        set(POLYFIT_TOPLEVEL_PROJECT ON)
else()
        set(POLYFIT_TOPLEVEL_PROJECT OFF)
endif()

set_property(GLOBAL PROPERTY USE_FOLDERS ON)

################################################################################

### Configuration
set(POLYFIT_ROOT         ${CMAKE_CURRENT_LIST_DIR})
set(POLYFIT_INCLUDE_DIR  ${POLYFIT_ROOT}  ${CMAKE_CURRENT_BINARY_DIR})
set(POLYFIT_SOURCE_DIR   ${POLYFIT_ROOT})


set(POLYFIT_glpk_DIR                ${POLYFIT_ROOT}/3rd_glpk)
set(POLYFIT_lpsolve_DIR             ${POLYFIT_ROOT}/3rd_lpsolve)
set(POLYFIT_qglviewer_DIR           ${POLYFIT_ROOT}/3rd_QGLViewer-2.6.3)
set(POLYFIT_scip_DIR                ${POLYFIT_ROOT}/3rd_scip)
set(POLYFIT_soplex_DIR              ${POLYFIT_ROOT}/3rd_soplex)

### conditionally compile certain modules depending on libraries found on the system
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake)

find_package(Boost REQUIRED)

################################################################################

add_subdirectory(3rd_glpk)
add_subdirectory(3rd_lpsolve)
add_subdirectory(3rd_QGLViewer-2.6.3)
add_subdirectory(3rd_scip)
add_subdirectory(3rd_soplex)

add_subdirectory(basic)
add_subdirectory(math)
add_subdirectory(method)
add_subdirectory(model)
add_subdirectory(renderer)
add_subdirectory(PolyFit)


