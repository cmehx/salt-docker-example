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

## Usage Example

### Install a pkg

#### CLI

To install docker to your minions
```
salt '*' pkg.install docker.io
```

#### File

To install a package from file create a file at /srv/salt/emacs.sls
add this inside
```
emacs:
  pkg.installed
```
then run:
```
salt '*' state.sls emacs
```

##### Other tools
```
salt '*' pkg.list_pkgs // list install pkgs
salt '*' sys.doc ssh // get the doc
salt '*' service.status docker // same as systemctl
```

##### Mysql Example

Salt mysql module offial doc:
https://docs.saltproject.io/en/latest/ref/modules/all/salt.modules.mysql.html

To get more information mysql configuration:
https://www.digitalocean.com/community/tutorials/saltstack-infrastructure-creating-salt-states-for-mysql-database-servers

- Install
```
salt '*' pkg.install mysql-server
salt '*' pkg.install python3-mysqldb // require for mysql salt module
salt '*' pkg.install debconf-utils
```

- Restart minion and master services

- Check Mysql install

run:
```
salt '*' mysql.db_create 'test'
salt '*' mysql.db_list
```

result:
```
vagrant-salt-minion:
    - information_schema
    - mysql
    - performance_schema
    - sys
    - test
```
