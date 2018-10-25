# KIWI - uWSGI Description for docker and OCI image

## Initial setup

1. Include _Virtualization/containers_ to your repositorys

    zypper addrepo http://download.opensuse.org/repositories/Virtualization:/containers/<DIST> container-tools

2. Install **umoci**, **skopeo** and **kiwi** tools

    zypper in python3-kiwi umoci skopeo

3. Clone this repository and optional submodules

    git clone --recurse-submodules git@github.com:appleonkel/kiwi-descriptions.git

## OCI Image

Build the image:

    sudo kiwi-ng-3 system build \
					--type oci \
					--description kiwi-descriptions/opensuse-tumbleweed-uwsgi-flask \
					--target-dir /tmp/myociimage
Load the image with podman.

    podman load -i /tmp/myociimage/openSUSE-Tumbleweed-uwsgi-container-image.x86_64-1.0.oci.tar.xz

Run it on host port 8080

    podman run -p 8080:9000 localhost/uwsgi-flask:latest

## Docker Image

Build the image:

    sudo kiwi-ng-3 system build \
					--type docker \
					--description kiwi-descriptions/opensuse-tumbleweed-uwsgi-flask \
					--target-dir /tmp/mydockerimage
Load the image with docker.

    docker load -i /tmp/myociimage/openSUSE-Tumbleweed-uwsgi-container-image.x86_64-1.0.oci.tar.xz

Run it on host port 8080

    docker run -p 8080:9000 localhost/uwsgi-flask:latest

Have a lot of fun!
