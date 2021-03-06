cmake_minimum_required(VERSION 3.10)
project(BlockingQueue)
 
####################### Build BlockingQueue targets ################################
# include all the headers from the include folder
include_directories(include)

# add the sources (.cpp) files for the BlockingQueue library and test stub targets
set (SOURCES src/Cpp11-BlockingQueue.cpp)

# generate the BlockingQueue (shared) library target (.so / .dll) from the SOURCES
add_library(BlockingQueue SHARED ${SOURCES} )

# generate the BlockingQueue (static) library target (.a / .lib) from the SOURCES
add_library(BlockingQueueStatic STATIC ${SOURCES} )

# generate the Utility test stub target (executable test) from the SOURCES
add_executable(BlockingQueueTest ${SOURCES})
add_definitions(-DTEST_BLOCKING_QUEUE)

if (UNIX)
    # link pthread to the BlockingQueueTest target
    target_link_libraries (BlockingQueueTest pthread)
endif (UNIX)

# install the statis and shared libs into the bin directory of the install directory
install(TARGETS BlockingQueueStatic  DESTINATION lib)



