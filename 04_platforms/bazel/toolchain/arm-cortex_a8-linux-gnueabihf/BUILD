package(default_visibility = ["//visibility:public"])

load(":cc_toolchain_config.bzl", "cc_toolchain_config")

filegroup(name = "empty")

filegroup(
  name = 'wrappers',
  srcs = glob([
    'wrappers/**',
  ]),
)

filegroup(
  name = 'all_files',
  srcs = [
    '@arm-buildroot-linux-gnueabihf-sysroot//:sysroot',
    '@arm-cortex_a8-linux-gnueabihf//:toolchain',
    ':wrappers',
  ],
)

cc_toolchain_config(name = "armv7_toolchain_config")

cc_toolchain(
    name = "armv7_toolchain",
    toolchain_identifier = "armv7-toolchain",
    toolchain_config = ":armv7_toolchain_config",
    all_files = ":all_files",
    compiler_files = ":all_files",
    dwp_files = ":empty",
    linker_files = ":all_files",
    objcopy_files = ":empty",
    strip_files = ":empty",
)

cc_toolchain_suite(
    name = "gcc_toolchain",
    toolchains = {
        "armv7": "//bazel/toolchain/arm-cortex_a8-linux-gnueabihf:armv7_toolchain",
    },
    tags = ["manual"]
)

toolchain(
    name = "armv7_linux_toolchain",
    exec_compatible_with = [
        "@platforms//os:linux",
        "@platforms//cpu:x86_64",
    ],
    target_compatible_with = [
        "@platforms//os:linux",
        "@platforms//cpu:armv7",
    ],
    toolchain = ":armv7_toolchain",
    toolchain_type = "@bazel_tools//tools/cpp:toolchain_type",
)
