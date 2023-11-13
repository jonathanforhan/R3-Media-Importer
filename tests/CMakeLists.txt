add_custom_target(COPY_ASSETS
	COMMAND ${CMAKE_COMMAND} -E copy_directory
		"${CMAKE_CURRENT_SOURCE_DIR}/assets"
		"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/assets")
add_custom_target(COPY_SHADERS
	COMMAND ${CMAKE_COMMAND} -E copy_directory
		"${CMAKE_CURRENT_SOURCE_DIR}/shaders"
		"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/shaders")

function(TEST_PROJECT)
	file(GLOB_RECURSE C_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.c")
	get_filename_component(DIRNAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
	add_executable(${DIRNAME})

	if (MSVC)
		set_target_properties(${DIRNAME} PROPERTIES COMPILE_FLAGS  "${CMAKE_C_FLAGS} /W4")
	else ()
		set_target_properties(${DIRNAME} PROPERTIES COMPILE_FLAGS  "${CMAKE_C_FLAGS} -Wall -Wextra -Wpedantic")
	endif ()

	target_sources(${DIRNAME} PUBLIC ${C_SOURCES})
	target_include_directories(${DIRNAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
	target_link_libraries(${DIRNAME} PUBLIC R3MI)
	add_dependencies(${DIRNAME} COPY_ASSETS)
	add_dependencies(${DIRNAME} COPY_SHADERS)
endfunction()

