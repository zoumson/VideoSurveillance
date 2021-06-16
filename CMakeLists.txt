cmake_minimum_required (VERSION 3.0)

PROJECT(morphology)

#Set the compiler
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE Release)
set( EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set( LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)


#Set ccache (for speeding up)
find_program(CCACHE_FOUND ccache) 
if(CCACHE_FOUND) 
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache) 
    set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache) 
endif(CCACHE_FOUND) 
set (CMAKE_CXX_FLAGS "-DPCL_ONLY_CORE_POINT_TYPES=ON -DNO_EXPLICIT_INSTANTIATIONS") 

# Requires OpenCV
FIND_PACKAGE( OpenCV 4.0.0 REQUIRED )
MESSAGE("OpenCV version : ${OpenCV_VERSION}")

include_directories(${OpenCV_INCLUDE_DIRS})
link_directories(${OpenCV_LIB_DIR})

ADD_EXECUTABLE( backgroundSubtraction ${PROJECT_SOURCE_DIR}/src/backgroundSubtraction.cpp )
TARGET_LINK_LIBRARIES( backgroundSubtraction ${OpenCV_LIBS} )

ADD_EXECUTABLE( dilation ${PROJECT_SOURCE_DIR}/src/dilation.cpp )
TARGET_LINK_LIBRARIES( dilation ${OpenCV_LIBS} )

ADD_EXECUTABLE( erosion ${PROJECT_SOURCE_DIR}/src/erosion.cpp )
TARGET_LINK_LIBRARIES( erosion ${OpenCV_LIBS} )

ADD_EXECUTABLE( frameDifferencing ${PROJECT_SOURCE_DIR}/src/frameDifferencing.cpp )
TARGET_LINK_LIBRARIES( frameDifferencing ${OpenCV_LIBS} )

ADD_EXECUTABLE( morphologicalOperations ${PROJECT_SOURCE_DIR}/src/morphologicalOperations.cpp )
TARGET_LINK_LIBRARIES( morphologicalOperations ${OpenCV_LIBS} )