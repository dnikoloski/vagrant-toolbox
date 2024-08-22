# Vangrat libvirt containerized

## Build the container

```sh
podman build -t localhost/vagrant-container-fedora:latest -f Dockerfile.(fedora || ubuntu) .
```

## Create a ~/.local/bin/vagrant-(fedora || ubuntu)

```sh
#! /bin/env bash

podman run -it --rm \
  --env LIBVIRT_DEFAULT_URI \
  --volume /var/run/libvirt/:/var/run/libvirt/ \
  --volume ~/.vagrant.d:/.vagrant.d \
  --volume $(realpath "${PWD}"):${PWD} \
  --workdir "${PWD}" \
  --privileged \
  --net host \
  --security-opt label=disable \
  localhost/vagrant-container-fedora:latest
```