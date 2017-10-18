project(container)

set(fixed_array_headers fixed_array.h)
add_library(fixed_array ${fixed_array_headers})
target_link_libraries(fixed_array algorithm core_headers dynamic_annotations throw_delegate)


set(inlined_vector_headers inlined_vector.h)
add_library(inlined_vector ${inlined_vector_headers})
target_link_libraries(inlined_vector algorithm core_headers throw_delegate memory)

# 
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
#     name = "fixed_array",
#     hdrs = ["fixed_array.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         "//absl/algorithm",
#         "//absl/base:core_headers",
#         "//absl/base:dynamic_annotations",
#         "//absl/base:throw_delegate",
#     ],
# )
# 
# 
# cc_library(
#     name = "inlined_vector",
#     hdrs = ["inlined_vector.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         "//absl/algorithm",
#         "//absl/base:core_headers",
#         "//absl/base:throw_delegate",
#         "//absl/memory",
#     ],
# )
# 
# 
# cc_library(
#     name = "test_instance_tracker",
#     testonly = 1,
#     srcs = ["internal/test_instance_tracker.cc"],
#     hdrs = ["internal/test_instance_tracker.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     visibility = [
#         "//absl:__subpackages__",
#     ],
# )
# 
# 
# cc_test(
#     name = "fixed_array_test",
#     srcs = ["fixed_array_test.cc"],
#     copts = ABSL_TEST_COPTS + ["-fexceptions"],
#     deps = [
#         ":fixed_array",
#         "//absl/base:core_headers",
#         "//absl/base:exception_testing",
#         "//absl/memory",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "fixed_array_test_noexceptions",
#     srcs = ["fixed_array_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":fixed_array",
#         "//absl/base:core_headers",
#         "//absl/base:exception_testing",
#         "//absl/memory",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "inlined_vector_test",
#     srcs = ["inlined_vector_test.cc"],
#     copts = ABSL_TEST_COPTS + ["-fexceptions"],
#     deps = [
#         ":inlined_vector",
#         ":test_instance_tracker",
#         "//absl/base",
#         "//absl/base:core_headers",
#         "//absl/base:exception_testing",
#         "//absl/memory",
#         "//absl/strings",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "inlined_vector_test_noexceptions",
#     srcs = ["inlined_vector_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":inlined_vector",
#         ":test_instance_tracker",
#         "//absl/base",
#         "//absl/base:core_headers",
#         "//absl/base:exception_testing",
#         "//absl/memory",
#         "//absl/strings",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# 
# cc_test(
#     name = "test_instance_tracker_test",
#     srcs = ["internal/test_instance_tracker_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":test_instance_tracker",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
