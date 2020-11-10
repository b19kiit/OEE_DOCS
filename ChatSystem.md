### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)

# Chat System

Realtime consistent Messaging system with assured Atomicity and scaliblity.

## Database
Chat System uses MySQL RDBMS to store it's message data of the users, and the system is designed to work in compliance with InnoDB Engine.

**Why MySQL on InnoDB?**
Chat messages require to be consistent, and their retrival is supposed to be consistent and flexibal.

In the messages table we assigned and `UNSIGNED INTEGER` as PRIMARY_KEY, these primary key are always assigned sequentialy, and any write operation on DB blocks the table from performing any operation on engaged enitite collections hence completely terminating any possiblity of missing messages.

Also MySQL allows Master Slave replication and sharding, making it potentially very scalable and avaiable.

**Where to deploy MySQL Instance?**
MySQL instance is available in all major Cloud-service-proiders, at affordable rates. And can be deployed as containers, dedicated instances etc

>  ***Reccomended*** : [AWS Aurora](https://aws.amazon.com/rds/aurora/?aurora-whats-new.sort-by=item.additionalFields.postDateTime&aurora-whats-new.sort-order=desc) it's fully managed and can scale upto 128TB

### Deploying the DataBase

Register remort MySQL client

Create a Database
```sql
CREATE DATABASE <db_name>;
USE <db_name>;
```

Create Table messages in Database <db_name>
```sql
CREATE TABLE IF NOT EXISTS messages(
   _id INT UNSIGNED NOT NULL AUTO_INCREMENT,
   sender_id VARCHAR(32) NOT NULL,
   reciver_id VARCHAR(32) NOT NULL,
   sent_at INT UNSIGNED NOT NULL,
   recived_at INT UNSIGNED,
   data LONGBLOB,
   PRIMARY KEY (_id)
);
```

Create indexs on messages table
```sql
CREATE INDEX message_time_index ON messages (sent_at);
```

## Chat System Backend Driver

[Repo](https://bitbucket.org/rishavbhowmiktgs/chat_system_bk_driver/src/master/)

Chat System Backend Driver is a component of the Chat System Backend, it performs operations on the Database.

## Chat System Server

[Repo](https://bitbucket.org/rishavbhowmiktgs/chat_system_server/src)

Chat System Server is another component of Chat System Backend and is built on Chat System Backend Driver. It is a server built using socket.io and allows Chat system Frontend driver IO, user authorization & other network-specific tasks. This component ensures a continues websocket connection with the clients, to enusre low latency & save bandwidth.

## Chat System Frontend Driver

[Repo](https://bitbucket.org/rishavbhowmiktgs/chat_system_front_end_driver/src/master/)

This component run on socket.io and allows user to connect chat_system backend


### [<INDEX](https://b19kiit.github.io/OEE_DOCS/)
