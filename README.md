# rasmus/debug

This repository contains the Dockerfile for a versatile debug container04. This container is equipped with a variety of networking and system utilities, making it an ideal tool for debugging and troubleshooting network issues, testing connectivity, and performing various administrative tasks in e.g. a Kubernetes cluster.

- https://hub.docker.com/r/rasmus/debug

### Run in Kubernetes

Example on how the container might be used in Kubernetes.

```
kubectl run -it --rm debug \
    --image rasmus/debug \
    --override-type='strategic' \
    --overrides='{"spec":{"containers":[{"name":"debug","resources":{"limits":{"memory":"2Gi","cpu":"200m"}}}]}}' \
    -- /bin/bash
```

### Run via Docker

Example on how the container might be used from a Docker command line.

```
docker run -it --rm rasmus/debug
```
