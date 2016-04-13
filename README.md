Litecoind for Docker
===================

**FORKED FROM:** https://github.com/kylemanna/docker-bitcoind

**ALSO BASED ON (but without dependencies):** https://hub.docker.com/r/zouchao2010/litecoind

Docker image that runs a litecoind node in a container for easy deployment.


Requirements
------------

* Physical machine, cloud instance, or VPS that supports Docker (i.e. [Vultr](http://bit.ly/1HngXg0), [Digital Ocean](http://bit.ly/18AykdD), KVM or XEN based VMs) running Ubuntu 14.04 or later (*not OpenVZ containers!*)
* At least 6 GB to store the block chain files
* At least 1 GB RAM + 2 GB swap file

Really Fast Quick Start
-----------------------

One liner for Ubuntu 14.04 LTS machines with JSON-RPC enabled on localhost and adds upstart init script:

    curl https://raw.githubusercontent.com/kelostrada/docker-litecoind/master/bootstrap-host.sh | sh -s trusty


Quick Start
-----------

1. Create a `litecoind-data` volume to persist the litecoind blockchain data, should exit immediately.  The `litecoind-data` container will store the blockchain when the node container is recreated (software upgrade, reboot, etc):

        docker volume create --name=litecoind-data
        docker run -v litecoind-data:/litecoin --name=litecoind-node -d \
            -p 9333:9333 \
            -p 9332:9332 \
            kelu/litecoin

2. Verify that the container is running and litecoind node is downloading the blockchain

        $ docker ps
        CONTAINER ID        IMAGE                         COMMAND             CREATED             STATUS              PORTS                                              NAMES
        d0e1076b2dca        kelu/litecoind:latest     "ltc_oneshot"       2 seconds ago       Up 1 seconds        127.0.0.1:8332->8332/tcp, 0.0.0.0:8333->8333/tcp   litecoind-node

3. You can then access the daemon's output thanks to the [docker logs command]( https://docs.docker.com/reference/commandline/cli/#logs)

        docker logs -f litecoind-node

4. Install optional init scripts for upstart and systemd are in the `init` directory.


Documentation
-------------

* Additional documentation in the [docs folder](docs).
