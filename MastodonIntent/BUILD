load("@bazel_skylib//rules:expand_template.bzl", "expand_template")
load("@build_bazel_rules_apple//apple:ios.bzl", "ios_extension")
load("@build_bazel_rules_apple//apple:resources.bzl", "apple_intent_library")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

ios_extension(
    name = "MastodonIntent",
    bundle_id = "org.joinmastodon.app.MastodonIntent",
    entitlements = "MastodonIntent.entitlements",
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
    deps = [":MastodonIntent.library"],
)

swift_library(
    name = "MastodonIntent.library",
    srcs = glob(["**/*.swift"]) + [
        ":Intents.intent",
        "//WidgetExtension:WidgetExtension.intent",
    ],
    copts = ["-application-extension"],
    module_name = "MastodonIntent",
    deps = ["@swiftpkg_mastodonsdk//:MastodonSDKDynamic"],
)

apple_intent_library(
    name = "Intents.intent",
    src = "Base.lproj/Intents.intentdefinition",
    language = "Swift",
    visibility = ["//visibility:public"],
)

expand_template(
    name = "InfoPlist",
    out = "Bazel.Info.plist",
    substitutions = {
        "$(CURRENT_PROJECT_VERSION)": "1",
        "$(MARKETING_VERSION)": "2024.3",
        "$(PRODUCT_MODULE_NAME)": "MastodonIntent",
    },
    template = "Info.plist",
)
