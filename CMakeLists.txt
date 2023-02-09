find_package(ZLIB REQUIRED)

file(GLOB_RECURSE SRCS "*.c")
add_library(bgzf STATIC ${SRCS})
set_property(TARGET bgzf PROPERTY POSITION_INDEPENDENT_CODE ON)
target_compile_options(bgzf PRIVATE -Wno-unused-result)

target_include_directories(bgzf
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include/bgzf ${ZLIB_INCLUDE_DIRS}
)

target_link_libraries(bgzf ${ZLIB_LIBRARIES})

if (CMAKE_BUILD_TYPE STREQUAL Release)
    target_compile_options(bgzf PRIVATE -fdata-sections -ffunction-sections)
endif()
