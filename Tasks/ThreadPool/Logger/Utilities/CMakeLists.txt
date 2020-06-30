cmake_minimum_required(VERSION 3.10)
project(Utilities)
 
# include all the headers from the include folder
include_directories(include)
 
# add the sources (.cpp) files for the Utilities library and test stub targets
set (SOURCES src/Utilities.cpp)

# generate the Utilities (shared) library target (.so / .dll) from the SOURCES
add_library(Utilities SHARED ${SOURCES} )

# generate the Utilities (static) library target (.a / .lib) from the SOURCES
add_library(UtilitiesStatic STATIC ${SOURCES} )

# generate the Utilities test stub target (executable test) from the SOURCES
add_executable(UtilitiesTest ${SOURCES})

# adds -D define flags to the compilation of source files (needed building the test stub target)
add_definitions(-DTEST_UTILITIES)




