# Copyright 2016 Google Inc. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################
#

# http_archive is not a native function since bazel 0.19
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load(
    "//:repositories.bzl",
    "googletest_repositories",
    "mixerapi_dependencies",
)

googletest_repositories()

mixerapi_dependencies()

bind(
    name = "boringssl_crypto",
    actual = "//external:ssl",
)

# When updating envoy sha manually please update the sha in istio.deps file also
#
# Determine SHA256 `wget https://github.com/istio/envoy/archive/$COMMIT.tar.gz && sha256sum $COMMIT.tar.gz`
# envoy commit date: 11/21/2019
# bazel version: 0.28.1
ENVOY_SHA = "736646a180e1a7943e715ec98487c2d9848a455a"

ENVOY_SHA256 = "f4df297789788609ae2a44607a8a9535568282845ce44c02cdb7492ea7743d79"

LOCAL_ENVOY_PROJECT = "/PATH/TO/ENVOY"

http_archive(
    name = "envoy",
    sha256 = ENVOY_SHA256,
    strip_prefix = "envoy-" + ENVOY_SHA,
    url = "https://github.com/istio/envoy/archive/" + ENVOY_SHA + ".tar.gz",
)

# TODO(silentdai) Use bazel args to select envoy between local or http
# Uncomment below and comment above http_archive to depends on local envoy.
#local_repository(
#     name = "envoy",
#     path = LOCAL_ENVOY_PROJECT,
#)

load("@envoy//bazel:api_binding.bzl", "envoy_api_binding")

envoy_api_binding()

load("@envoy//bazel:api_repositories.bzl", "envoy_api_dependencies")

envoy_api_dependencies()

load("@envoy//bazel:repositories.bzl", "envoy_dependencies")

envoy_dependencies()

load("@envoy//bazel:dependency_imports.bzl", "envoy_dependency_imports")

envoy_dependency_imports()
