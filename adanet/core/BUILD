# Description:
# Core AdaNet logic.

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

whitelist = [
    "//adanet:__subpackages__",
]

py_library(
    name = "core",
    srcs = ["__init__.py"],
    visibility = whitelist,
    deps = [
        ":ensemble_builder",
        ":estimator",
        ":evaluator",
        ":report_materializer",
        ":summary",
        ":tpu_estimator",
    ],
)

py_library(
    name = "estimator",
    srcs = ["estimator.py"],
    visibility = ["//adanet/keras:__subpackages__"],
    deps = [
        ":architecture",
        ":candidate",
        ":ensemble_builder",
        ":eval_metrics",
        ":iteration",
        ":report_accessor",
        ":summary",
        ":timer",
        "//adanet/distributed",
        "//adanet/distributed:devices",
        "//adanet/ensemble",
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
        "@six_archive//:six",
    ],
)

py_test(
    name = "estimator_test",
    size = "large",
    srcs = ["estimator_test.py"],
    shard_count = 41,
    deps = [
        ":ensemble_builder",
        ":estimator",
        ":evaluator",
        ":report_materializer",
        ":testing_utils",
        "//adanet/replay",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_test(
    name = "estimator_v2_test",
    size = "large",
    srcs = ["estimator_v2_test.py"],
    shard_count = 2,
    deps = [
        ":ensemble_builder",
        ":estimator",
        ":evaluator",
        ":report_materializer",
        ":testing_utils",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_test(
    name = "estimator_distributed_test",
    size = "large",
    srcs = ["estimator_distributed_test.py"],
    data = [
        ":estimator_distributed_test_runner" +
        "",
    ],
    # Transient gRPC server errors when calling train_and_evaluate.
    flaky = 1,
    shard_count = 16,
    deps = [
        ":estimator",
        ":timer",
        "//adanet/subnetwork",
        "@absl_py//absl/logging",
        "@absl_py//absl/testing:parameterized",
    ],
)

# Subprocess binary for estimator_distributed_test.
py_binary(
    name = "estimator_distributed_test_runner",
    testonly = 1,
    srcs = ["estimator_distributed_test_runner.py"],
    python_version = "PY3",
    srcs_version = "PY2AND3",
    deps = [
        ":estimator",
        "//adanet/autoensemble",
        "//adanet/distributed",
        "//adanet/subnetwork",
        "@absl_py//absl:app",
        "@absl_py//absl/testing:absltest",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "tpu_estimator",
    srcs = ["tpu_estimator.py"],
    deps = [
        ":estimator",
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
    ],
)

py_test(
    name = "tpu_estimator_test",
    srcs = ["tpu_estimator_test.py"],
    shard_count = 10,
    deps = [
        ":testing_utils",
        ":tpu_estimator",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "candidate",
    srcs = ["candidate.py"],
    deps = [
        "//adanet/tf_compat",
    ],
)

py_test(
    name = "candidate_test",
    srcs = ["candidate_test.py"],
    deps = [
        ":candidate",
        ":testing_utils",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "iteration",
    srcs = ["iteration.py"],
    deps = [
        ":ensemble_builder",
        ":eval_metrics",
        "//adanet/distributed",
        "//adanet/subnetwork",
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
    ],
)

py_test(
    name = "iteration_test",
    srcs = ["iteration_test.py"],
    deps = [
        ":architecture",
        ":candidate",
        ":ensemble_builder",
        ":iteration",
        ":summary",
        ":testing_utils",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "evaluator",
    srcs = ["evaluator.py"],
    deps = [
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
    ],
)

py_test(
    name = "evaluator_test",
    srcs = ["evaluator_test.py"],
    deps = [
        ":candidate",
        ":ensemble_builder",
        ":evaluator",
        ":testing_utils",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "ensemble_builder",
    srcs = ["ensemble_builder.py"],
    deps = [
        ":architecture",
        ":eval_metrics",
        ":summary",
        "//adanet/ensemble",
        "//adanet/subnetwork",
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
    ],
)

py_test(
    name = "ensemble_builder_test",
    srcs = ["ensemble_builder_test.py"],
    shard_count = 10,
    deps = [
        ":architecture",
        ":ensemble_builder",
        ":summary",
        ":testing_utils",
        "//adanet/ensemble",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "eval_metrics",
    srcs = ["eval_metrics.py"],
    deps = [
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
        "@six_archive//:six",
    ],
)

py_test(
    name = "eval_metrics_test",
    srcs = ["eval_metrics_test.py"],
    deps = [
        ":architecture",
        ":candidate",
        ":ensemble_builder",
        ":eval_metrics",
        ":testing_utils",
        "//adanet/tf_compat",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "summary",
    srcs = ["summary.py"],
    deps = [
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
        "@six_archive//:six",
    ],
)

py_test(
    name = "summary_test",
    srcs = ["summary_test.py"],
    deps = [
        ":summary",
        ":testing_utils",
        "@absl_py//absl/testing:parameterized",
        "@six_archive//:six",
    ],
)

py_test(
    name = "summary_v2_test",
    srcs = ["summary_v2_test.py"],
    deps = [
        ":summary",
        ":testing_utils",
        "@absl_py//absl/testing:parameterized",
        "@six_archive//:six",
    ],
)

py_library(
    name = "timer",
    srcs = ["timer.py"],
)

py_test(
    name = "timer_test",
    srcs = ["timer_test.py"],
    deps = [
        ":timer",
    ],
)

py_library(
    name = "testing_utils",
    testonly = 1,
    srcs = ["testing_utils.py"],
    visibility = whitelist,
    deps = [
        ":architecture",
        ":candidate",
        ":ensemble_builder",
        ":eval_metrics",
        "//adanet/ensemble",
        "//adanet/subnetwork",
        "//adanet/tf_compat",
        "@absl_py//absl/flags",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "report_accessor",
    srcs = ["report_accessor.py"],
    deps = [
        "//adanet/subnetwork",
        "@absl_py//absl/logging",
        "@six_archive//:six",
    ],
)

py_test(
    name = "report_accessor_test",
    srcs = ["report_accessor_test.py"],
    deps = [
        ":report_accessor",
        "//adanet/subnetwork",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "report_materializer",
    srcs = ["report_materializer.py"],
    deps = [
        "//adanet/subnetwork",
        "//adanet/tf_compat",
        "@absl_py//absl/logging",
    ],
)

py_test(
    name = "report_materializer_test",
    srcs = ["report_materializer_test.py"],
    deps = [
        ":report_materializer",
        ":testing_utils",
        "//adanet/subnetwork",
        "//adanet/tf_compat",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "architecture",
    srcs = ["architecture.py"],
)

py_test(
    name = "architecture_test",
    srcs = ["architecture_test.py"],
    deps = [
        ":architecture",
        "@absl_py//absl/testing:parameterized",
    ],
)
