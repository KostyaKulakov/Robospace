cmake_minimum_required(VERSION 2.8.8)

project(Robospace)

set(Robospace_SRCS
	src/main.cpp
	src/Robospace.cpp
)

set(Robospace_HDRS
	src/Robospace.h
)

# TODO: Currently, there is no polycode finding
# This section should be completely rewritten

# find_package(Polycode REQUIRED)

if(POLYCODE_FOUND)
else(POLYCODE_FOUND)
	set(POLYCODE_DIR "/usr/lib/Polycode" CACHE STRING "Polycode framework directory")
	set(POLYCODE_INCLUDE_DIRS
		${POLYCODE_DIR}/Core/include
		/usr/include/freetype2
		/usr/include/AL
	)
	set(POLYCODE_LINK_DIR
		${POLYCODE_DIR}/Core/lib
	)
	set(POLYCODE_LIBRARIES
		GL
		GLU
		Polycore
		SDL
		X11
		assimp
		freetype
		openal
		physfs
		png
	)
endif(POLYCODE_FOUND)

file(COPY ${Robospace_SOURCE_DIR}/res
	DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

include_directories(${POLYCODE_INCLUDE_DIRS})
link_directories(${POLYCODE_LINK_DIR})


add_executable(Robospace ${Robospace_SRCS})
target_link_libraries(Robospace ${POLYCODE_LIBRARIES})
