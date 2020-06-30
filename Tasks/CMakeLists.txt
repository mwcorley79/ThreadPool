cmake_minimum_required(VERSION 3.10)
project(Tasks)

add_subdirectory(ThreadPool)

# include all the headers from the include folder
include_directories(include  ./ThreadPool/include ./ThreadPool/Logger/include  ./ThreadPool/Logger/BlockingQueue/include ./ThreadPool/Logger/Utilities/include)

# add the sources (.cpp) files for the Tasks library and test stub targets
set (SOURCES src/Task.cpp)

# generate the Tasks (shared) library target (.so / .dll) from the SOURCES
add_library(Task SHARED ${SOURCES} )

# generate the Tasks (static) library target (.a / .lib) from the SOURCES
add_library(TaskStatic STATIC ${SOURCES} )

# generate the Tasks test stub target (executable test) from the SOURCES
add_executable(TaskTest ${SOURCES})

# adds -D define flags to the compilation of source files (needed building the test stub target)
add_definitions(-DTEST_TASK)

target_link_libraries(TaskTest ThreadPool Logger BlockingQueue Utilities pthread)
