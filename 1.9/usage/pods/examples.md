---
post_title: Examples
feature_maturity: preview
menu_order: 30
---

# A pod with multiple containers
	
The following pod definition specifies a pod with 3 containers. <!-- Validated by Joel 1/3/17 -->

```json
{
  "id": "/pod-with-multiple-containers",
  "labels": {},
  "version": "2017-01-03T18:21:19.31Z",
  "environment": {},
  "containers": [
    {
      "name": "sleep1",
      "exec": {
        "command": {
          "shell": "sleep 1000"
        }
      },
      "resources": {
        "cpus": 0.01,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [],
      "artifacts": [],
      "labels": {}
    },
    {
      "name": "sleep2",
      "exec": {
        "command": {
          "shell": "sleep 1000"
        }
      },
      "resources": {
        "cpus": 0.01,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [],
      "artifacts": [],
      "labels": {}
    },
    {
      "name": "sleep3",
      "exec": {
        "command": {
          "shell": "sleep 1000"
        }
      },
      "resources": {
        "cpus": 0.01,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [],
      "artifacts": [],
      "labels": {}
    }
  ],
  "secrets": {},
  "volumes": [],
  "networks": [
    {
      "mode": "host",
      "labels": {}
    }
  ],
  "scaling": {
    "kind": "fixed",
    "instances": 10,
    "maxInstances": null
  },
  "scheduling": {
    "backoff": {
      "backoff": 1,
      "backoffFactor": 1.15,
      "maxLaunchDelay": 3600
    },
    "upgrade": {
      "minimumHealthCapacity": 1,
      "maximumOverCapacity": 1
    },
    "placement": {
      "constraints": [],
      "acceptedResourceRoles": []
    },
    "killSelection": "Youngest_First",
    "unreachableStrategy": {
      "inactiveAfterSeconds": 900,
      "expungeAfterSeconds": 604800
    }
  },
  "executorResources": {
    "cpus": 0.1,
    "mem": 32,
    "disk": 10
  }
}
```

# A Pod that Uses Ephemeral Volumes

The following pod definition specifies an ephemeral volume called `v1`. <!-- Validated by Joel 1/3/17 -->

```json
{
  "id": "/with-ephemeral-vol",
  "labels": {},
  "version": "2017-01-03T17:36:39.389Z",
  "environment": {},
  "containers": [
    {
      "name": "ct1",
      "exec": {
        "command": {
          "shell": "while true; do echo the current time is $(date) > ./jdef-v1/clock; sleep 1; done"
        }
      },
      "resources": {
        "cpus": 0.1,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [
        {
          "name": "v1",
          "mountPath": "jdef-v1"
        }
      ],
      "artifacts": [],
      "labels": {}
    },
    {
      "name": "ct2",
      "exec": {
        "command": {
          "shell": "while true; do cat ./etc/clock; sleep 1; done"
        }
      },
      "resources": {
        "cpus": 0.1,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [
        {
          "name": "v1",
          "mountPath": "etc"
        }
      ],
      "artifacts": [],
      "labels": {}
    }
  ],
  "secrets": {},
  "volumes": [
    {
      "name": "v1"
    }
  ],
  "networks": [
    {
      "mode": "host",
      "labels": {}
    }
  ],
  "scaling": {
    "kind": "fixed",
    "instances": 1,
    "maxInstances": null
  },
  "scheduling": {
    "backoff": {
      "backoff": 1,
      "backoffFactor": 1.15,
      "maxLaunchDelay": 3600
    },
    "upgrade": {
      "minimumHealthCapacity": 1,
      "maximumOverCapacity": 1
    },
    "placement": {
      "constraints": [],
      "acceptedResourceRoles": []
    },
    "killSelection": "Youngest_First",
    "unreachableStrategy": {
      "inactiveAfterSeconds": 900,
      "expungeAfterSeconds": 604800
    }
  },
  "executorResources": {
    "cpus": 0.1,
    "mem": 32,
    "disk": 10
  }
}
```

## IP-per-Pod Networking

The following pod definition specifies a virtual (user) network named `dcos`. <!-- Validated by Joel 1/3/17 -->

