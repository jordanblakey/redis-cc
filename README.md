# Redis Crash Course

## What is Redis?

- open source
- an in-memory data structure store
- used as a:
  - database
  - cache
  - message broker

### Supported Data Types

It supports strings, hashses, lists, sets, sorted sets, bitmaps, hyperloglogs and geospatial indexes with radius queries.

### Features

- built in replication
- Lua scripting
- LRU eviction
- different levels of on-disk persistence
- high availability via Redis Sentinel & Redis Cluster

## Installation

```sh
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
make install
```

## Commands

### Executables

`redis-server` is the Redis Server itself.<br>
`redis-sentinel` is the Redis Sentinel executable (monitoring and failover).<br>
`redis-cli` is the command line interface utility to talk with Redis.<br>
`redis-benchmark` is used to check Redis performances.<br>
`redis-check-aof` and redis-check-dump are useful in the rare event of corrupted data files.

### Running the server

`touch /etc/redis.conf` create a configuration file
`redis-server /etc/redis.conf` start the redis server with a conf file
`tail -f /var/log/redis/redis-server.log` tail the log file.

### REPL

`redis-cli`
`ping`
`set mykey somevalue`
`get mykey`
`ECHO 'Hello World'`
`QUIT`