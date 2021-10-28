find_package(LLVM REQUIRED CONFIG)

add_definitions(${LLVM_DEFINITIONS})
include_directories(${LLVM_INCLUDE_DIRS})
link_directories(${LLVM_LIBRARY_DIRS})

add_executable(LLVMStringObfuscator StrObfusPass.cpp)
llvm_map_components_to_libnames(llvm_libs core support irreader)
target_link_libraries(LLVMStringObfuscator ${llvm_libs})