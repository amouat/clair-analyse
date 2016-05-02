Analyse-local-images in Docker
==============================

Simple Dockerfile that builds an image with
[analyse-local-images](https://github.com/coreos/clair/tree/master/contrib/analyze-local-images)
installed, to be used in association with the [Clair vulnerability
scanner](https://github.com/coreos/clair).

Usage is:

    $ docker run -it \
        --net clair-container-network \
        -v /var/run/docker.sock:/var/run/docker.sock \
        --name analyser \
        amouat/clair-analyse -endpoint http://clair:6060 -my-address analyser image-to-scan

This assumes Clair is running in container available as "clair" on
"clair-container-network". It's necessary to give the container a name (such as
"analyser") in order for Clair to be able to resolve the address when
transferring the image to analyse.

Docker is installed in the image and the socket mounted for access to images. It
would be cleaner to only install the Docker client and to avoid the
http://get.docker.com script, but this was easier.

