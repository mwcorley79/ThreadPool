cmake_minimum_required(VERSION 3.10)
project(ThreadPool)

add_subdirectory(Logger)

# include all the headers from the include folder
include_directories(include ./Logger/include  ./Logger/BlockingQueue/include ./Logger/Utilities/include)

# add the sources (.cpp) files for the ThreadPool library and test stub targets
set (SOURCES src/ThreadPool.cpp)

# generate the ThreadPool (shared) library target (.so / .dll) from the SOURCES
add_library(ThreadPool SHARED ${SOURCES} )

# generate the ThreadPool (static) library target (.a / .lib) from the SOURCES
add_library(ThreadPoolStatic STATIC ${SOURCES} )

# generate the ThreadPool test stub target (executable test) from the SOURCES
add_executable(ThreadPoolTest ${SOURCES})

# adds -D define flags to the compilation of source files (needed building the test stub target)
add_definitions(-DTEST_THREADPOOL)

target_link_libraries(ThreadPoolTest Logger BlockingQueue Utilities pthread)
