project(algorithm)

set(algorithm_headers algorithm.h)
add_library(algorithm ${algorithm_headers})
set_target_properties(algorithm PROPERTIES LINKER_LANGUAGE CXX)

set(container_headers container.h)
add_library(container ${container_headers})
target_link_libraries(container algorithm core_headers type_traits)

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
#     name = "algorithm",
#     hdrs = ["algorithm.h"],
#     copts = ABSL_DEFAULT_COPTS,
# )
# 
# cc_test(
#     name = "algorithm_test",
#     size = "small",
#     srcs = ["algorithm_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":algorithm",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_library(
#     name = "container",
#     hdrs = [
#         "container.h",
#     ],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         ":algorithm",
#         "//absl/base:core_headers",
#         "//absl/meta:type_traits",
#     ],
# )
# 
# cc_test(
#     name = "container_test",
#     srcs = ["container_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":container",
#         "//absl/base",
#         "//absl/base:core_headers",
#         "//absl/memory",
#         "//absl/types:span",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
