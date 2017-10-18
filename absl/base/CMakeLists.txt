project(base)


#
# Copyright 2017 The Abseil Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

###
### Config Library
###
set(config_headers
config.h
policy_checks.h)

add_library(config ${config_headers})
set_target_properties(config PROPERTIES LINKER_LANGUAGE CXX)


###
### dynamic_annotations library
###
set(dynamic_annotations_sources dynamic_annotations.cc)
set(dynamic_annotations_headers dynamic_annotations.h)
add_library(dynamic_annotations ${dynamic_annotations_sources} ${dynamic_annotations_headers})
target_include_directories(dynamic_annotations PUBLIC ${abseil-cpp_SOURCE_DIR})

###
### core_headers library
### 
set(core_headers
attributes.h
         macros.h
         optimization.h
         port.h
         thread_annotations.h)
add_library(core_headers ${core_headers})
target_link_libraries(core_headers config dynamic_annotations)

###
### spinlock_wait library
###
set(spinlock_wait_sources 
        internal/spinlock_posix.inc
        internal/spinlock_wait.cc
        internal/spinlock_win32.inc
        )
        
set(spinlock_wait_headers
internal/scheduling_mode.h
        internal/spinlock_wait.h)
        
add_library(spinlock_wait ${spinlock_wait_sources} ${spinlock_wait_headers})
target_link_libraries(spinlock_wait core_headers)

###
### base_internal
###
set(base_internal_headers
internal/identity.h
internal/invoke.h)

add_library(base_internal ${base_internal_headers})
set_target_properties(base_internal PROPERTIES LINKER_LANGUAGE CXX)

###
### base
###

set(base_sources
internal/cycleclock.cc
internal/raw_logging.cc
internal/spinlock.cc
internal/sysinfo.cc
internal/thread_identity.cc
internal/unscaledcycleclock.cc
)

set(base_headers
call_once.h
casts.h
internal/atomic_hook.h
internal/cycleclock.h
internal/log_severity.h
internal/low_level_scheduling.h
internal/per_thread_tls.h
internal/raw_logging.h
internal/spinlock.h
internal/sysinfo.h
internal/thread_identity.h
internal/tsan_mutex_interface.h
internal/unscaledcycleclock.h
)

add_library(base ${base_sources} ${base_headers})
target_link_libraries(base base_internal config core_headers dynamic_annotations spinlock_wait)

###
### malloc_extension
###
set(malloc_extension_sources
internal/malloc_extension.cc
)

set(malloc_extension_headers
internal/malloc_extension.h
internal/malloc_extension_c.h)

add_library(malloc_extension ${malloc_extension_headers} ${malloc_extension_headers})
target_link_libraries(malloc_extension core_headers dynamic_annotations)

###
### malloc_internal
###
set(malloc_internal_sources
internal/low_level_alloc.cc
internal/malloc_hook.cc
internal/malloc_hook_mmap_linux.inc)

set(malloc_internal_headers
internal/low_level_alloc.h
internal/malloc_hook.h
internal/malloc_hook_c.h)

set(malloc_internal_textual_headers internal/malloc_hook_invoke.h)

add_library(malloc_internal ${malloc_internal_sources} ${malloc_internal_headers} ${malloc_internal_textual_headers})
target_link_libraries(malloc_internal base config core_headers dynamic_annotations spinlock_wait)

###
### endian library 
###
set(endian_headers internal/endian.h internal/unaligned_access.h)
add_library(endian ${endian_headers})
target_link_libraries(endian config core_headers)

# cc_library(
#     name = "endian",
#     hdrs = [
#         "internal/endian.h",
#         "internal/unaligned_access.h",
#     ],
#     copts = ABSL_DEFAULT_COPTS,
#     deps = [
#         ":config",
#         ":core_headers",
#     ],
# )

