### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

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
+--- 📁 distribution_config
+------ 📄 config.json
+------ 📄 private.json
+------ 📄 server_manifest.json
+--- 📁 file_processing_driver [ ON HOLD ]
+--- 📁 file_store_bk_driver
+--- 📁 file_store_server
```
#### Files in Distribution Config

- **config.json**
```JSON
{
    "server_id":"FS0000"
}
```
- **private.json**
```JSON
{
    "file_access_token_key":"<JWT token private key for file access>",
    "user_token_key":"<JWT token private key for User verification>"
}
```
- **server_manifest.json**
```JS
{
    "port":<valid port number>,   //server will run on this port, if env.PORT is not defined
    "fastify_options":{
        "logger": true,
        "file": "./server/logs"
    }
}
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
  "contactPoints":["127.0.0.1:9042"],
  "localDataCenter":"datacenter1",
  "credentials": { "username": "cassandra", "password": "cassandra" },
  "keyspace": "ks1"
})
```

#### Commands to configure keyspace with tables

Create KeySpace
```CQL
CREATE KEYSPACE ks1;
DESCRIBE KEYSPACES;
```

Create Tables
```CQL
USE ks1;
CREATE TABLE ks1.file_store (
    id text PRIMARY KEY,
    buffer blob,
    owner_id text,
    time_added bigint,
    time_expire bigint
);
DESCRIBE TABLE ks1.file_store;
```

Add Indexes
```
Will do this later
```

### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)
