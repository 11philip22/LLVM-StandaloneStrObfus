project(StrObfuscation)
cmake_minimum_required(VERSION 3.20)

if(WIN32)
    set(LT_LLVM_INSTALL_DIR "C:/llvm" CACHE PATH "LLVM installation directory")
    set(LT_LLVM_INCLUDE_DIR "${LT_LLVM_INSTALL_DIR}/include/llvm")
    set(LT_LLVM_CMAKE_FILE "${LT_LLVM_INSTALL_DIR}/lib/cmake/llvm/LLVMConfig.cmake")
endif()

list(APPEND CMAKE_PREFIX_PATH "${LT_LLVM_INSTALL_DIR}/lib/cmake/llvm/")

find_package(LLVM REQUIRED CONFIG)

add_definitions(${LLVM_DEFINITIONS})
include_directories(${LLVM_INCLUDE_DIRS})
link_directories(${LLVM_LIBRARY_DIRS})

add_executable(LLVMStringObfuscator StrObfusPass.cpp)
llvm_map_components_to_libnames(llvm_libs core support irreader)
target_link_libraries(LLVMStringObfuscator ${llvm_libs})
