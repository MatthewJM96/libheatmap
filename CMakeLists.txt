cmake_minimum_required(VERSION 3.22)

########################################################################################

###################
#     Options     #
###################

project(heatmap)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)

if (UNIX OR MINGW)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
    set(CMAKE_CXX_FLAGS_RELEASE "-O3")
    set(CMAKE_CXX_FLAGS_DEBUG "-g")
elseif (MSVC)
    set(CMAKE_CXX_FLAGS "/W3 /WX /EHsc /Zc:preprocessor")
    set(CMAKE_CXX_FLAGS_RELEASE "/MD /O2")
    set(CMAKE_CXX_FLAGS_DEBUG "/MDd /Od /Zi")

    # Don't error on secure warnings.
    add_compile_definitions(_CRT_SECURE_NO_WARNINGS=1)
endif()

########################################################################################

###############################
#     Compile Definitions     #
###############################

if (CMAKE_BUILD_TYPE STREQUAL "Debug")
    add_compile_definitions(DEBUG=1)
endif()

########################################################################################

#######################
#     Source Tree     #
#######################

add_library(heatmap STATIC
    "${PROJECT_SOURCE_DIR}/heatmap.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Blues.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/BrBG.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/BuGn.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/BuPu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/GnBu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/gray.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Greens.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Greys.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Oranges.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/OrRd.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PiYG.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PRGn.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PuBu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PuBuGn.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PuOr.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/PuRd.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Purples.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/RdBu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/RdGy.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/RdPu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/RdYlBu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/RdYlGn.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Reds.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/Spectral.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/YlGn.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/YlGnBu.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/YlOrBr.c"
    "${PROJECT_SOURCE_DIR}/colorschemes/YlOrRd.c"
)

########################################################################################

###########################################
#     Include and Library Directories     #
###########################################

target_include_directories(heatmap
    PUBLIC
    "${PROJECT_SOURCE_DIR}"
)

if (UNIX OR MINGW)
    target_link_libraries(heatmap
        m
    )
endif()
