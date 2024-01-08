
#===REQUIRED_CMAKE_VARIABLES================================#
#                                                           #
# set(ISPC_COMPILER_LOCATION "C:/ispc_compiler/ispc.exe")   #
# set(ISPC_COMPILER_TARGET "avx2")                          #
#                                                           #
#===========================================================#

project(ispc_texture_compressor)
if (DEFINED ISPC_COMPILER_LOCATION AND DEFINED ISPC_COMPILER_TARGET)
    add_custom_command(
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/ispc_texcomp/kernel.ispc
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel.o
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_ispc.h

            COMMAND
            ${ISPC_COMPILER_LOCATION}
            --target=${CMAKE_ISPC_COMPILER_TARGET}
            --arch=x86-64 ${CMAKE_CURRENT_SOURCE_DIR}/ispc_texcomp/kernel.ispc
            --header-outfile=${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_ispc.h
            -o ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel.o
    )

    add_custom_command(
            DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/ispc_texcomp/kernel_astc.ispc
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_astc.o
            OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_astc_ispc.h

            COMMAND ${ISPC_COMPILER_LOCATION}
            --target=${CMAKE_ISPC_COMPILER_TARGET}
            --arch=x86-64 ${CMAKE_CURRENT_SOURCE_DIR}/ispc_texcomp/kernel_astc.ispc
            --header-outfile=${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_astc_ispc.h
            -o ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/kernel_astc.o
    )

    add_library(ispc_texture_compressor
            ispc_texcomp/ispc/kernel_ispc.h
            ispc_texcomp/ispc/kernel.o

            ispc_texcomp/ispc/kernel_astc_ispc.h
            ispc_texcomp/ispc/kernel_astc.o

            ispc_texcomp/ispc_texcomp.h
            ispc_texcomp/ispc_texcomp.cpp
            ispc_texcomp/ispc_texcomp_astc.cpp
    )

    target_include_directories(ispc_texture_compressor
            PUBLIC ispc_texcomp/
            PUBLIC ${CMAKE_CURRENT_BINARY_DIR}/ispc_texcomp/ispc/
    )

else ()
    if (NOT DEFINED ISPC_COMPILER_LOCATION)
        message("Error: Did not ser var ISPC_COMPILER_TARGET")
    endif ()
    if (NOT DEFINED ISPC_COMPILER_LOCATION)
        message("Error: Did not ser var ISPC_COMPILER_LOCATION")
    endif ()
endif ()