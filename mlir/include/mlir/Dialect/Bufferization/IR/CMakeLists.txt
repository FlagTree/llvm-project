option(FLAGTREE_MLIR_TD_COMPAT_OLD_LLVM_VERSION
  "Enable Ascend backend assembly format for bufferization.to_memref"
  OFF)

if(FLAGTREE_MLIR_TD_COMPAT_OLD_LLVM_VERSION)
  list(APPEND LLVM_TABLEGEN_FLAGS "-DFLAGTREE_MLIR_TD_COMPAT_OLD_LLVM_VERSION")
endif()
add_mlir_dialect(BufferizationOps bufferization)
add_mlir_doc(BufferizationOps BufferizationOps Dialects/ -gen-dialect-doc)
add_mlir_interface(AllocationOpInterface)
add_mlir_interface(BufferDeallocationOpInterface)
add_mlir_interface(BufferizableOpInterface)
add_mlir_interface(BufferViewFlowOpInterface)

set(LLVM_TARGET_DEFINITIONS BufferizationEnums.td)
mlir_tablegen(BufferizationEnums.h.inc -gen-enum-decls)
mlir_tablegen(BufferizationEnums.cpp.inc -gen-enum-defs)
add_public_tablegen_target(MLIRBufferizationEnumsIncGen)
add_dependencies(mlir-headers MLIRBufferizationEnumsIncGen)
