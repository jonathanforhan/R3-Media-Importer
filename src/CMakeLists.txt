file(GLOB_RECURSE C_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.c")
add_library(R3MI STATIC ${C_SOURCES});
target_include_directories(R3MI PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")

if (MSVC)
    set_target_properties(R3MI PROPERTIES COMPILE_FLAGS  "${CMAKE_CXX_FLAGS} /W4")
else ()
    set_target_properties(R3MI PROPERTIES COMPILE_FLAGS  "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -Werror")
endif ()