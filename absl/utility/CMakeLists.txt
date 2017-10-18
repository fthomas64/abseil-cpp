project(utility)

set(utility_sources utility.cc)
set(utility_headers utility.h)
add_library(utility ${utility_headers} ${utility_sources})
target_link_libraries(utility config type_traits)
target_include_directories(utility PUBLIC ${abseil-cpp_SOURCE_DIR})

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
#     name = "utility",
#     srcs = ["utility.cc"],
#     hdrs = ["utility.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         "//absl/base:config",
#         "//absl/meta:type_traits",
#     ],
# )
# 
# cc_test(
#     name = "utility_test",
#     srcs = ["utility_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":utility",
#         "//absl/base:core_headers",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
