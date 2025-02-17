cmake_minimum_required (VERSION 3.8)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR})

set(SrcFiles
	${MY_SRC_DIR}/SearchEngine.cpp
	${MY_SRC_DIR}/ConverterJSON.cpp
	${MY_SRC_DIR}/InvertedIndex.cpp
)

set(TestFiles
	test_search_engine.cpp
)

include(FetchContent)

FetchContent_Declare(
  googletest
  GIT_REPOSITORY https://github.com/google/googletest.git
  GIT_TAG release-1.12.1
)
FetchContent_MakeAvailable(googletest)
include_directories(${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
enable_testing()
include(GoogleTest)

add_executable(GtestTests ${TestsFiles} ${SrcFiles})

gtest_discover_tests(GtestTests)

target_link_libraries(GtestTests nlohmann_json::nlohmann_json GTest::gtest_main)
target_include_directories(GtestTests PUBLIC ${MY_INCLUDE_DIR})
