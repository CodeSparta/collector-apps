# Koffer Collector | RedHat OpenShift Auxiliary Apps
## Provides
This repo runs an artifact collector with the Koffer Engine and produces a tarball
of artifacts for airgap infrastructure deployment.

## Instructions:
### 1. Run Koffer Engine
```
 sudo podman run -it --rm \
     --entrypoint=/usr/bin/entrypoint \
     --volume /tmp/platform:/root/deploy:z \
     --volume /tmp/platform/secrets/docker/quay.json:/root/.docker/config.json:ro \
  docker.io/containercraft/koffer:latest \
  https://repo1.dsop.io/dsop/redhat/platformone/ocp4x/ansible/collector-apps.git master
```
### 2. Move Koffer Bundle to restricted environment target host `/tmp` directory
### 3. Extract to docker registry path
```
 tar xv -f /tmp/koffer-bundle.collector-apps.tar -C /root/deploy/mirror
```
### 4. Start or Restart your docker registry container
# [Developer Docs & Utils](./dev)
