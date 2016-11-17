## cluster deployment
```
curl -X GET -u "admin:admin" http://54.245.27.236:7180/api/v13/cm/deployment
```

```
{
  "timestamp" : "2016-11-17T22:42:20.087Z",
  "clusters" : [ {
    "name" : "cluster",
    "displayName" : "Cluster 1",
    "version" : "CDH5",
    "fullVersion" : "5.8.3",
    "services" : [ {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "ip-10-0-60-244.us-west-2.compute.internal"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "admin"
        }, {
          "name" : "hive_metastore_database_user",
          "value" : "metastore"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-0f46b368249e95db1df5e7aee4ca51c6",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "f72fede6-24b6-4411-a3a5-942a1d8c29d3"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-GATEWAY-BASE"
        }
      }, {
        "name" : "hive-GATEWAY-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-GATEWAY-BASE"
        }
      }, {
        "name" : "hive-GATEWAY-3f5b4aee6670e33f6f10eb3ba2d13008",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "aae2b5ea-252d-4061-be5b-99cee9b93ab1"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-GATEWAY-BASE"
        }
      }, {
        "name" : "hive-GATEWAY-47ac12a07573a05c9569413a68f0059a",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "5355de14-66cf-4d4e-b277-6e021bab00ec"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-GATEWAY-BASE"
        }
      }, {
        "name" : "hive-GATEWAY-8dfc931daad83a768a0dbd56279b1f4b",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "1aec38b1-c11a-4b66-aaab-0edc170f3b3e"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-GATEWAY-BASE"
        }
      }, {
        "name" : "hive-HIVEMETASTORE-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "aeg1l3iqn0c12o52hj18ix41d"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-HIVEMETASTORE-BASE"
        }
      }, {
        "name" : "hive-HIVESERVER2-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dj4izx30nza5t6694hw6de20s"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-HIVESERVER2-BASE"
        }
      }, {
        "name" : "hive-WEBHCAT-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "WEBHCAT",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "hive_webhcat_secret_key",
            "value" : "AlKnphXoeEbW4i7zvOusnxjg49klyP"
          }, {
            "name" : "role_jceks_password",
            "value" : "7z12sm3j959juqz0qlj0k9s3i"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hive-WEBHCAT-BASE"
        }
      } ],
      "displayName" : "Hive",
      "roleConfigGroups" : [ {
        "name" : "hive-GATEWAY-BASE",
        "displayName" : "Gateway Default Group",
        "roleType" : "GATEWAY",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hive"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-BASE",
        "displayName" : "Hive Metastore Server Default Group",
        "roleType" : "HIVEMETASTORE",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hive"
        },
        "config" : {
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "547356672"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-BASE",
        "displayName" : "HiveServer2 Default Group",
        "roleType" : "HIVESERVER2",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hive"
        },
        "config" : {
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "547356672"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "2683672985"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "451"
          } ]
        }
      }, {
        "name" : "hive-WEBHCAT-BASE",
        "displayName" : "WebHCat Server Default Group",
        "roleType" : "WEBHCAT",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hive"
        },
        "config" : {
          "items" : [ ]
        }
      } ],
      "replicationSchedules" : [ ]
    }, {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-0f46b368249e95db1df5e7aee4ca51c6",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "f72fede6-24b6-4411-a3a5-942a1d8c29d3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_health_suppression_zookeeper_server_data_directory_free_space",
            "value" : "true"
          }, {
            "name" : "role_health_suppression_zookeeper_server_data_log_directory_free_space",
            "value" : "true"
          }, {
            "name" : "role_health_suppression_zookeeper_server_log_directory_free_space",
            "value" : "true"
          }, {
            "name" : "role_jceks_password",
            "value" : "1ngrt6igc14dcpuqkonr1rt61"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "zookeeper-SERVER-BASE"
        }
      }, {
        "name" : "zookeeper-SERVER-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5c6uhs7e76xk759prvyfj5cch"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "zookeeper-SERVER-BASE"
        }
      }, {
        "name" : "zookeeper-SERVER-47ac12a07573a05c9569413a68f0059a",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "5355de14-66cf-4d4e-b277-6e021bab00ec"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8jafygx6nzjvqvpl8m1fxp1e5"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "zookeeper-SERVER-BASE"
        }
      } ],
      "displayName" : "ZooKeeper",
      "roleConfigGroups" : [ {
        "name" : "zookeeper-SERVER-BASE",
        "displayName" : "Server Default Group",
        "roleType" : "SERVER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "zookeeper"
        },
        "config" : {
          "items" : [ {
            "name" : "zookeeper_server_java_heapsize",
            "value" : "547356672"
          } ]
        }
      } ]
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "items" : [ {
          "name" : "database_host",
          "value" : "ip-10-0-60-244.us-west-2.compute.internal"
        }, {
          "name" : "database_password",
          "value" : "admin"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-3cd6aad89f71c4bab93338e2e1cfe9bc"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-0f46b368249e95db1df5e7aee4ca51c6",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "f72fede6-24b6-4411-a3a5-942a1d8c29d3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_health_suppression_hue_server_log_directory_free_space",
            "value" : "true"
          }, {
            "name" : "role_jceks_password",
            "value" : "38w60jm615t5xtjexdp9rrwsl"
          }, {
            "name" : "secret_key",
            "value" : "toPuQzW3mPsCA0qVbwA8xBZ3ehvUzY"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hue-HUE_SERVER-BASE"
        }
      } ],
      "displayName" : "Hue",
      "roleConfigGroups" : [ {
        "name" : "hue-HUE_LOAD_BALANCER-BASE",
        "displayName" : "Load Balancer Default Group",
        "roleType" : "HUE_LOAD_BALANCER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hue"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hue-HUE_SERVER-BASE",
        "displayName" : "Hue Server Default Group",
        "roleType" : "HUE_SERVER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hue"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hue-KT_RENEWER-BASE",
        "displayName" : "Kerberos Ticket Renewer Default Group",
        "roleType" : "KT_RENEWER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hue"
        },
        "config" : {
          "items" : [ ]
        }
      } ]
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bhvirueqv97fcle29idj1ccsm"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "oozie-OOZIE_SERVER-BASE"
        }
      } ],
      "displayName" : "Oozie",
      "roleConfigGroups" : [ {
        "name" : "oozie-OOZIE_SERVER-BASE",
        "displayName" : "Oozie Server Default Group",
        "roleType" : "OOZIE_SERVER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "oozie"
        },
        "config" : {
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "ip-10-0-60-244.us-west-2.compute.internal"
          }, {
            "name" : "oozie_database_password",
            "value" : "admin"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "547356672"
          } ]
        }
      } ]
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "vGZdWrwY1Yiu9EJyAEzEQXlqVZszzK"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "967n8o7qi4r66ygh1yeaciky4"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "yarn-JOBHISTORY-BASE"
        }
      }, {
        "name" : "yarn-NODEMANAGER-3f5b4aee6670e33f6f10eb3ba2d13008",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "aae2b5ea-252d-4061-be5b-99cee9b93ab1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "1jdi28amlwy9n60g5akpz5tbw"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "yarn-NODEMANAGER-1"
        }
      }, {
        "name" : "yarn-NODEMANAGER-47ac12a07573a05c9569413a68f0059a",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "5355de14-66cf-4d4e-b277-6e021bab00ec"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2x283vxrt1qz5vic6w4e66lic"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "yarn-NODEMANAGER-BASE"
        }
      }, {
        "name" : "yarn-NODEMANAGER-8dfc931daad83a768a0dbd56279b1f4b",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "1aec38b1-c11a-4b66-aaab-0edc170f3b3e"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "bd6gwkqiat2v1h9ord5ore3xu"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "yarn-NODEMANAGER-2"
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "84"
          }, {
            "name" : "role_jceks_password",
            "value" : "31sbtcfbu49rzltuk08qhlkgs"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "yarn-RESOURCEMANAGER-BASE"
        }
      } ],
      "displayName" : "YARN (MR2 Included)",
      "roleConfigGroups" : [ {
        "name" : "yarn-GATEWAY-BASE",
        "displayName" : "Gateway Default Group",
        "roleType" : "GATEWAY",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "6"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "1"
          } ]
        }
      }, {
        "name" : "yarn-JOBHISTORY-BASE",
        "displayName" : "JobHistory Server Default Group",
        "roleType" : "JOBHISTORY",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "mr2_jobhistory_java_heapsize",
            "value" : "547356672"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-1",
        "displayName" : "NodeManager Group 1",
        "roleType" : "NODEMANAGER",
        "base" : false,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "4"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "4939"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-2",
        "displayName" : "NodeManager Group 2",
        "roleType" : "NODEMANAGER",
        "base" : false,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "4"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "3011"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-BASE",
        "displayName" : "NodeManager Default Group",
        "roleType" : "NODEMANAGER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          }, {
            "name" : "yarn_nodemanager_resource_cpu_vcores",
            "value" : "4"
          }, {
            "name" : "yarn_nodemanager_resource_memory_mb",
            "value" : "3852"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-BASE",
        "displayName" : "ResourceManager Default Group",
        "roleType" : "RESOURCEMANAGER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "yarn"
        },
        "config" : {
          "items" : [ {
            "name" : "resource_manager_java_heapsize",
            "value" : "547356672"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "4939"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "4"
          } ]
        }
      } ]
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "items" : [ {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "jblp6J3PGm1MD1DFEZNgqmXNXnYnBG"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "p7D5XqFDbsCZ6rln6inxzDRPSZUCcW"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "esyv5qvZpe0rznzxMO9xOZ7zxr123H"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-BALANCER-BASE"
        }
      }, {
        "name" : "hdfs-DATANODE-3f5b4aee6670e33f6f10eb3ba2d13008",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "aae2b5ea-252d-4061-be5b-99cee9b93ab1"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "e2cr7jftea16uci6uteei18c9"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-DATANODE-BASE"
        }
      }, {
        "name" : "hdfs-DATANODE-47ac12a07573a05c9569413a68f0059a",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "5355de14-66cf-4d4e-b277-6e021bab00ec"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8f6mxr91xtaecrl76m1rnpx7u"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-DATANODE-2"
        }
      }, {
        "name" : "hdfs-DATANODE-8dfc931daad83a768a0dbd56279b1f4b",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "1aec38b1-c11a-4b66-aaab-0edc170f3b3e"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2bakci7irsyf1tt2t6nar9cxw"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-DATANODE-1"
        }
      }, {
        "name" : "hdfs-HTTPFS-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "b5pf4psr3pq68qbf30dyentis"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-HTTPFS-BASE"
        }
      }, {
        "name" : "hdfs-NAMENODE-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "namenode_id",
            "value" : "88"
          }, {
            "name" : "role_jceks_password",
            "value" : "4c4zmdgoepic5jyfziofne0t1"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-NAMENODE-BASE"
        }
      }, {
        "name" : "hdfs-NFSGATEWAY-3cd6aad89f71c4bab93338e2e1cfe9bc",
        "type" : "NFSGATEWAY",
        "hostRef" : {
          "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "czhqd76xiq4f95xs2z094al2r"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-NFSGATEWAY-BASE"
        }
      }, {
        "name" : "hdfs-SECONDARYNAMENODE-8dfc931daad83a768a0dbd56279b1f4b",
        "type" : "SECONDARYNAMENODE",
        "hostRef" : {
          "hostId" : "1aec38b1-c11a-4b66-aaab-0edc170f3b3e"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5knr5n7gajlkqk6zkmzod76ao"
          } ]
        },
        "roleConfigGroupRef" : {
          "roleConfigGroupName" : "hdfs-SECONDARYNAMENODE-BASE"
        }
      } ],
      "displayName" : "HDFS",
      "roleConfigGroups" : [ {
        "name" : "hdfs-BALANCER-BASE",
        "displayName" : "Balancer Default Group",
        "roleType" : "BALANCER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "balancer_java_heapsize",
            "value" : "547356672"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-1",
        "displayName" : "DataNode Group 1",
        "roleType" : "DATANODE",
        "base" : false,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "4293706956"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "3157262336"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-2",
        "displayName" : "DataNode Group 2",
        "roleType" : "DATANODE",
        "base" : false,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "4293706956"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4039114752"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-BASE",
        "displayName" : "DataNode Default Group",
        "roleType" : "DATANODE",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "4293706956"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-BASE",
        "displayName" : "Failover Controller Default Group",
        "roleType" : "FAILOVERCONTROLLER",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-GATEWAY-BASE",
        "displayName" : "Gateway Default Group",
        "roleType" : "GATEWAY",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }
      }, {
        "name" : "hdfs-HTTPFS-BASE",
        "displayName" : "HttpFS Default Group",
        "roleType" : "HTTPFS",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-BASE",
        "displayName" : "JournalNode Default Group",
        "roleType" : "JOURNALNODE",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-NAMENODE-BASE",
        "displayName" : "NameNode Default Group",
        "roleType" : "NAMENODE",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          } ]
        }
      }, {
        "name" : "hdfs-NFSGATEWAY-BASE",
        "displayName" : "NFS Gateway Default Group",
        "roleType" : "NFSGATEWAY",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-SECONDARYNAMENODE-BASE",
        "displayName" : "SecondaryNameNode Default Group",
        "roleType" : "SECONDARYNAMENODE",
        "base" : true,
        "serviceRef" : {
          "clusterName" : "cluster",
          "serviceName" : "hdfs"
        },
        "config" : {
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/dfs/snn"
          } ]
        }
      } ],
      "replicationSchedules" : [ ],
      "snapshotPolicies" : [ ]
    } ],
    "parcels" : [ {
      "product" : "CDH",
      "version" : "5.8.3-1.cdh5.8.3.p0.2",
      "stage" : "DISTRIBUTED",
      "clusterRef" : {
        "clusterName" : "cluster"
      }
    }, {
      "product" : "CDH",
      "version" : "5.8.3-1.cdh5.8.3.p0.2",
      "stage" : "ACTIVATED",
      "clusterRef" : {
        "clusterName" : "cluster"
      }
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "68db1604-4302-4f5c-a217-837362be655c",
    "ipAddress" : "10.0.60.244",
    "hostname" : "ip-10-0-60-244.us-west-2.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ {
        "name" : "memory_overcommit_threshold",
        "value" : "0.9"
      } ]
    }
  }, {
    "hostId" : "f72fede6-24b6-4411-a3a5-942a1d8c29d3",
    "ipAddress" : "10.0.60.245",
    "hostname" : "ip-10-0-60-245.us-west-2.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "1aec38b1-c11a-4b66-aaab-0edc170f3b3e",
    "ipAddress" : "10.0.60.246",
    "hostname" : "ip-10-0-60-246.us-west-2.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ {
        "name" : "memory_overcommit_threshold",
        "value" : "0.9"
      } ]
    }
  }, {
    "hostId" : "5355de14-66cf-4d4e-b277-6e021bab00ec",
    "ipAddress" : "10.0.60.247",
    "hostname" : "ip-10-0-60-247.us-west-2.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "aae2b5ea-252d-4061-be5b-99cee9b93ab1",
    "ipAddress" : "10.0.60.248",
    "hostname" : "ip-10-0-60-248.us-west-2.compute.internal",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__mgmt-ACTIVITYMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "b7d0751bb22da845ce47658409ed76054eb8ba4989a619f30386b0e5a3857322",
    "pwSalt" : 6449527119708843527,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-3cd6aad89f71c4bab93338e2e1cfe9bc",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "ace4c6136ddd37aa03e64841ee16e644caabd4b88e89fa17704c5838f2a49b0d",
    "pwSalt" : -5114457672777632080,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "d573b94c39ff3f15bd4c1053cde4a34078ce27cdec92a8016cd4970049fd495a",
    "pwSalt" : 6912344859661043046,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-3cd6aad89f71c4bab93338e2e1cfe9bc",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "ac44d2078525fcbf7fb8e76743b8a6de43fe6e5970173fe7ea4543f6b6c33bcb",
    "pwSalt" : 4119028541863689141,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "b70ab1d7a0563fb6716cd338baa01f86fe44888b694a52748b7c2ae64622690d",
    "pwSalt" : 6158411915513536272,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "e553a5e668113f0849aecf7010856b6c75cca35cf3ce5cfc1d830607c9240b71",
    "pwSalt" : -1342192164511911744,
    "pwLogin" : true
  }, {
    "name" : "philka",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "0219d5d7bc22d2e42c06762adf5c94b2c8f766f3c8b8f9bc70dea643507e4560",
    "pwSalt" : 6285282772357747953,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.8.2",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20160916-1419",
    "gitHash" : "d23c620f3a3bbd85d8511d6ebba49beaaab14b75",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ACTIVITYMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "ACTIVITYMONITOR",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "bww0xkxoshi1wnpsmnwp1u77d"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-ACTIVITYMONITOR-BASE"
      }
    }, {
      "name" : "mgmt-ALERTPUBLISHER-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "26qdnjr6g214zl96ejv35ucp3"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-ALERTPUBLISHER-BASE"
      }
    }, {
      "name" : "mgmt-EVENTSERVER-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "4qym61ozv993vy7ivrkf74bkh"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-EVENTSERVER-BASE"
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "5dohuxxsz5a8p76x25b4p97l6"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-HOSTMONITOR-BASE"
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "81f79ziomzqqhz5at5q0nheof"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-REPORTSMANAGER-BASE"
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-3cd6aad89f71c4bab93338e2e1cfe9bc",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "68db1604-4302-4f5c-a217-837362be655c"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "cuqourzq6659s9za3d33hty4i"
        } ]
      },
      "roleConfigGroupRef" : {
        "roleConfigGroupName" : "mgmt-SERVICEMONITOR-BASE"
      }
    } ],
    "displayName" : "Cloudera Management Service",
    "roleConfigGroups" : [ {
      "name" : "mgmt-ACTIVITYMONITOR-BASE",
      "displayName" : "Activity Monitor Default Group",
      "roleType" : "ACTIVITYMONITOR",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ {
          "name" : "firehose_database_host",
          "value" : "ip-10-0-60-244.us-west-2.compute.internal"
        }, {
          "name" : "firehose_database_name",
          "value" : "amon"
        }, {
          "name" : "firehose_database_password",
          "value" : "admin"
        }, {
          "name" : "firehose_database_user",
          "value" : "amon"
        }, {
          "name" : "firehose_heapsize",
          "value" : "547356672"
        } ]
      }
    }, {
      "name" : "mgmt-ALERTPUBLISHER-BASE",
      "displayName" : "Alert Publisher Default Group",
      "roleType" : "ALERTPUBLISHER",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-BASE",
      "displayName" : "Event Server Default Group",
      "roleType" : "EVENTSERVER",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ {
          "name" : "event_server_heapsize",
          "value" : "547356672"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-BASE",
      "displayName" : "Host Monitor Default Group",
      "roleType" : "HOSTMONITOR",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ ]
      }
    }, {
      "name" : "mgmt-NAVIGATOR-BASE",
      "displayName" : "Navigator Audit Server Default Group",
      "roleType" : "NAVIGATOR",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ ]
      }
    }, {
      "name" : "mgmt-NAVIGATORMETASERVER-BASE",
      "displayName" : "Navigator Metadata Server Default Group",
      "roleType" : "NAVIGATORMETASERVER",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-BASE",
      "displayName" : "Reports Manager Default Group",
      "roleType" : "REPORTSMANAGER",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "ip-10-0-60-244.us-west-2.compute.internal"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "admin"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        }, {
          "name" : "headlamp_heapsize",
          "value" : "547356672"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-BASE",
      "displayName" : "Service Monitor Default Group",
      "roleType" : "SERVICEMONITOR",
      "base" : true,
      "serviceRef" : {
        "serviceName" : "mgmt"
      },
      "config" : {
        "items" : [ ]
      }
    } ]
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/26/2012 2:10"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/{latest_supported}/,https://archive.cloudera.com/cdh4/parcels/latest/,https://archive.cloudera.com/impala/parcels/latest/,https://archive.cloudera.com/search/parcels/latest/,https://archive.cloudera.com/accumulo/parcels/1.4/,https://archive.cloudera.com/accumulo-c5/parcels/latest/,https://archive.cloudera.com/kafka/parcels/latest/,https://archive.cloudera.com/navigator-keytrustee5/parcels/latest/,https://archive.cloudera.com/spark/parcels/latest/,https://archive.cloudera.com/sqoop-connectors/parcels/latest/"
    } ]
  },
  "allHostsConfig" : {
    "items" : [ ]
  },
  "peers" : [ ],
  "hostTemplates" : {
    "items" : [ ]
  }
}
0
```