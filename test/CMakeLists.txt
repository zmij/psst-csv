#    /psst-csv/test/CMakeLists.txt
#
#    @author zmij
#    @date Jan 25, 2019

cmake_minimum_required(VERSION 2.6)

find_package(ExternalProjectGTest REQUIRED)
if (NOT CMAKE_THREAD_LIBS_INIT)
    find_package(Threads REQUIRED)
endif()

# Add your package dependencies for test here

include_directories(${GTEST_INCLUDE_DIRS})

set(
    test_program_SRCS
    # Add your sources here
    csv_test.cpp
)
add_executable(test-psst-csv ${test_program_SRCS})
target_link_libraries(
    test-psst-csv
    ${GTEST_BOTH_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    # Add your libraries here
)

if (GTEST_XML_OUTPUT)
    set (
        TEST_ARGS
        --gtest_output=xml:test-psst-csv-detail.xml
    )
endif()

add_test(
    NAME test-psst-csv
    COMMAND test-psst-csv ${TEST_ARGS}
)
