# set a variable that contains the list
# of source files to be built for our targets
set(${PROJECT_ID}_TEST_SOURCES
	BoardTest.cpp
	GameTest.cpp
	main.cpp
)

# the ${PROJECT_ID}-test target shall be an executable
add_executable(${PROJECT_ID}-test)

# set the source files to be built into the executable
target_sources(${PROJECT_ID}-test
	PRIVATE
		${${PROJECT_ID}_TEST_SOURCES}
)

# provide private include paths for our executable
target_include_directories(${PROJECT_ID}-test
	PRIVATE
		../include
)

# set the C++ 20 standard
target_compile_features(${PROJECT_ID}-test
	PRIVATE
		cxx_std_20
)

target_compile_options(${PROJECT_ID}-test
	PRIVATE
		-ftest-coverage
		-fPIC
)

target_link_libraries(${PROJECT_ID}-test
	PUBLIC
		${PROJECT_ID}-static
		gtest
		gmock
)
include(GoogleTest)
gtest_discover_tests(${PROJECT_ID}-test)
