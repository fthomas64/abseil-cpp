project(meta)

###
### Config Library
###
set(type_traits_headers type_traits.h)

add_library(type_traits ${type_traits_headers})
set_target_properties(type_traits PROPERTIES LINKER_LANGUAGE CXX)
target_link_libraries(type_traits config)

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
#     name = "type_traits",
#     hdrs = ["type_traits.h"],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         "//absl/base:config",
#     ],
# )
# 
# cc_test(
#     name = "type_traits_test",
#     srcs = ["type_traits_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":type_traits",
#         "//absl/base:core_headers",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
