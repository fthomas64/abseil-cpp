project(memory)

set(memory_headers memory.h)
add_library(memory ${memory_headers})
target_link_libraries(memory type_traits)
set_target_properties(memory PROPERTIES LINKER_LANGUAGE CXX)

# load(
#     "//absl:copts.bzl",
#     "ABSL_DEFAULT_COPTS",
#     "ABSL_TEST_COPTS",
# )
# 
# package(default_visibility = ["//visibility:public"])
# 
# licenses(["notice"])  # Apache 2.0
# 
# cc_library(
#     name = "memory",
#     hdrs = ["memory.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = ["//absl/meta:type_traits"],
# )
# 
# cc_test(
#     name = "memory_test",
#     srcs = ["memory_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":memory",
#         "//absl/base",
#         "//absl/base:core_headers",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
