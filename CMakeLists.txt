cmake_minimum_required( VERSION 3.10 )

project( feature_detector )

set( CMAKE_BUILD_TYPE "Release" )
set( CMAKE_CXX_FLAGS "-std=c++17 -O3 -Wall" )
set( CMAKE_EXPORT_COMPILE_COMMANDS ON )

find_package( OpenCV REQUIRED )
find_package( Eigen3 REQUIRED )

set( SLAM_UTILITY_PATH ${PROJECT_SOURCE_DIR}/../Slam_Utility )

# include_directories( "/usr/include/eigen3" )
include_directories( ${SLAM_UTILITY_PATH}/src/datatype )
include_directories( ${SLAM_UTILITY_PATH}/src/log )
include_directories( ${SLAM_UTILITY_PATH}/src/math )
include_directories( ${PROJECT_SOURCE_DIR}/src )
include_directories( ${PROJECT_SOURCE_DIR}/test )

aux_source_directory( ${SLAM_UTILITY_PATH}/src/datatype     SLAM_UTILITY_DATATYPE )
aux_source_directory( ${SLAM_UTILITY_PATH}/src/log          SLAM_UTILITY_LOG )
aux_source_directory( ${SLAM_UTILITY_PATH}/src/math         SLAM_UTILITY_MATH )
aux_source_directory( ${PROJECT_SOURCE_DIR}/src             FEATURE_DETECTOR )

add_executable( test_feature_detector
    ${SLAM_UTILITY_DATATYPE}
    ${SLAM_UTILITY_LOG}
    ${SLAM_UTILITY_MATH}
    ${FEATURE_DETECTOR}
    test/test_feature_detector.cpp
)

target_link_libraries( test_feature_detector
    # TBB::tbb
    ${OpenCV_LIBS}
)
