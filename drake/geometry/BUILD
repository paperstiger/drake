# -*- python -*-
# This file contains rules for Bazel; see drake/doc/bazel.rst.

load(
    "//tools:drake.bzl",
    "drake_cc_googletest",
    "drake_cc_library",
)
load("//tools:lint.bzl", "add_lint_tests")

package(default_visibility = ["//visibility:public"])

drake_cc_library(
    name = "geometry_frame",
    srcs = [],
    hdrs = ["geometry_frame.h"],
    deps = ["//drake/common"],
)

drake_cc_library(
    name = "geometry_ids",
    srcs = [],
    hdrs = ["geometry_ids.h"],
    deps = [":identifier"],
)

drake_cc_library(
    name = "geometry_instance",
    srcs = ["geometry_instance.cc"],
    hdrs = ["geometry_instance.h"],
    deps = [
        "//drake/common",
    ],
)

drake_cc_library(
    name = "geometry_system",
    srcs = ["geometry_system.cc"],
    hdrs = [
        "geometry_system.h",
        "query_handle.h",
    ],
    deps = [
        ":geometry_frame",
        ":geometry_instance",
        "//drake/common",
        "//drake/geometry/query_results:penetration_as_point_pair",
        "//drake/systems/framework",
    ],
)

drake_cc_library(
    name = "identifier",
    srcs = [],
    hdrs = ["identifier.h"],
    deps = ["//drake/common"],
)

# -----------------------------------------------------

drake_cc_library(
    name = "expect_error_message",
    srcs = [],
    hdrs = ["test/expect_error_message.h"],
)

drake_cc_googletest(
    name = "geometry_system_test",
    deps = [
        ":expect_error_message",
        ":geometry_system",
    ],
)

drake_cc_googletest(
    name = "identifier_test",
    deps = [":identifier"],
)

add_lint_tests()
