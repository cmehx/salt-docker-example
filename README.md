# Project Goal

Student project to learn how to deploy a salt manager and its minions using
docker containers with podman and podman-compose

# Requirements

- Docker
- Podman
- Podman-compose

# Configuration

By default the master is in auto_accept:true to avoid key checking to all n
minion to join without any manual validation
Line 16 of master/Containerfile

By default minions add the salt-master to match master container hostname
to connect by domaine name to its master
Line 16 minion/Containerfile

# Deploying Salt Master and Minion on containers

#### Launch a Master and a Minion containers using podman-compose
- podman-compose up
#### Example with -f to specify a file entry / -d for background execution mode
- podman-compose -f compose.yaml up -d

#### To enter a container in bash mode
- docker-compose exec <container_name> bash
#### To enter salt-master in bash mode
- docker-compose exec salt-master bash
