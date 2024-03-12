load("@build_bazel_rules_apple//apple:ios.bzl", "ios_ui_test")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_ui_test(
    name = "MastodonUITests",
    bundle_id = "org.joinmastodon.MastodonUITests",
    minimum_os_version = "16.0",
    test_host = "//Mastodon:Mastodon",
    deps = [":MastodonUITests.library"],
)

swift_library(
    name = "MastodonUITests.library",
    srcs = glob(["**/*.swift"]),
    module_name = "MastodonUITests",
    testonly = True,
)
