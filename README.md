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
### 2. Push bundle directory
```
 sudo chown -R $USER /tmp/bundle
 rsync --progress -avzh /tmp/bundle -e "ssh -i ~/.ssh/${keyname}" ec2-user@${rhel_bastion_public_ip}:~
```
### 3. Extract to CloudCtl Artifact Directory
```
 sudo tar xv -f ~/bundle/koffer-bundle.collector-apps.tar -C /root
```

## Develop:
### 1. Clone Repo
```
 git clone https://github.com/codesparta/collector-apps.git && cd collector-apps
```
### 2. Exec into Koffer Engine
```
 sudo podman run -it --rm \
     --entrypoint bash \
     --volume /tmp/bundle:/root/deploy/bundle:z \
     --volume $(pwd):/root/koffer:z \
  docker.io/codesparta/koffer
```
### 3. Start Koffer Internal Registry Service
```
 run_registry.sh
```
### 4. Run Playbook
```
 ./site.yml
```
