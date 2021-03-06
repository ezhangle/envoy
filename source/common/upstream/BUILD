licenses(["notice"])  # Apache 2

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "cds_api_lib",
    srcs = ["cds_api_impl.cc"],
    hdrs = ["cds_api_impl.h"],
    deps = [
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/json:json_object_interface",
        "//include/envoy/local_info:local_info_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
        "//source/common/http:headers_lib",
        "//source/common/http:rest_api_fetcher_lib",
        "//source/common/json:config_schemas_lib",
        "//source/common/json:json_loader_lib",
    ],
)

envoy_cc_library(
    name = "cluster_manager_lib",
    srcs = ["cluster_manager_impl.cc"],
    hdrs = ["cluster_manager_impl.h"],
    deps = [
        ":cds_api_lib",
        ":load_balancer_lib",
        ":ring_hash_lb_lib",
        ":sds_lib",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/http:codes_interface",
        "//include/envoy/local_info:local_info_interface",
        "//include/envoy/network:dns_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/thread_local:thread_local_interface",
        "//include/envoy/upstream:cluster_manager_interface",
        "//source/common/common:enum_to_int",
        "//source/common/common:utility_lib",
        "//source/common/http:async_client_lib",
        "//source/common/http/http1:conn_pool_lib",
        "//source/common/http/http2:conn_pool_lib",
        "//source/common/json:config_schemas_lib",
        "//source/common/json:json_loader_lib",
        "//source/common/router:shadow_writer_lib",
    ],
)

envoy_cc_library(
    name = "health_checker_lib",
    srcs = ["health_checker_impl.cc"],
    hdrs = ["health_checker_impl.h"],
    deps = [
        ":host_utility_lib",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/http:codec_interface",
        "//include/envoy/http:codes_interface",
        "//include/envoy/network:connection_interface",
        "//include/envoy/network:filter_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/stats:stats_interface",
        "//include/envoy/upstream:health_checker_interface",
        "//source/common/buffer:buffer_lib",
        "//source/common/common:empty_string",
        "//source/common/common:enum_to_int",
        "//source/common/common:hex_lib",
        "//source/common/common:logger_lib",
        "//source/common/common:utility_lib",
        "//source/common/http:codec_client_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http:headers_lib",
        "//source/common/http:utility_lib",
        "//source/common/json:json_loader_lib",
        "//source/common/network:filter_lib",
    ],
)

envoy_cc_library(
    name = "host_utility_lib",
    srcs = ["host_utility.cc"],
    hdrs = ["host_utility.h"],
    deps = ["//include/envoy/upstream:upstream_interface"],
)

envoy_cc_library(
    name = "load_balancer_lib",
    srcs = ["load_balancer_impl.cc"],
    hdrs = ["load_balancer_impl.h"],
    deps = [
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/stats:stats_interface",
        "//include/envoy/upstream:load_balancer_interface",
        "//include/envoy/upstream:upstream_interface",
        "//source/common/common:assert_lib",
    ],
)

envoy_cc_library(
    name = "logical_dns_cluster_lib",
    srcs = ["logical_dns_cluster.cc"],
    hdrs = ["logical_dns_cluster.h"],
    deps = [
        ":upstream_includes",
        "//include/envoy/thread_local:thread_local_interface",
        "//source/common/common:empty_string",
        "//source/common/network:address_lib",
        "//source/common/network:utility_lib",
    ],
)

envoy_cc_library(
    name = "outlier_detection_lib",
    srcs = ["outlier_detection_impl.cc"],
    hdrs = ["outlier_detection_impl.h"],
    deps = [
        "//include/envoy/access_log:access_log_interface",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/upstream:outlier_detection_interface",
        "//include/envoy/upstream:upstream_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:utility_lib",
        "//source/common/http:codes_lib",
        "//source/common/json:json_loader_lib",
    ],
)

envoy_cc_library(
    name = "resource_manager_lib",
    hdrs = ["resource_manager_impl.h"],
    deps = [
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/upstream:resource_manager_interface",
        "//source/common/common:assert_lib",
    ],
)

envoy_cc_library(
    name = "ring_hash_lb_lib",
    srcs = ["ring_hash_lb.cc"],
    hdrs = ["ring_hash_lb.h"],
    deps = [
        ":load_balancer_lib",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/upstream:load_balancer_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:logger_lib",
    ],
)

envoy_cc_library(
    name = "sds_lib",
    srcs = ["sds.cc"],
    hdrs = ["sds.h"],
    deps = [
        ":upstream_includes",
        "//include/envoy/local_info:local_info_interface",
        "//source/common/http:headers_lib",
        "//source/common/http:rest_api_fetcher_lib",
        "//source/common/json:config_schemas_lib",
        "//source/common/network:address_lib",
        "//source/common/network:utility_lib",
    ],
)

envoy_cc_library(
    name = "upstream_lib",
    srcs = ["upstream_impl.cc"],
    deps = [
        ":health_checker_lib",
        ":logical_dns_cluster_lib",
        ":sds_lib",
        ":upstream_includes",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:timer_interface",
        "//include/envoy/network:dns_interface",
        "//include/envoy/ssl:context_interface",
        "//include/envoy/upstream:health_checker_interface",
        "//source/common/common:enum_to_int",
        "//source/common/common:utility_lib",
        "//source/common/http:utility_lib",
        "//source/common/json:config_schemas_lib",
        "//source/common/json:json_loader_lib",
        "//source/common/network:address_lib",
        "//source/common/network:utility_lib",
        "//source/common/ssl:connection_lib",
        "//source/common/ssl:context_config_lib",
    ],
)

envoy_cc_library(
    name = "upstream_includes",
    hdrs = ["upstream_impl.h"],
    deps = [
        ":outlier_detection_lib",
        ":resource_manager_lib",
        "//include/envoy/event:timer_interface",
        "//include/envoy/local_info:local_info_interface",
        "//include/envoy/network:dns_interface",
        "//include/envoy/runtime:runtime_interface",
        "//include/envoy/ssl:context_manager_interface",
        "//include/envoy/thread_local:thread_local_interface",
        "//include/envoy/upstream:cluster_manager_interface",
        "//include/envoy/upstream:health_checker_interface",
        "//include/envoy/upstream:load_balancer_interface",
        "//include/envoy/upstream:upstream_interface",
        "//source/common/common:enum_to_int",
        "//source/common/common:logger_lib",
        "//source/common/stats:stats_lib",
    ],
)
