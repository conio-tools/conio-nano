# Conio nano

This repository is a fork of the [big-data-europe/docker-hadoop](https://github.com/big-data-europe/docker-hadoop) but configured to run and test [Conio shim](https://github.com/conio-tools/conio-shim) easily.

About quick start, configurations and other details visit docker-hadoop's [README.md](https://github.com/big-data-europe/docker-hadoop/blob/master/README.md).

## Changes between

Conio nano:
- Exposed ResourceManager, NodeManager and JobHistory Server UI
- Uses the Linux Container Executor (with configurable `container-executor.cfg`) for the NodeManager
- Mounts the Docker socket to the NodeManager's container thus creating a [dind-variant](https://hub.docker.com/_/docker) container
- Is configured to schedule Docker containers
- Is added a Conio make target for this project which builds a container where the Conio shim client can run

## Get started

1. Copy the yaml file and the fat conio shim jar (with dependencies) to the `/conio` folder.

1. Type the following command: `make conio`

1. Start the dockerized Hadoop service according to the `docker-hadoop` [docs](https://github.com/big-data-europe/docker-hadoop/blob/master/README.md).

1. Start the Conio shim client in a Docker container with some options like:
```
docker run -it --env-file hadoop.env --network docker-hadoop_default -v $(PWD)/conio:/conio conio/base:master -- sudo -u conio java -jar /conio/conio-1.0-SNAPSHOT-jar-with-dependencies.jar -yaml /conio/pod.yaml -queue default
```
