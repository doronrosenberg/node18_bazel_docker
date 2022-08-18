load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Go (due to bug in docker)
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "16e9fca53ed6bd4ff4ad76facc9b7b651a89db1689a2877d6fd7b82aa824e366",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.18.3")

http_archive(
    name = "bazel_gazelle",
    sha256 = "501deb3d5695ab658e82f6f6f549ba681ea3ca2a5fb7911154b5aa45596183fa",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.26.0/bazel-gazelle-v0.26.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.26.0/bazel-gazelle-v0.26.0.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

# start of node docker
http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "b1e80761a8a8243d03ebca8845e9cc1ba6c82ce7c5179ce2b295cd36f7e394bf",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.25.0/rules_docker-v0.25.0.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:go_repositories.bzl",
    container_go_deps = "go_deps",
)

container_go_deps()

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load("@io_bazel_rules_docker//container:container.bzl", "container_pull")

container_pull(
    name = "alpine_linux_arm64",
    digest = "sha256:9b2a28eb47540823042a2ba401386845089bb7b62a9637d55816132c4c3c36eb",
    registry = "index.docker.io",
    repository = "library/alpine",
    # tag field is ignored since digest is set
    tag = "latest",
)

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "ee3280a7f58aa5c1caa45cb9e08cbb8f4d74300848c508374daf37314d5390d6",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/5.5.1/rules_nodejs-5.5.1.tar.gz"],
)

# load js rules
load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")

# register js
build_bazel_rules_nodejs_dependencies()

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

node_repositories(
    node_repositories = {
        "18.7.0-darwin_amd64": ("node-v18.7.0-darwin-x64.tar.gz", "node-v18.7.0-darwin-x64", "ce95b924b450edbcfeaf422b3635a6b44b17ad23cd1f5efff6b051c60db548c8"),
        "18.7.0-darwin_arm64": ("node-v18.7.0-darwin-x64.tar.gz", "node-v18.7.0-darwin-x64", "ce95b924b450edbcfeaf422b3635a6b44b17ad23cd1f5efff6b051c60db548c8"),
        "18.7.0-linux_amd64": ("node-v18.7.0-linux-x64.tar.xz", "node-v18.7.0-linux-x64", "8bc6a1b9deaed2586d726fc62d4bee9c1bfc5a30b96c1c4cff7edd15225a11a2"),
    },
    node_version = "18.7.0",
    yarn_version = "1.22.19",
)

load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = "18.7.0",
)

# old repo
load(
    "@io_bazel_rules_docker//nodejs:image.bzl",
    nodejs_image_repositories = "repositories",
)

nodejs_image_repositories()

# new repo
container_pull(
    name = "distroless_debian11",
    registry = "gcr.io",
    repository = "distroless/base-debian11:latest",
)