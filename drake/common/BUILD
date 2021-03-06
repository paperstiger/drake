# -*- python -*-
# This file contains rules for Bazel; see drake/doc/bazel.rst.

load(
    "//tools:drake.bzl",
    "drake_cc_binary",
    "drake_cc_googletest",
    "drake_cc_library",
)
load("//tools:install.bzl", "install")
load("//tools:lint.bzl", "add_lint_tests")

package(default_visibility = ["//visibility:public"])

# A library of things that EVERYONE should want and MUST EAT.
# Be appropriately hesitant when adding new things here.
drake_cc_library(
    name = "common",
    srcs = [
        "drake_assert_and_throw.cc",
        "text_logging.cc",
    ],
    hdrs = [
        "constants.h",
        "drake_assert.h",
        "drake_assertion_error.h",
        "drake_compat.h",
        "drake_copyable.h",
        "drake_deprecated.h",
        "drake_optional.h",
        "drake_throw.h",
        "eigen_stl_types.h",
        "eigen_types.h",
        "never_destroyed.h",
        "text_logging.h",
    ],
    deps = [
        "//drake/thirdParty:stx",
        "@eigen",
        "@spdlog",
    ],
)

# Specific traits and operators that are relevant to all ScalarTypes.
drake_cc_library(
    name = "cond",
    srcs = ["cond.cc"],
    hdrs = ["cond.h"],
    deps = [
        ":double",
    ],
)

drake_cc_library(
    name = "dummy_value",
    hdrs = ["dummy_value.h"],
)

drake_cc_library(
    name = "number_traits",
    hdrs = ["number_traits.h"],
)

# Drake's specific ScalarType-providing libraries.
drake_cc_library(
    name = "double",
    srcs = ["double_overloads.cc"],
    hdrs = ["double_overloads.h"],
)

drake_cc_library(
    name = "autodiff",
    hdrs = [
        "autodiff_overloads.h",
        "eigen_autodiff_types.h",
    ],
    deps = [
        ":common",
        ":cond",
        ":dummy_value",
        ":eigen_autodiff_limits",
    ],
)

drake_cc_library(
    name = "eigen_autodiff_limits",
    hdrs = ["eigen_autodiff_limits.h"],
)

drake_cc_library(
    name = "extract_double",
    hdrs = ["extract_double.h"],
    deps = [
        ":common",
        ":nice_type_name",
        ":number_traits",
    ],
)