# cc_test(
#     name = "bit_cast_test",
#     size = "small",
#     srcs = [
#         "bit_cast_test.cc",
#     ],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         ":core_headers",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_library(
#     name = "throw_delegate",
#     srcs = ["internal/throw_delegate.cc"],
#     hdrs = ["internal/throw_delegate.h"],
#     copts = ABSL_DEFAULT_COPTS + ABSL_EXCEPTIONS_FLAG,
#     features = [
#         "-use_header_modules",
#     ],
#     visibility = [
#         "//absl:__subpackages__",
#     ],
#     deps = [
#         ":base",
#         ":config",
#         ":core_headers",
#     ],
# )
# 
# cc_test(
#     name = "throw_delegate_test",
#     srcs = ["throw_delegate_test.cc"],
#     copts = ABSL_TEST_COPTS + ABSL_EXCEPTIONS_FLAG,
#     deps = [
#         ":throw_delegate",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_library(
#     name = "exception_testing",
#     testonly = 1,
#     hdrs = ["internal/exception_testing.h"],
#     copts = ABSL_TEST_COPTS,
#     visibility = ["//absl:__subpackages__"],
#     deps = [
#         ":config",
#         "@com_google_googletest//:gtest",
#     ],
# )
# 
# cc_test(
#     name = "invoke_test",
#     size = "small",
#     srcs = ["invoke_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base_internal",
#         "//absl/memory",
#         "//absl/strings",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# # Common test library made available for use in non-absl code that overrides
# # AbslInternalSpinLockDelay and AbslInternalSpinLockWake.
# cc_library(
#     name = "spinlock_test_common",
#     testonly = 1,
#     srcs = ["spinlock_test_common.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         ":core_headers",
#         ":spinlock_wait",
#         "//absl/synchronization",
#         "@com_google_googletest//:gtest",
#     ],
#     alwayslink = 1,
# )
# 
# cc_test(
#     name = "spinlock_test",
#     size = "medium",
#     srcs = ["spinlock_test_common.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         ":core_headers",
#         ":spinlock_wait",
#         "//absl/synchronization",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 

# 
# cc_test(
#     name = "endian_test",
#     srcs = ["internal/endian_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         ":config",
#         ":endian",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "config_test",
#     srcs = ["config_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":config",
#         "//absl/synchronization:thread_pool",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "call_once_test",
#     srcs = ["call_once_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         ":core_headers",
#         "//absl/synchronization",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "raw_logging_test",
#     srcs = ["raw_logging_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "sysinfo_test",
#     size = "small",
#     srcs = ["internal/sysinfo_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     deps = [
#         ":base",
#         "//absl/synchronization",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "low_level_alloc_test",
#     size = "small",
#     srcs = ["internal/low_level_alloc_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     linkopts = select({
#         "//absl:windows": [],
#         "//conditions:default": ["-pthread"],
#     }),
#     deps = [":malloc_internal"],
# )
# 
# cc_test(
#     name = "thread_identity_test",
#     size = "small",
#     srcs = ["internal/thread_identity_test.cc"],
#     copts = ABSL_TEST_COPTS,
#     linkopts = select({
#         "//absl:windows": [],
#         "//conditions:default": ["-pthread"],
#     }),
#     deps = [
#         ":base",
#         ":core_headers",
#         "//absl/synchronization",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
# cc_test(
#     name = "malloc_extension_system_malloc_test",
#     size = "small",
#     srcs = ["internal/malloc_extension_test.cc"],
#     copts = select({
#         "//absl:windows": [
#             "/DABSL_MALLOC_EXTENSION_TEST_ALLOW_MISSING_EXTENSION=1",
#         ],
#         "//conditions:default": [
#             "-DABSL_MALLOC_EXTENSION_TEST_ALLOW_MISSING_EXTENSION=1",
#         ],
#     }) + ABSL_TEST_COPTS,
#     features = [
#         # This test can't be run under lsan because the test requires system
#         # malloc, and lsan provides a competing malloc implementation.
#         "-leak_sanitize",
#     ],
#     deps = [
#         ":malloc_extension",
#         "@com_google_googletest//:gtest_main",
#     ],
# )
# 
