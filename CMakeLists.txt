cmake_minimum_required(VERSION 3.12)

find_package(Clang CONFIG REQUIRED)

add_executable(index-import index-import.cpp)
target_include_directories(index-import SYSTEM PRIVATE ${LLVM_INCLUDE_DIRS} ${CLANG_INCLUDE_DIRS})
target_compile_features(index-import PRIVATE cxx_std_14)
set_target_properties(index-import PROPERTIES CXX_EXTENSIONS OFF)
target_compile_options(index-import PRIVATE -Wall -Wextra)
if(NOT LLVM_ENABLE_RTTI)
  target_compile_options(index-import PRIVATE -fno-rtti)
endif()
target_link_libraries(index-import PRIVATE clangIndex)
target_link_options(index-import PRIVATE -dead_strip)