drake_cc_library(
    name = "hash",
    hdrs = ["hash.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "polynomial",
    srcs = ["polynomial.cc"],
    hdrs = [
        "polynomial.h",
        "trig_poly.h",
    ],
    deps = [
        ":autodiff",
        ":common",
    ],
)

drake_cc_library(
    name = "symbolic",
    # We only expose `symbolic.h` to the users of symbolic target and hide the
    # rest of the header files by adding them in `srcs` section.
    srcs = [
        "symbolic.cc",
        "symbolic_environment.cc",
        "symbolic_environment.h",
        "symbolic_expression.cc",
        "symbolic_expression.h",
        "symbolic_expression_cell.cc",
        "symbolic_expression_cell.h",
        "symbolic_expression_visitor.h",
        "symbolic_formula.cc",
        "symbolic_formula.h",
        "symbolic_formula_cell.cc",
        "symbolic_formula_cell.h",
        "symbolic_formula_visitor.h",
        "symbolic_monomial.cc",
        "symbolic_monomial.h",
        "symbolic_monomial_util.cc",
        "symbolic_monomial_util.h",
        "symbolic_polynomial.cc",
        "symbolic_polynomial.h",
        "symbolic_variable.cc",
        "symbolic_variable.h",
        "symbolic_variables.cc",
        "symbolic_variables.h",
    ],
    hdrs = [
        "symbolic.h",
    ],
    deps = [
        ":common",
        ":cond",
        ":dummy_value",
        ":hash",
        ":number_traits",
        ":polynomial",
        "//drake/math:matrix_util",
    ],
)

drake_cc_library(
    name = "symbolic_test_util",
    testonly = 1,
    hdrs = [
        "test/symbolic_test_util.h",
    ],
    deps = [
        ":symbolic",
    ],
)

# Miscellaneous utilities.

DRAKE_RESOURCE_SENTINEL = "//:.drake-resource-sentinel"

drake_cc_library(
    name = "find_resource",
    srcs = ["find_resource.cc"],
    hdrs = ["find_resource.h"],
    data = [
        DRAKE_RESOURCE_SENTINEL,
    ],
    deps = [
        ":common",
        "//drake/thirdParty:spruce",
    ],
)

drake_cc_library(
    name = "drake_path",
    srcs = ["drake_path_bazel.cc"],
    hdrs = ["drake_path.h"],
    data = [
        DRAKE_RESOURCE_SENTINEL,
    ],
    visibility = ["//drake:__pkg__"],
    deps = [
        ":common",
        ":find_resource",
        "//drake/thirdParty:spruce",
    ],
)

# TODO(jwnimmer-tri) Move this header file into test/ subdirectory (and this
# stanza below the "test/" comment marker).
drake_cc_library(
    name = "eigen_matrix_compare",
    testonly = 1,
    hdrs = ["eigen_matrix_compare.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "is_approx_equal_abstol",
    hdrs = ["is_approx_equal_abstol.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "is_dynamic_castable",
    testonly = 1,
    hdrs = ["test/is_dynamic_castable.h"],
    deps = [
        ":nice_type_name",
    ],
)

drake_cc_library(
    name = "is_memcpy_movable",
    testonly = 1,
    hdrs = ["test/is_memcpy_movable.h"],
)

drake_cc_library(
    name = "nice_type_name",
    srcs = ["nice_type_name.cc"],
    hdrs = ["nice_type_name.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "is_cloneable",
    srcs = [],
    hdrs = ["is_cloneable.h"],
)

drake_cc_library(
    name = "copyable_unique_ptr",
    srcs = [],
    hdrs = ["copyable_unique_ptr.h"],
    deps = [":is_cloneable"],
)

drake_cc_library(
    name = "reinit_after_move",
    hdrs = ["reinit_after_move.h"],
)

drake_cc_library(
    name = "sorted_vectors_have_intersection",
    hdrs = ["sorted_vectors_have_intersection.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "text_logging_gflags",
    hdrs = ["text_logging_gflags.h"],
    # TODO(jwnimmer-tri) Ideally, gflags BUILD would do this for us.  Figure
    # out what's going on.  Definitely don't let "-pthread" get copy-pasta'd
    # throughout our code.
    linkopts = select({
        "//tools:linux": ["-pthread"],
        "//conditions:default": [],
    }),
    deps = [
        ":common",
        "@com_github_gflags_gflags//:gflags",
    ],
)

drake_cc_library(
    name = "type_safe_index",
    hdrs = ["type_safe_index.h"],
    deps = [
        ":common",
        ":nice_type_name",
    ],
)

drake_cc_library(
    name = "unused",
    hdrs = ["unused.h"],
    deps = [
        ":common",
    ],
)

drake_cc_library(
    name = "scoped_singleton",
    hdrs = ["scoped_singleton.h"],
    deps = [
        ":common",
    ],
)

drake_cc_binary(
    name = "resource_tool",
    srcs = ["resource_tool.cc"],
    deps = [
        ":common",
        ":find_resource",
        ":text_logging_gflags",
    ],
)

install(
    name = "install",
    targets = [":resource_tool"],
    # TODO(jwnimmer-tri) The install rule should offer more specific options
    # for putting programs into libexec and including the workspace and/or
    # package name in the installed path.  For now, we'll just specify it
    # manually.
    runtime_dest = "libexec/drake/drake/common",
    data_dest = "share/drake",
    guess_data = "WORKSPACE",
    allowed_externals = [DRAKE_RESOURCE_SENTINEL],
)

# === test/ ===

drake_cc_library(
    name = "random_polynomial_matrix",
    testonly = 1,
    hdrs = ["test/random_polynomial_matrix.h"],
    deps = [
        ":polynomial",
    ],
)

drake_cc_library(
    name = "measure_execution",
    testonly = 1,
    hdrs = ["test/measure_execution.h"],
)

drake_cc_googletest(
    name = "autodiff_overloads_test",
    deps = [
        ":autodiff",
        ":common",
        ":eigen_matrix_compare",
        ":extract_double",
    ],
)

drake_cc_googletest(
    name = "reinit_after_move_test",
    deps = [
        ":reinit_after_move",
    ],
)

drake_cc_googletest(
    name = "cond_test",
    deps = [
        ":cond",
    ],
)

drake_cc_googletest(
    name = "double_overloads_test",
    deps = [
        ":common",
        ":cond",
        ":double",
    ],
)

# Functional test of DRAKE_ASSERT at runtime.
drake_cc_googletest(
    name = "drake_assert_test",
    deps = [
        ":common",
    ],
)

# Same, but with assertions forced enabled.
drake_cc_googletest(
    name = "drake_assert_test_enabled",
    srcs = ["test/drake_assert_test.cc"],
    copts = [
        "-DDRAKE_ENABLE_ASSERTS",
        "-UDRAKE_DISABLE_ASSERTS",
    ],
    deps = [
        ":common",
    ],
)

# Same, but with assertions forced disabled.
drake_cc_googletest(
    name = "drake_assert_test_disabled",
    srcs = ["test/drake_assert_test.cc"],
    copts = [
        "-UDRAKE_ENABLE_ASSERTS",
        "-DDRAKE_DISABLE_ASSERTS",
    ],
    deps = [
        ":common",
    ],
)

# Functional test of DRAKE_ASSERT at compile time.
drake_cc_googletest(
    name = "drake_assert_test_compile",
    deps = [
        ":common",
        ":unused",
    ],
)

# Needed by :drake_assert_test_compile_variants.
genrule(
    name = "capture_cc",
    outs = ["capture_cc.env"],
    cmd = "echo \"BAZEL_CC=$(CC)\" > '$@'",
    visibility = ["//visibility:private"],
)

# Functional test that mistyped DRAKE_ASSERTs will failt to compile.
sh_test(
    name = "drake_assert_test_compile_variants",
    srcs = ["test/drake_assert_test_compile_variants.sh"],
    data = [
        "capture_cc.env",
        "drake_assert.h",
        "drake_compat.h",
        "test/drake_assert_test_compile.cc",
        "unused.h",
        "//tools:third_party/bazel/tools/cpp/osx_cc_wrapper.sh",
    ],
)

drake_cc_googletest(
    name = "is_cloneable_test",
    deps = [
        ":is_cloneable",
    ],
)

drake_cc_googletest(
    name = "copyable_unique_ptr_test",
    deps = [
        ":copyable_unique_ptr",
        ":is_dynamic_castable",
    ],
)

drake_cc_googletest(
    name = "drake_deprecated_test",
    # Remove spurious warnings from the default build output.
    copts = ["-Wno-deprecated-declarations"],
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "drake_optional_test",
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "drake_throw_test",
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "dummy_value_test",
    deps = [
        ":dummy_value",
    ],
)

drake_cc_googletest(
    name = "eigen_matrix_compare_test",
    deps = [
        ":common",
        ":eigen_matrix_compare",
    ],
)

drake_cc_googletest(
    name = "eigen_stl_types_test",
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "eigen_types_test",
    deps = [
        ":common",
        ":nice_type_name",
    ],
)

drake_cc_googletest(
    name = "extract_double_test",
    deps = [
        ":common",
        ":extract_double",
    ],
)

drake_cc_googletest(
    name = "find_resource_test",
    data = [
        "test/find_resource_test_data.txt",
    ],
    deps = [
        ":find_resource",
    ],
)

drake_cc_googletest(
    name = "is_approx_equal_abstol_test",
    deps = [
        ":common",
        ":is_approx_equal_abstol",
    ],
)

drake_cc_googletest(
    name = "symbolic_monomial_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "never_destroyed_test",
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "nice_type_name_test",
    deps = [
        ":common",
        ":nice_type_name",
    ],
)

drake_cc_googletest(
    name = "is_dynamic_castable_test",
    deps = [
        ":is_dynamic_castable",
    ],
)

drake_cc_googletest(
    name = "is_memcpy_movable_test",
    deps = [
        ":is_memcpy_movable",
    ],
)

drake_cc_googletest(
    name = "polynomial_test",
    deps = [
        ":common",
        ":eigen_matrix_compare",
        ":random_polynomial_matrix",
    ],
)

drake_cc_googletest(
    name = "sorted_vectors_have_intersection_test",
    deps = [
        ":common",
        ":sorted_vectors_have_intersection",
    ],
)

drake_cc_googletest(
    name = "symbolic_environment_test",
    deps = [
        ":common",
        ":symbolic",
    ],
)

drake_cc_googletest(
    name = "symbolic_expansion_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_test",
    deps = [
        ":common",
        ":is_memcpy_movable",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_differentiation_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_jacobian_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_array_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_matrix_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_expression_transform_test",
    deps = [
        ":common",
        ":symbolic",
        "//drake/math:geometric_transform",
    ],
)

drake_cc_googletest(
    name = "symbolic_mixing_scalar_types_test",
    deps = [
        ":common",
        ":symbolic",
    ],
)

drake_cc_googletest(
    name = "symbolic_polynomial_test",
    # Test size increased to not timeout when run with Valgrind.
    size = "medium",
    deps = [
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_polynomial_matrix_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_substitution_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_variable_overloading_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_formula_test",
    deps = [
        ":common",
        ":is_memcpy_movable",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_formula_visitor_test",
    deps = [
        ":common",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_variable_test",
    deps = [
        ":common",
        ":is_memcpy_movable",
        ":symbolic",
        ":symbolic_test_util",
    ],
)

drake_cc_googletest(
    name = "symbolic_variables_test",
    deps = [
        ":common",
        ":symbolic",
    ],
)

drake_cc_googletest(
    name = "text_logging_test",
    deps = [
        ":common",
    ],
)

drake_cc_googletest(
    name = "trig_poly_test",
    deps = [
        ":common",
        ":polynomial",
    ],
)

drake_cc_googletest(
    name = "type_safe_index_test",
    deps = [
        ":type_safe_index",
        ":unused",
    ],
)

drake_cc_googletest(
    name = "eigen_autodiff_types_test",
    deps = [":autodiff"],
)

drake_cc_googletest(
    name = "scoped_singleton_test",
    deps = [
        ":scoped_singleton",
    ],
)

py_test(
    name = "resource_tool_test",
    srcs = ["test/resource_tool_test.py"],
    data = [
        "test/resource_tool_test_data.txt",
        ":resource_tool",
        "//drake/examples/pendulum:models",
    ],
)

py_test(
    name = "resource_tool_installed_test",
    srcs = ["test/resource_tool_installed_test.py"],
    data = [
        ":install",
    ],
)

# TODO(jwnimmer-tri) These tests are currently missing...
# - drake_assert_test in fancy variants
# - drake_assert_test_compile in fancy variants
# - text_logging_test in fancy variants
# - drake_deprecated_test in fancy variants
# - cpplint_wrapper_test.py

add_lint_tests()
