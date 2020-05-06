cmake_minimum_required(VERSION 3.16)

project(TestProject)

# NOTE: you're going to need to go in and set this to something, e.g., in cmake-gui,
# otherwise it's going to be an empty string. It's pretty hard to check and see if CONFIG is blank actually.
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "Potatoes")

# https://cmake.org/cmake/help/v3.17/manual/cmake-generator-expressions.7.html#debugging
# Since generator expressions are evaluated during generation of the buildsystem, 
# and not during processing of CMakeLists.txt files, it is not possible to inspect their result with the message() command
#
# So that means, look for a file named generated_values.txt in your build directory
set(outputFilePath ${CMAKE_CURRENT_BINARY_DIR}/generated_values.txt)

set(expressionvalue "CONFIG is '$<CONFIG>', The generator expression resolves to '$<$<CONFIG:Debug>:debug>$<$<CONFIG:Release>:release>$<$<CONFIG:Potatoes>:tomatoes>'")

file(GENERATE OUTPUT ${outputFilePath} CONTENT ${expressionvalue})
