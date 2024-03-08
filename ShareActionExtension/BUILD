load("@bazel_skylib//rules:expand_template.bzl", "expand_template")
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_extension")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_extension(
    name = "ShareActionExtension",
    bundle_id = "org.joinmastodon.app.ShareActionExtension",
    entitlements = "ShareActionExtension.entitlements",
    families = [
        "ipad",
        "iphone",
    ],
    infoplists = [":InfoPlist"],
    minimum_os_version = "16.0",
    resources = glob(
        [
            "**/*.lproj/**",
            "**/*.js",
            "**/*.xcassets/**",
        ],
        exclude = [".*"],
    ),
    visibility = ["//visibility:public"],
    deps = [":ShareActionExtension.library"],
)

swift_library(
    name = "ShareActionExtension.library",
    srcs = glob(["**/*.swift"]),
    copts = ["-application-extension"],
    module_name = "ShareActionExtension",
    deps = ["@swiftpkg_mastodonsdk//:MastodonSDKDynamic"],
)

expand_template(
    name = "InfoPlist",
    out = "Bazel.Info.plist",
    substitutions = {
        "$(CURRENT_PROJECT_VERSION)": "1",
        "$(MARKETING_VERSION)": "2024.3",
    },
    template = "Info.plist",
)
