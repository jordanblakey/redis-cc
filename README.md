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
vi /etc/redis.conf
  append-only
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

### REDIS-CLI

```sh
redis-cli # ENTER CLI
PING # CHECK CONNECTION
ECHO 'Hello World'

# SET KEYS AND CHECK EXISTENCE
SET mykey somevalue
EXISTS mykey
GET mykey

# INCREMENTING/DECRIMENING
SET foo 100
INCR foo
DECR foo

# OBJECTS
SET server:name someserver
GET server:name
SET server:port 8000
GET SERVER:port

# TTL/EXPIRE
SET greeting "Hello World"
GET greeting
EXPIRE greeting 50
TTL greeting # 50, 49, 48...
SETEX greeting 30 "Hello World" # Set value for key and expiration simultaneously
PERSIST greeting # Remove the expiry for a key

# SET MULTIPLE
MSET key1 "HELLO" key2 "WORLD"
GET key2 # "WORLD"
APPEND key1 " WORLD"
GET key1 #"HELLO WORLD"

# RENAME
RENAME key1 greeting
GET key1 #(nil)
GET greeting # "HELLO WORLD"

# LISTS
LPUSH people "Brad"
LPUSH people "Jen"
LPUSH people "Tom"
LRANGE people 0 -1 # Return entire list
LPOP people # "Brad"
RPOP people # "Tom"
LINSERT people AFTER Jen Brad

# SETS
SADD cars "Ford"
SADD cars "Honda"
SADD cars "BMW"
SISMEMBER cars "Ford" # 1
SYSMEMBER cars "Audi" # 0
SMOVE cars cars mycars "Ford"
SREM cars "BMW"
SMEMBERS cars

# SORTED SETS
ZADD users 1981 "Jordan Smith" # Add member Jordan with score of 1981
ZADD users 1971 "John Doe"
ZADD users 1971 "Jack Doe"
ZADD users 1975 "Kate Rogers"
ZRANK users "John Doe"
ZRANGE users 0 -1 # list all
ZINCRBY users 10 "John Doe" # increment score by 10

# HASHES
HSET user:brad name "Brad Smith"
HSET user:brad email "brad@mail.com"
HGET user:brad email
HGETALL user:brad
HMSET user:john name "John Doe" email "jdoe@mail.com" age "25"
HGETALL user:john # get all key value pairs
HINCRBY user:john age 1
HDEL user:john age # delete a key value pair
HVALS user:john # get all values

SAVE # Save snapshot to disk
SAVE 60 1000 # Save every 60 seconds if 1000 records have changed > dump.rdb
FLUSHALL # EMPTY THE CACHE
QUIT
```