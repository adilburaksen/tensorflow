load("@rules_cc//cc:cc_library.bzl", "cc_library")
load("//xla/tsl:tsl.bzl", "if_oss")
load("//xla/tsl/platform:build_config.bzl", "tsl_cc_test")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    default_visibility = [
        "//visibility:public",
    ],
    licenses = ["notice"],
)

cc_library(
    name = "builddata",
    srcs = if_oss(
        [
            "builddata_globals.h",
            "utils.h",
            "//xla/tsl/platform/default:builddata_srcs",
        ],
        google_value = [
            "//xla/tsl/platform/google:builddata_srcs",
        ],
    ),
    hdrs = [
        "builddata.h",
    ],
    linkstamp = if_oss(
        "builddata_globals.cc",
        google_value = None,
    ),
    deps = [
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/strings:string_view",
        "@com_google_absl//absl/time",
    ] + if_oss(
        [
            "//xla/tsl/platform:logging",
        ],
        google_value = [
            "@com_google_absl//absl/base:builddata",
        ],
    ),
)

tsl_cc_test(
    name = "test_stamping",
    srcs = [
        "test_stamping.cc",
        "utils.h",
    ],
    deps = [
        ":builddata",
        "//xla/tsl/platform:logging",
        "@com_google_absl//absl/strings",
        "@com_google_googletest//:gtest_main",
    ],
)
