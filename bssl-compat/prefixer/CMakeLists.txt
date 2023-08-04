project(prefixer)

# https://llvm.org/docs/CMake.html#embedding-llvm-in-your-project

find_package(Clang REQUIRED CONFIG)
find_package(LLVM REQUIRED CONFIG)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "LLVM_CMAKE_DIR          = ${LLVM_CMAKE_DIR}")
message(STATUS "LLVM_INCLUDE_DIRS       = ${LLVM_INCLUDE_DIRS}")
message(STATUS "LLVM_LIBRARY_DIRS       = ${LLVM_LIBRARY_DIRS}")
message(STATUS "LLVM_ENABLE_EH          = ${LLVM_ENABLE_EH}")
message(STATUS "LLVM_ENABLE_RTTI        = ${LLVM_ENABLE_RTTI}")
message(STATUS "LLVM_DEFINITIONS        = ${LLVM_DEFINITIONS}")
message(STATUS "LLVM_LINK_LLVM_DYLIB    = ${LLVM_LINK_LLVM_DYLIB}")


list(APPEND CMAKE_MODULE_PATH ${LLVM_CMAKE_DIR})
include(AddLLVM)


add_executable(prefixer prefixer.cpp)
llvm_update_compile_flags(prefixer)
target_include_directories(prefixer PRIVATE "${LLVM_INCLUDE_DIRS}")
target_link_directories(prefixer PRIVATE "${LLVM_LIBRARY_DIRS}")
target_link_libraries(prefixer PRIVATE clang-cpp)
