docker-clusterenv
=================

or: *development of cluster applications meets docker*

or : *One change in the source code to rule them all*

Objectives
----------

Do you develop applications...

* that run on a cluster (or in parallel on more than one machine)?
* that interact with other components (client/server, peer-to-peer)?
* targeted on different runtime environments? (OS flavor, language version, ...)?


**docker-clusterenv** allows you to start a small cluster of severall docker containers
customized to your development needs.

* ssh access enabled
* dns lookup working
* just one command to specify where ...
    * to mount local (source) directories, and
    * to create symbolic links (for applications using absolute path names)

⇒  One change in the source code is available instantaniously on your whole development cluster.


Prerequisites
-------------

* [docker](https://www.docker.io/): *an open source project to pack, ship and run any application as a lightweight container*
    * (strongly recommended) use docker as [non-root user](http://docs.docker.io/en/latest/use/basics/#why-sudo)
* [bash](http://www.gnu.org/software/bash/)
* [python](http://www.python.org/)
* [docopt](http://docopt.org/)

tl;dr
-----

```bash
# just the first time: download base image, update to newest versions, create docker image
./build-containers

# start some machines
./start-machine foo1
./start-machine foo2
./start-machine foo3 --interactive

# tadahh! thats it, 3 machines up-n-running
#
# but what can you do with them?
# so from here, interactivly on 'foo3':

# your current working directory, writeable
ls -al /local-fs

# dns for your other cluster machines
cat /etc/dnsmasq.d/*

# ssh on other machine
ssh foo1 hostname

# ...

stop-machines
```

Commands
--------

configure-docker
################

- restarts the docker service

- configures both unix and tcp socket (for dockerui)

- starts dockerui container (see http://localhost:9000/)

- customizing:

    - honors the DOCKER_ROOT_DIR env variable, if present: sets the docker root dir (default: /var/lib/docker)

    - example:

    ```bash
    DOCKER_ROOT_DIR=/mnt/big_disk/docker/ ./configure-docker
    ```

TODO
----

* ~~get rid of update-env, every machine registers itself with dnsmasq~~
* ~~get rid of generated stop-clusterenv script, provide function that parses dnsmasq info~~
* ~~check for hostname clashes~~
* document --link-files
* document _python_path_

