load("@bazel_skylib//rules:expand_template.bzl", "expand_template")
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_application(
    name = "Mastodon",
    bundle_id = "org.joinmastodon.app",
    entitlements = "Mastodon.entitlements",
    extensions = [
        "//MastodonIntent",
        "//NotificationService",
        "//OpenInActionExtension",
        "//ShareActionExtension",
        "//WidgetExtension",
    ],
    families = [
        "ipad",
        "iphone",
    ],
    infoplists = [":InfoPlist"],
    minimum_os_version = "16.0",
    resources = glob(
        [
            "Resources/**",
            "Supporting Files/**",
        ],
        exclude = [
            ".*",
            "Resources/Preview Assets.xcassets",
        ],
    ),
    visibility = ["//visibility:public"],
    deps = [":Mastodon.library"],
)

swift_library(
    name = "Mastodon.library",
    srcs = glob(["**/*.swift"]) + [
        "//MastodonIntent:Intents.intent",
        "//WidgetExtension:WidgetExtension.intent",
    ],
    module_name = "Mastodon",
    visibility = ["//MastodonTests:__pkg__"],
    deps = [
        "@swiftpkg_kanna//:Kanna",
        "@swiftpkg_mastodonsdk//:MastodonSDKDynamic",
        "@swiftpkg_mbprogresshud//:MBProgressHUD",
    ],
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
