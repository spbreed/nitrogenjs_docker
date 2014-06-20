nitrogenjs_docker
=================

##Dockerfiles for NitrogenJS

[NitrogenJS](https://github.com/nitrogenjs) is a platform for building connected devices and applications and is composed of various client and server components.  This project provides [Dockerfiles](https://docs.docker.com/reference/builder) to ease development and deployment of NitrogenJS server components using [Docker](http://www.docker.com)

###NitrogenJS_Service
This allows you to build an image to run the NitrogenJS Service.  At image build time the latest code is synced from the [NitrogenJS repository](https://github.com/nitrogenjs/service).  

The image uses the default service configuration with local storage, MongoDB and a Redis cache.  MongoDB is pulled from the official Ubuntu packages, and Redis is built from the latest sources per Redis recommendations.

To build the NitrogenJS_Service image

    git clone https://github.com/stefangordon/nitrogenjs_docker.git
    cd nitrogenjs_docker/nitrogenjs_service
    docker build -t yourname/nitrogenjs_service .

To run the service, start a container like this:

    docker run -t -i yourname/nitrogenjs_service

This will allocate a tty and provide output in your terminal.  If you would prefer to let it run in the background, omit -t -i

    docker run yourname/nitrogenjs_service

If you would like to access bash in the container for debugging or modification try this:

    docker run -t -i yourname/nitrogenjs_service /bin/bash

And once at a terminal you can start NitrogenJS Service yourself like this:

    cd /home/nitrogen
    ./run
