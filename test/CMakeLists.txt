cmake_minimum_required(VERSION 2.8)
project(tester)

set(CMAKE_CXX_STANDARD 17)
find_package(CxxTest REQUIRED)

if(CXXTEST_FOUND)
	enable_testing()
	file(GLOB_RECURSE TESTES ${CMAKE_CURRENT_SOURCE_DIR}/*.h ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
	CXXTEST_ADD_TEST(${PROJECT_NAME} runner.cpp ${TESTES})
	target_link_libraries(${PROJECT_NAME} unprecacher_static)
	set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "-m32 -O0" LINK_FLAGS "-m32 -O0")
	add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND ./${PROJECT_NAME})
endif()
