load("@bazel_skylib//rules:expand_template.bzl", "expand_template")
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_extension")
load("@build_bazel_rules_apple//apple:resources.bzl", "apple_intent_library")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_extension(
    name = "WidgetExtension",
    bundle_id = "org.joinmastodon.app.WidgetExtension",
    entitlements = "WidgetExtension.entitlements",
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
    deps = [":WidgetExtension.library"],
)

swift_library(
    name = "WidgetExtension.library",
    srcs = glob(["**/*.swift"]) + [":WidgetExtension.intent"],
    copts = ["-application-extension"],
    module_name = "WidgetExtension",
    deps = [
        "@swiftpkg_lightchart//:LightChart",
        "@swiftpkg_mastodonsdk//:MastodonSDKDynamic",
    ],
)

apple_intent_library(
    name = "WidgetExtension.intent",
    src = "Base.lproj/WidgetExtension.intentdefinition",
    language = "Swift",
    visibility = ["//visibility:public"],
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
