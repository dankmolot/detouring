file(GLOB MINHOOK_SRC_FILES ${CMAKE_CURRENT_LIST_DIR}/minhook/src/*.c)
file(GLOB SRC_FILES ${CMAKE_CURRENT_LIST_DIR}/source/*.cpp)

add_library(garrysmod_detouring STATIC hde/src/hde.c  ${MINHOOK_SRC_FILES} ${SRC_FILES})
add_library(gmod::detouring ALIAS garrysmod_detouring)

target_include_directories(garrysmod_detouring PRIVATE include/detouring)
target_include_directories(garrysmod_detouring PUBLIC
    include
    hde/include
    minhook/include
)
# target_include_directories(garrysmod_detouring PRIVATE include/scanning)
target_link_libraries(garrysmod_detouring ${CMAKE_DL_LIBS})

# Let everyone know that scanning was included
set(DETOURING_FOUND TRUE CACHE INTERNAL "DETOURING_FOUND")
