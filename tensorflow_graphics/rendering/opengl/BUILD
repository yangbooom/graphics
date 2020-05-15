# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#Copyright 2019 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# OpenGL functionalities for tf-graphics.

licenses(["notice"])  # Apache 2.0

package(default_visibility = ["//visibility:public"])

py_library(
    name = "opengl",
    srcs = [
        "__init__.py",
    ],
    data = [":rasterizer_op.so"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":math",
        # ":triangle_rasterizer",
        "//tensorflow_graphics/util:export_api",
    ],
)

cc_library(
    name = "EGL_headers",
    hdrs = [
        "EGL/egl.h",
        "EGL/eglext.h",
        "EGL/eglplatform.h",
        "KHR/khrplatform.h",
    ],
    defines = ["USE_OZONE"],
    features = [
        "-parse_headers",
    ],
    includes = ["."],
    linkopts = [
        "-Wl,-L/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-L/usr/lib/x86_64-linux-gnu",
        "-Wl,-lEGL",
        "-Wl,-lGLESv2",
    ],
)

cc_library(
    name = "egl_offscreen_context",
    srcs = ["egl_offscreen_context.cc"],
    hdrs = ["egl_offscreen_context.h"],
    deps = [
        ":EGL_headers",
        ":egl_util",
        ":macros",
        "//tensorflow_graphics/util:cleanup",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "egl_offscreen_context_test",
    srcs = ["tests/egl_offscreen_context_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":egl_offscreen_context",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "egl_util",
    srcs = ["egl_util.cc"],
    hdrs = ["egl_util.h"],
    visibility = ["//visibility:public"],
    deps = [
        ":EGL_headers",
    ],
)

cc_test(
    name = "egl_util_test",
    srcs = ["egl_util_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    deps = [
        ":EGL_headers",
        ":egl_util",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "macros",
    hdrs = ["macros.h"],
    visibility = ["//visibility:private"],
    deps = [
        ":EGL_headers",
        "@com_google_absl//absl/strings",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "gl_program",
    srcs = ["gl_program.cc"],
    hdrs = ["gl_program.h"],
    deps = [
        ":macros",
        "//tensorflow_graphics/util:cleanup",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "gl_program_test",
    srcs = ["tests/gl_program_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":egl_offscreen_context",
        ":gl_program",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "gl_render_targets",
    srcs = ["gl_render_targets.cc"],
    hdrs = ["gl_render_targets.h"],
    deps = [
        ":macros",
        "//tensorflow_graphics/util:cleanup",
        "@com_google_absl//absl/types:span",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "gl_render_targets_test",
    srcs = ["tests/gl_render_targets_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":egl_offscreen_context",
        ":gl_render_targets",
        ":macros",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "gl_shader_storage_buffer",
    srcs = ["gl_shader_storage_buffer.cc"],
    hdrs = ["gl_shader_storage_buffer.h"],
    deps = [
        ":macros",
        "//tensorflow_graphics/util:cleanup",
        "@com_google_absl//absl/types:span",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "gl_shader_storage_buffer_test",
    srcs = ["tests/gl_shader_storage_buffer_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":gl_shader_storage_buffer",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:libtensorflow_framework",
    ],
)

py_library(
    name = "math",
    srcs = ["math.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow_graphics/math:vector",
        "//tensorflow_graphics/math/interpolation:weighted",
        "//tensorflow_graphics/util:asserts",
        "//tensorflow_graphics/util:export_api",
        "//tensorflow_graphics/util:shape",
    ],
)

py_test(
    name = "math_test",
    timeout = "long",
    srcs = ["tests/math_test.py"],
    shard_count = 32,
    srcs_version = "PY2AND3",
    deps = [
        ":math",
        "//tensorflow_graphics/util:test_case",
    ],
)

cc_library(
    name = "rasterizer",
    srcs = ["rasterizer.cc"],
    hdrs = ["rasterizer.h"],
    deps = [
        ":gl_program",
        ":gl_render_targets",
        ":gl_shader_storage_buffer",
        "//tensorflow_graphics/util:cleanup",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "rasterizer_test",
    srcs = ["tests/rasterizer_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":egl_offscreen_context",
        ":rasterizer",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:libtensorflow_framework",
    ],
)

cc_library(
    name = "rasterizer_op_lib",
    srcs = ["rasterizer_op.cc"],
    deps = [
        ":macros",
        ":rasterizer_with_context",
        ":thread_safe_resource_pool",
        "//third_party/tensorflow/core:framework",
        "@com_google_absl//absl/types:span",
        "@local_config_tf//:tf_header_lib",
    ],
    alwayslink = 1,
)

cc_binary(
    name = "rasterizer_op.so",
    srcs = [
        "egl_offscreen_context.cc",
        "egl_offscreen_context.h",
        "egl_util.cc",
        "egl_util.h",
        "gl_program.cc",
        "gl_program.h",
        "gl_render_targets.cc",
        "gl_render_targets.h",
        "gl_shader_storage_buffer.cc",
        "gl_shader_storage_buffer.h",
        "macros.h",
        "rasterizer.cc",
        "rasterizer.h",
        "rasterizer_op.cc",
        "rasterizer_with_context.cc",
        "rasterizer_with_context.h",
        "thread_safe_resource_pool.h",
    ],
    linkopts = [
        "-Wl,-L/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-L/usr/lib/x86_64-linux-gnu",
        "-Wl,-lEGL",
        "-Wl,-lGLESv2",
    ],
    linkshared = 1,
    deps = [
        ":EGL_headers",
        "//tensorflow_graphics/util:cleanup",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/container:inlined_vector",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/synchronization",
        "@com_google_absl//absl/time",
        "@com_google_absl//absl/types:optional",
        "@com_google_absl//absl/types:span",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

py_test(
    name = "rasterizer_op_test",
    srcs = [
        "tests/rasterizer_op_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":math",
        ":opengl",
        "//tensorflow_graphics/util:test_case",
    ],
)

cc_library(
    name = "rasterizer_with_context",
    srcs = ["rasterizer_with_context.cc"],
    hdrs = ["rasterizer_with_context.h"],
    deps = [
        ":egl_offscreen_context",
        ":rasterizer",
        "//tensorflow_graphics/util:cleanup",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "rasterizer_with_context_test",
    srcs = ["tests/rasterizer_with_context_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    tags = [
        "nomsan",  # Un-initialized values in libEGL.
        "requires-gpu-nvidia",
    ],
    deps = [
        ":rasterizer_with_context",
        ":thread_safe_resource_pool",
        "@com_google_absl//absl/types:span",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_library(
    name = "thread_safe_resource_pool",
    hdrs = ["thread_safe_resource_pool.h"],
    deps = [
        ":macros",
        "@com_google_absl//absl/synchronization",
        "@local_config_tf//:tf_header_lib",
    ],
)

cc_test(
    name = "thread_safe_resource_pool_test",
    srcs = ["tests/thread_safe_resource_pool_test.cc"],
    linkopts = [
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu/mesa-egl",
        "-Wl,-rpath,/usr/lib/x86_64-linux-gnu",
    ],
    deps = [
        ":thread_safe_resource_pool",
        "@com_google_googletest//:gtest_main",
        "@local_config_tf//:libtensorflow_framework",
        "@local_config_tf//:tf_header_lib",
    ],
)

py_library(
    name = "triangle_rasterizer",
    srcs = ["triangle_rasterizer.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":math",
        ":opengl",
        "//tensorflow_graphics/util:export_api",
        "//tensorflow_graphics/util:shape",
    ],
)

py_test(
    name = "triangle_rasterizer_test",
    timeout = "long",
    srcs = ["tests/triangle_rasterizer_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":triangle_rasterizer",
        "//tensorflow_graphics/util:test_case",
    ],
)
