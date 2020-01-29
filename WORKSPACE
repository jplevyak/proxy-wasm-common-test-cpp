workspace(name = "common_wasm_test_cpp")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository", "new_git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
  name = 'emscripten_toolchain',
  url = 'https://github.com/emscripten-core/emsdk/archive/a5082b232617c762cb65832429f896c838df2483.tar.gz',
  build_file = '//bazel/external:emscripten-toolchain.BUILD',
  strip_prefix = "emsdk-a5082b232617c762cb65832429f896c838df2483",
  patch_cmds = [
      "./emsdk install 1.39.0-upstream",
      "./emsdk activate --embedded 1.39.0-upstream",
  ]
)

http_archive(
    name = "bazel_skylib",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.0.2/bazel-skylib-1.0.2.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.0.2/bazel-skylib-1.0.2.tar.gz",
    ],
    sha256 = "97e70364e9249702246c0e9444bccdc4b847bed1eb03c5a3ece4f83dfe6abc44",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

# this must be named com_google_protobuf to match dependency pulled in by
# rules_proto.
git_repository(
    name = "com_google_protobuf",
    remote = "https://github.com/protocolbuffers/protobuf",
    commit = "655310ca192a6e3a050e0ca0b7084a2968072260",
)

new_git_repository(
    name = "envoy_wasm_api",
    remote = "https://github.com/envoyproxy/envoy-wasm",
    commit = "49f411875801c85fc25b869da77ef98cde3f7f65",
    workspace_file_content = 'workspace(name = "envoy_wasm_api")',
    strip_prefix = "api/wasm/cpp",
    patch_cmds = ["rm BUILD"],
    build_file = '//bazel/external:envoy-wasm-api.BUILD',
)

http_archive(
    name = "rules_proto",
    sha256 = "602e7161d9195e50246177e7c55b2f39950a9cf7366f74ed5f22fd45750cd208",
    strip_prefix = "rules_proto-97d8af4dc474595af3900dd85cb3a29ad28cc313",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
        "https://github.com/bazelbuild/rules_proto/archive/97d8af4dc474595af3900dd85cb3a29ad28cc313.tar.gz",
    ],
)
load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()
