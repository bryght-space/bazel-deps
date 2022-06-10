workspace(name = "com_github_johnynek_bazel_deps")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl",
     "git_repository", "new_git_repository")

git_repository(
    name = "io_bazel_rules_scala",
    remote = "https://github.com/bazelbuild/rules_scala",
    commit = "a676633dc14d8239569affb2acafbef255df3480" # HEAD as of 2020-01-15, update this as needed
)

http_archive(
    name = "rules_proto",
    sha256 = "e017528fd1c91c5a33f15493e3a398181a9e821a804eb7ff5acdd1d2d6c2b18d",
    strip_prefix = "rules_proto-4.0.0-3.20.0",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/4.0.0-3.20.0.tar.gz",
    ],
)

http_archive(
    name = "bazel_skylib",
    sha256 = "7832382668c6dde9f57e18923763a24f9087cac66a50fbcc5afca848d03f2aa1",
    strip_prefix = "bazel-skylib-b113ed5d05ccddee3093bb157b9b02ab963c1c32",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/b113ed5d05ccddee3093bb157b9b02ab963c1c32.tar.gz"],
)

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()
rules_proto_toolchains()


load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")
scala_repositories()
register_toolchains("//:scala_toolchain")

load("//3rdparty:workspace.bzl", "maven_dependencies")

maven_dependencies()


load("//3rdparty:target_file.bzl", "build_external_workspace")
build_external_workspace(name = "third_party")
bind(name = 'io_bazel_rules_scala/dependency/scalatest/scalatest', actual = '//3rdparty/jvm/org/scalatest')