```json
{
  "id": "/pod-with-virtual-network",
  "labels": {},
  "version": "2017-01-03T18:17:11.237Z",
  "environment": {},
  "containers": [
    {
      "name": "sleep1",
      "exec": {
        "command": {
          "shell": "sleep 1000"
        }
      },
      "resources": {
        "cpus": 0.1,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [],
      "environment": {},
      "volumeMounts": [],
      "artifacts": [],
      "labels": {}
    }
  ],
  "secrets": {},
  "volumes": [],
  "networks": [
    {
      "name": "dcos",
      "mode": "container",
      "labels": {}
    }
  ],
  "scaling": {
    "kind": "fixed",
    "instances": 1,
    "maxInstances": null
  },
  "scheduling": {
    "backoff": {
      "backoff": 1,
      "backoffFactor": 1.15,
      "maxLaunchDelay": 3600
    },
    "upgrade": {
      "minimumHealthCapacity": 1,
      "maximumOverCapacity": 1
    },
    "placement": {
      "constraints": [],
      "acceptedResourceRoles": []
    },
    "killSelection": "Youngest_First",
    "unreachableStrategy": {
      "inactiveAfterSeconds": 900,
      "expungeAfterSeconds": 604800
    }
  },
  "executorResources": {
    "cpus": 0.1,
    "mem": 32,
    "disk": 10
  }
}
```

This pod declares a “web” endpoint that listens on port 80. <!-- Validated by Joel 1/3/17 -->

```json
{
  "id": "/pod-with-endpoint",
  "labels": {},
  "version": "2017-01-03T18:18:45.632Z",
  "environment": {},
  "containers": [
    {
      "name": "sleep1",
      "exec": {
        "command": {
          "shell": "sleep 1000"
        }
      },
      "resources": {
        "cpus": 0.1,
        "mem": 32,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [
        {
          "name": "web",
          "containerPort": 80,
          "protocol": [
            "http"
          ],
          "labels": {}
        }
      ],
      "environment": {},
      "volumeMounts": [],
      "artifacts": [],
      "labels": {}
    }
  ],
  "secrets": {},
  "volumes": [],
  "networks": [
    {
      "name": "dcos",
      "mode": "container",
      "labels": {}
    }
  ],
  "scaling": {
    "kind": "fixed",
    "instances": 1,
    "maxInstances": null
  },
  "scheduling": {
    "backoff": {
      "backoff": 1,
      "backoffFactor": 1.15,
      "maxLaunchDelay": 3600
    },
    "upgrade": {
      "minimumHealthCapacity": 1,
      "maximumOverCapacity": 1
    },
    "placement": {
      "constraints": [],
      "acceptedResourceRoles": []
    },
    "killSelection": "Youngest_First",
    "unreachableStrategy": {
      "inactiveAfterSeconds": 900,
      "expungeAfterSeconds": 604800
    }
  },
  "executorResources": {
    "cpus": 0.1,
    "mem": 32,
    "disk": 10
  }
}
```

# Complete Pod 
The following pod definition can serve as a reference to create more complicated pods. 

```json
{
  "id": "/complete-pod",
  "labels": {
    "owner": "zeus",
    "note": "Away from olympus"
  },
  "environment": {
    "XPS1": "Test"
  },
  "volumes": [
    {
      "name": "etc",
      "host": "/etc"
    }
  ],
  "networks": [
    {
     "mode": "container", 
     "name": "dcos"
    }
  ],
  "scaling": {
    "kind": "fixed",
    "instances": 1
  },
  "scheduling": {
    "backoff": {
      "backoff": 1,
      "backoffFactor": 1.15,
      "maxLaunchDelay": 3600
    },
    "upgrade": {
      "minimumHealthCapacity": 1,
      "maximumOverCapacity": 1
    },
    "placement": {
      "constraints": [],
      "acceptedResourceRoles": []
    }
  },
  "containers": [
    {
      "name": "container1",
      "resources": {
        "cpus": 1,
        "mem": 128,
        "disk": 0,
        "gpus": 0
      },
      "endpoints": [
        {
          "name": "http-endpoint",
          "containerPort": 80,
          "hostPort": 0,
          "protocol": [ "HTTP" ],
          "labels": {}
        }
      ],
      "image": {
        "id": "nginx:latest",
        "kind": "DOCKER",
        "forcePull": false
      },
      "environment": {
        "XPS1": "Test"
      },
      "user": "root",
      "healthCheck": {
        "gracePeriodSeconds": 30,
        "intervalSeconds": 5,
        "maxConsecutiveFailures": 3,
        "timeoutSeconds": 4,
        "delaySeconds": 2,
        "http": {
          "path": "/",
          "scheme": "HTTP",
          "endpoint": "http-endpoint"
        }
      },
      "volumeMounts": [
        {
          "name": "etc",
          "mountPath": "/mnt/etc",
          "readOnly": true
        }
      ],
      "artifacts": [
        {
          "uri": "https://ftp.gnu.org/gnu/glibc/glibc-2.25.tar.gz",
          "executable": false,
          "extract": true,
          "cache": true,
          "destPath": "glibc-2.25.tar.gz"
        }
      ],
      "labels": {
        "owner": "zeus",
        "note": "Away from olympus"
      },
      "lifecycle": {
        "killGracePeriodSeconds": 60
      }
    }
  ]
}
```
