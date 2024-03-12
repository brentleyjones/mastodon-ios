load("@build_bazel_rules_apple//apple:ios.bzl", "ios_unit_test")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_unit_test(
    name = "MastodonTests",
    bundle_id = "org.joinmastodon.MastodonTests",
    minimum_os_version = "16.0",
    test_host = "//Mastodon:Mastodon",
    deps = [":MastodonTests.library"],
)

swift_library(
    name = "MastodonTests.library",
    srcs = glob(["**/*.swift"]),
    module_name = "MastodonTests",
    testonly = True,
    deps = [
        "@swiftpkg_mastodonsdk//:MastodonSDKDynamic",
        "//Mastodon:Mastodon.library",
    ],
)
