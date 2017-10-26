#### Syntax

Server infomation example:

###### example
```
redis 127.0.0.1:6379> INFO

# Server
redis_version:2.8.13
...

# Clients
connected_clients:1
...

# Memory
used_memory:589016
...

# Persistence
loading:0
rdb_changes_since_last_save:3
...

# Stats
total_connections_received:24
total_commands_processed:294
...

# Replication
role:master
connected_slaves:0
...

# CPU
used_cpu_sys:10.49
used_cpu_user:4.96
...

# Keyspace
db0:keys=94,expires=1,avg_ttl=41638810
db1:keys=1,expires=0,avg_ttl=0
db3:keys=1,expires=0,avg_ttl=0
```

#### Related Commands

* **BGREWRITEAOF**

> Asynchronously rewrite the append-only file

> Redis BGREWRITEAOF command instruct Redis to start an Append Only File rewrite process. The rewrite will create a small optimized version of the current Append Only File. If BGREWRITEAOF fails, no data gets lost as the old AOF will be untouched. The rewrite will be only triggered by Redis if there is not already a background process doing persistence.

* **BGSAVE**

> Asynchronously save the dataset to disk

> Redis BGSAVE command save the DB in background. The OK code is immediately returned. Redis forks, the parent continues to serve the clients, the child saves the DB on disk then exits. A client my be able to check if the operation succeeded using the LASTSAVE command.

* **CLIENT KILL** [ip:port] [ID client-id]

> Kill the connection of a client

> With Redis 2.8.12 or greater, the command can be run with multiple options as shown below:

> * CLIENT KILL ADDR ip:port. This is exactly the same as the old three-arguments behavior.

> * CLIENT KILL ID client-id. Allows to kill a client by its unique ID field, which was introduced in the CLIENT LIST command starting from Redis 2.8.12.

> * CLIENT KILL TYPE type, where type is one of normal, slave, pubsub. This closes the connections of all the clients in the specified class. Note that clients blocked into the MONITOR command are considered to belong to the normal class.

> * CLIENT KILL SKIPME yes/no. By default this option is set to yes, that is, the client calling the command will not get killed, however setting this option to no will have the effect of also killing the client calling the command.

* **CLIENT LIST**

> Get the list of client connections connection to the server

> ```
127.0.0.1:6379> client list
addr=127.0.0.1:40462 fd=5 name= age=2317639 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 events=r cmd=ping
addr=127.0.0.1:40464 fd=6 name= age=2317639 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 events=r cmd=subscribe
addr=127.0.0.1:40466 fd=7 name= age=2317639 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 events=r cmd=publish
addr=127.0.0.1:40468 fd=8 name= age=2317639 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 events=r cmd=subscribe
addr=127.0.0.1:6380 fd=9 name= age=2317629 idle=0 flags=M db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 events=r cmd=publish
addr=127.0.0.1:40562 fd=10 name= age=1086 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 events=r cmd=client
> ```

* **CLIENT GETNAME**

> Get the name of current connection

> Redis CLIENT GETNAME command returns the name of the current connection as set by CLIENT SETNAME. Since every new connection starts without an associated name, if no name was assigned a null bulk reply is returned.

* **CLIENT PAUSE timeout**

> Stop processing commands from clients for specified time

> Redis CLIENT PAUSE command is a connections control command able to suspend all the Redis clients for the specified amount of time (in milliseconds). The command performs the following actions:

> * It stops processing all the pending commands from normal and pub/sub clients. However interactions with slaves will continue normally.

> * However it returns OK to the caller ASAP, so the CLIENT PAUSE command execution is not paused by itself.

> * When the specified amount of time has elapsed, all the clients are unblocked: this will trigger the processing of all the commands accumulated in the query buffer of every client during the pause.

* **CLIENT SETNAME** connection-name

> Set the current connection name

* **CLUSTER SLOTS**

> Get array of Cluster slot to node mappings

> Redis `CLUSTER SLOTS` returns array reply of current cluster state.

* **COMMAND**

> Get array of Redis command details

* **COMMAND COUNT**

> Get total number of Redis commands

* **COMMAND GETKEYS**

> Extract keys given a full Redis command

> ```
redis 127.0.0.1:6379> COMMAND GETKEYS MSET a b c d e f 
1) "a"
2) "c"
3) "e"
> ```

* **COMMAND INFO** command-name [command-name ...]

> Get array of specific Redis command details

* **CONFIG GET** parameter

> Get the value of a configuration parameter

* **CONFIG REWRITE**

> Rewrite the configuration file with the in memory configuration

* **CONFIG SET** parameter value

> Set a configuration parameter to the given value

* **CONFIG RESETSTAT**

> Reset the stats returned by INFO

* **DBSIZE**

> Return the number of keys in the selected database

* **DEBUG SEGFAULT**

> Make the server crash

> ```
redis 127.0.0.1:6379> DEBUG SEGFAULT 
Could not connect to Redis at 127.0.0.1:6379: Connection refused
not connected>
> ```

* **FLUSHALL**

> Remove all keys from all databases

* **FLUSHDB**

> Remove all keys from the current database

* **INFO** [section]

> Get information and statistics about the server

* **LASTSAVE**

> Get the UNIX time stamp of the last successful save to disk

* **MONITOR**

> Listen for all requests received by the server in real time

* **ROLE**

> Return the role of the instance in the context of replication

> The command returns an array of elements. The first element is the role of the instance, as one of the following three strings:

> * master

> * slave

> *sentinel

* **SAVE**

> Synchronously save the dataset to disk

* **SHUTDOWN [NOSAVE] [SAVE]**

> Synchronously save the dataset to disk and then shut down the server

* **SLAVEOF** host port

> Make the server a slave of another instance, or promote it as master

* **SLOWLOG** subcommand [argument]

> Manages the Redis slow queries log

> The Redis Slow Log is a system to log queries that exceeded a specified execution time. The execution time does not include I/O operations like talking with the client, sending the reply and so forth, but just the time needed to actually execute the command (this is the only stage of command execution where the thread is blocked and can not serve other requests in the meantime). You can configure the slow log with two parameters: slowlog-log-slower-than tells Redis what is the execution time, in microseconds, to exceed in order for the command to get logged. Note that a negative number disables the slow log, while a value of zero forces the logging of every command. slowlog-max-len is the length of the slow log. The minimum value is zero. When a new command is logged and the slow log is already at its maximum length, the oldest one is removed from the queue of logged commands in order to make space. The configuration can be done by editing redis.conf or while the server is running using the CONFIG GET and CONFIG SET commands.

* **SLAVEOF** host port

> Make the server a slave of another instance, or promote it as master

> Redis SLAVEOF command can change the replication settings of a slave on the fly. If a Redis server is already acting as slave, the command SLAVEOF NO ONE will turn off the replication, turning the Redis server into a MASTER. In the proper form SLAVEOF hostname port will make the server a slave of another server listening at the specified hostname and port. If a server is already a slave of some master, SLAVEOF hostname port will stop the replication against the old server and start the synchronization against the new one, discarding the old dataset.

* **SYNC**

> Redis SYNC command used to sync slave to master.

* **TIME**

> Return the current server time