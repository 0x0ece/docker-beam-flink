# Apache Beam (over Flink) on Docker

## Installation

0. Prerequisites: `docker` and `docker-compose`

1. Clone this repo

2. Run `sh ./build.sh`

## Deploy

1. Deploy cluster and see config/setup log output (best run in a screen session)

  `docker-compose up`

  Or, deploy as a daemon (and return)

  `docker-compose up -d`

2. Scale the cluster up or down to *N* TaskManagers

  `docker-compose scale taskmanager=<N>`

## Run a Demo

1. Open the web UI on (exposed on port 48080)

  `open http://localhost:48080`

   or on Mac OS X with `docker-machine`

  `open http://$(docker-machine ip default):48080`

2. Click "Submit new Job" in the right menu

3. Flag the checkbox near `beam-starter-<ver>.jar`

4. Click on "Show Plan" (or "Submit") -- no param is needed, but you can play with that too

![Home Page](https://raw.githubusercontent.com/ecesena/docker-beam-flink/master/screenshots/showplan.png)

## Other Operations

- Access the JobManager node with SSH (exposed on port 220)

`ssh root@$(docker-machine ip default) -p 220`

The password is 'secret'

- Kill the cluster

`docker-compose kill`

- Upload a jar to the cluster

`scp -P 220 <your_jar> root@$(docker-machine ip default):/<your_path>`

- Run a topology

`ssh -p 220 root@$(docker-machine ip default) /usr/local/flink/bin/flink run -c <your_class> <your_jar> <your_params>`

or

ssh to the job manager and run the topology from there.

## Ports

- The Web Dashboard is on port `48080`
- The Web Client is on port `48081`
- JobManager RPC port `6123` (default, not exposed to host)
- TaskManagers RPC port `6121` (default, not exposed to host)
- TaskManagers Data port `6122` (default, not exposed to host)
- JobManager SSH `220`
- TaskManagers SSH: randomly assigned port, check wih `docker ps`

Edit the `docker-compose.yml` file to edit port settings.

## TODO

- Add the JAR to the front end during image building
- Remove `beam-starter-<ver>.jar` from this repo and download it from release

## Open source

Forked from https://github.com/apache/flink/tree/master/flink-contrib/docker-flink
