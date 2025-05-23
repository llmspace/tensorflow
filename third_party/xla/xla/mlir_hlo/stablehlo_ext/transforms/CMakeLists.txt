# Copyright 2023 The StableHLO Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(LLVM_TARGET_DEFINITIONS passes.td)
mlir_tablegen(passes.h.inc -gen-pass-decls)
add_public_tablegen_target(StablehloExtensionPassesIncGen)

add_mlir_dialect_library(StablehloExtensionPasses
  PARTIAL_SOURCES_INTENDED
  chlo_recompose_ops.cpp
  chlo_preserve_high_level_ops.cpp
  stablehlo_canonicalize_dynamism.cpp
  stablehlo_refine_shapes.cpp
  sdy_refine_shapes.cpp

  DEPENDS
  StablehloExtensionPassesIncGen

  LINK_LIBS PUBLIC
  ChloOps
  MLIRFuncDialect
  MLIRIR
  MLIRInferTypeOpInterface
  MLIRSupport
  MLIRTransformUtils
  StablehloExtensionOps
  StablehloBase
  StablehloOps
  StablehloOptimizationPasses
  StablehloPasses
  StablehloTypeInference
)
