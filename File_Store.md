# File Store

This system is a microservice built on the Cassandra database and can store any type of file (each file size can be up to 2GB)

The system uses Cassandra as Cassandra is a highly scalable database, and deliver uncompromised throughput and redundancy.

## Components

### file_store_bk_driver

[Repo of file_store_bk_driver](https://bitbucket.org/rishavbhowmiktgs/file_store_bk_driver/src/master/)

This package handles the io operations on the database and also takes care of access rights of the respective files.

### file_store_server

[Repo for file_store_server](https://bitbucket.org/rishavbhowmiktgs/file_store_server/src/master/)

This package is the server which allows the front end to access the file_store_system, and also performs user validation and authorizations.
This package is built on file_store_bk_driver

### Distribution Folder

This folder stores the JSON files that define the state of individual server + driver combo since the system is designed for horizontal scaling in all the layers.
```
+--- 📁 private
+------ 📄 config.json
+------ 📄 private.json
+------ 📄 server_manifest.json
```

## Deployment guide

### Database setup

#### For Docker

[cassandra with bitnami docker](https://hub.docker.com/r/bitnami/cassandra/)

//Docker compose file for single cluseter key space
```YAML
version: '2'

services:
  cassandra:
    image: 'docker.io/bitnami/cassandra:3-debian-10'
    ports:
      - '7000:7000'
      - '9042:9042'
    volumes:
      - 'cassandra_data:/bitnami'
    environment:
      - CASSANDRA_SEEDS=cassandra
      - CASSANDRA_PASSWORD_SEEDER=yes
      - CASSANDRA_PASSWORD=cassandra
volumes:
  cassandra_data:
    driver: local
```
#### For Fully managed database

- [https://aws.amazon.com/keyspaces/](https://aws.amazon.com/keyspaces/)

#### DB Connection configration template for Cassandra Driver

```JSON
{
  contactPoints:['127.0.0.1:9042'],
  localDataCenter:"datacenter1",
  credentials: { username: 'cassandra', password: 'cassandra' },
  keyspace: 'ks1'
})
```

