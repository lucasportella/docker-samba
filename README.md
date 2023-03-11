[aguslr/docker-samba][1]
========================

[![publish-docker-image](https://github.com/aguslr/docker-samba/actions/workflows/docker-publish.yml/badge.svg)](https://github.com/aguslr/docker-samba/actions/workflows/docker-publish.yml) [![docker-pulls](https://img.shields.io/docker/pulls/aguslr/samba)](https://hub.docker.com/r/aguslr/samba) [![image-size](https://img.shields.io/docker/image-size/aguslr/samba/latest)](https://hub.docker.com/r/aguslr/samba)


This *Docker* image sets up *Samba* inside a docker container.

> **[Samba][2]** is a free software re-implementation of the SMB networking
> protocol.


Installation
------------

To use *docker-samba*, follow these steps:

1. Clone and start the container:

       docker run -p 445:445 \
         -e SAMBA_USER=bob \
         -e SAMBA_PASS=123456 \
         -v "${PWD}"/data:/data \
         -v "${PWD}"/home:/home \
         docker.io/aguslr/samba:latest

2. Configure your *Samba* client software to connect to your *Samba* server's IP
   address with user `SAMBA_USER`.


### Variables

The image is configured using environment variables passed at runtime. All these
variables are prefixed by `SAMBA_`.

| Variable | Function                          | Required |
| :------- | :-------------------------------- | -------- |
| `USER`   | Name of user to access the shares | Y        |
| `PASS`   | Password of user                  | Y        |


#### Custom `smb.conf`

To configure additional shares or parameters, we can add these to a `smb.conf`
file and mount it with this command:

    docker run -p 445:445 \
      -e SAMBA_USER=bob \
      -e SAMBA_PASS=123456 \
      -v "${PWD}"/data:/data \
      -v "${PWD}"/home:/home \
      -v "${PWD}"/smb.conf:/etc/samba/includes.conf \
      docker.io/aguslr/samba:latest


Build locally
-------------

Instead of pulling the image from a remote repository, you can build it locally:

1. Clone the repository:

       git clone https://github.com/aguslr/docker-samba.git

2. Change into the newly created directory and use `docker-compose` to build and
   launch the container:

       cd docker-samba && docker-compose up --build -d


[1]: https://github.com/aguslr/docker-samba
[2]: https://www.samba.org/
