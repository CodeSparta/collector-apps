# Koffer Collector | OpenShift Auxiliary Apps
This repo runs an artifact collector with the Koffer Engine and produces a tarball
of artifacts for airgap infrastructure deployment.

## Instructions:
### 1. Run Koffer Engine  
```
 sudo podman run -it --rm \
     --volume /tmp/bundle:/root/deploy/bundle:z \
  docker.io/codesparta/koffer bundle \
  --service github.com --user codesparta --repo collector-apps --branch master
```
### 2. Extract to docker registry path
```
 tar xv -f /tmp/koffer-bundle.collector-apps.tar -C /root
```
### 3. Extract to docker registry path
```
 tar xv -f /tmp/koffer-bundle.collector-apps.tar -C /root
```

## Develop:
### 1. Clone Repo
```
 git clone https://github.com/codesparta/collector-apps.git && cd collector-apps
```
### 2. Exec into Koffer Engine
```
 sudo podman run -it --rm \
     --volume /tmp/bundle:/root/deploy/bundle:z \
     --volume $(pwd):/root/koffer:z \
  docker.io/codesparta/koffer bundle \
  --service github.com --user codesparta --repo collector-apps --branch master
```
### 3. Start Koffer Internal Registry Service
```
 run_registry.sh
```
### 4. Run Playbook
```
 ./site.yml
```
