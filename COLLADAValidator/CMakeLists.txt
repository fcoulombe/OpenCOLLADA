set(name OpenCOLLADAValidator)
project(${name})

set(libValidator_include_dirs
	${CMAKE_CURRENT_SOURCE_DIR}/include
)

set(libValidator_include_dirs ${libValidator_include_dirs} PARENT_SCOPE)  # adding include dirs to a parent scope

set(SRC
	src/main.cpp
	src/ValidationErrorHandler.cpp
	
	include/ValidationErrorHandler.h
	include/Writer.h
)

set(libValidator_libs
	optimized OpenCOLLADASaxFrameworkLoader
	optimized GeneratedSaxParser
	optimized OpenCOLLADAFramework
	optimized OpenCOLLADABaseUtils
	optimized MathMLSolver
	optimized ${PCRE_LIBRARIES}
	optimized ${LIBXML2_LIBRARIES}
	optimized UTF
	debug OpenCOLLADASaxFrameworkLoaderd
	debug GeneratedSaxParserd
	debug OpenCOLLADAFrameworkd
	debug OpenCOLLADABaseUtilsd
	debug MathMLSolverd
	debug ${PCRE_LIBRARIES}d
	debug ${LIBXML2_LIBRARIES}d
	debug UTFd
)

include_directories(
	${libValidator_include_dirs}
	${libBaseUtils_include_dirs}
	${libFramework_include_dirs}
	${libSaxFrameworkLoader_include_dirs}
	${libGeneratedSaxParser_include_dirs}
)
link_directories(${LIBRARY_OUTPUT_PATH})

add_executable(${name} ${SRC})
target_link_libraries(${name} ${libValidator_libs})
add_dependencies(${name} ${CMAKE_REQUIRED_LIBRARIES})
