cmake_minimum_required(VERSION 3.10)
project(Logger)

add_subdirectory(BlockingQueue)
add_subdirectory(Utilities)

# include all the headers from the include folder
include_directories(include ./BlockingQueue/include ./Utilities/include)

# add the sources (.cpp) files for the Logger library and test stub targets
set (SOURCES src/Logger.cpp)

# generate the Logger (shared) library target (.so / .dll) from the SOURCES
add_library(Logger SHARED ${SOURCES} )

# generate the Logger (static) library target (.a / .lib) from the SOURCES
add_library(LoggerStatic STATIC ${SOURCES} )

# generate the Logger test stub target (executable test) from the SOURCES
add_executable(LoggerTest ${SOURCES})

# adds -D define flags to the compilation of source files (needed building the test stub target)
add_definitions(-DTEST_LOGGER)

target_link_libraries(LoggerTest BlockingQueue Utilities pthread)
