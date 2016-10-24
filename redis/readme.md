#Documentation
Redis is an open source, advanced key-value store and a serious solution for building high-performance, scalable web applications.

Redis has three main peculiarities that set it apart from much of its competition:

* Redis holds its database entirely in memory, using the disk only for persistence.

* Redis has a relatively rich set of data types when compared to many key-value data stores.

* Redis can replicate data to any number of slaves.

#Redis Advantages
* Exceptionally Fast : Redis is very fast and can perform about 110000 SETs per second, about 81000 GETs per second.

* Supports Rich data types : Redis natively supports most of the datatypes that most developers already know like list, set, sorted set, hashes. This makes it very easy to solve a variety of problems because we know which problem can be handled better by which data type.

* Operations are atomic : All the Redis operations are atomic, which ensures that if two clients concurrently access Redis server will get the updated value.

* MultiUtility Tool : Redis is a multi utility tool and can be used in a number of usecases like caching, messaging-queues (Redis natively supports Publish/ Subscribe ), any short lived data in your application like web application sessions, web page hit counts, etc.

#Guide
* [Environment](#environment)
* [Configuration](#configuration)
* [Data Types](#dataTypes)
* [Basic Commands](#basic-commands)
* [Advanced Commands](#advanced-commands)

##Environment
Sample use Ubuntu...

Windows version see [here](#windows)
```
$sudo apt-get update
$sudo apt-get install redis-server
```
else, we can download tar zip file and use make install manucal
```
$ wget http://download.redis.io/releases/redis-3.2.4.tar.gz
$ tar xzf redis-3.2.4.tar.gz
$ cd redis-3.2.4
$ make
```
After installation completed, the default server port is 6379. So 127.0.0.1 is your machine's IP address and 6379 is port on which redis server is running. Now type the PING command as shown below.
```
$redis-cli
$redis-cli -h 127.0.0.1 -p 6379
```

```
redis 127.0.0.1:6379> ping
PONG
```

##Configuration
Redis is able to start without a configuration file using a built-in default configuration, however this setup is only recommended for testing and development purposes.
The proper way to configure Redis is by providing a Redis configuration file, usually called redis.conf.
The redis.conf file contains a number of directives that have a very simple format:

```
keyword argument1 argument2 ... argumentN
```

Since Redis 2.6 it is possible to also pass Redis configuration parameters using the command line directly. This is very useful for testing purposes. The following is an example that starts a new Redis instance using port 6380 as a slave of the instance running at 127.0.0.1 port 6379.
```
./redis-server --port 6380 --slaveof 127.0.0.1 6379
```

Changing Redis configuration while the server is running
It is possible to reconfigure Redis on the fly without stopping and restarting the service, or querying the current configuration programmatically using the special commands CONFIG SET and CONFIG GET
Not all the configuration directives are supported in this way, but most are supported as expected. Please refer to the CONFIG SET and CONFIG GET pages for more information.
Note that modifying the configuration on the fly has no effects on the redis.conf file so at the next restart of Redis the old configuration will be used instead.
Make sure to also modify the redis.conf file accordingly to the configuration you set using CONFIG SET. You can do it manually, or starting with Redis 2.8, you can just use CONFIG REWRITE, which will automatically scan your redis.conf file and update the fields which don't match the current configuration value. Fields non existing but set to the default value are not added. Comments inside your configuration file are retained.
```
redis 127.0.0.1:6379> CONFIG GET loglevel

1) "loglevel"
2) "notice"

redis 127.0.0.1:6379> CONFIG GET *

  1) "dbfilename"
  2) "dump.rdb"
  ......

redis 127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE

redis 127.0.0.1:6379> CONFIG SET loglevel "notice"
OK
redis 127.0.0.1:6379> CONFIG GET loglevel

1) "loglevel"
2) "notice"

```

##DataTypes
Redis supports 5 types of data types, which are described below:
The detail see [here](http://redis.io/topics/data-types-intro)

###Strings
Redis string is a sequence of bytes. Strings in Redis are binary safe, meaning they have a known length not determined by any special terminating characters, so you can store anything up to 512 megabytes in one string.
```
redis 127.0.0.1:6379> SET name "tutorialspoint"
OK
redis 127.0.0.1:6379> GET name
"tutorialspoint"
```

**NOTE:**<em> A String value can be at max 512 Megabytes in length.</em>

###Hashes
A Redis hash is a collection of key value pairs. Redis Hashes are maps between string fields and string values, so they are used to represent objects

While hashes are handy to represent objects, actually the number of fields you can put inside a hash has no practical limits (other than available memory), so you can use hashes in many different ways inside your application.
The command HMSET sets multiple fields of the hash, while HGET retrieves a single field. HMGET is similar to HGET but returns an array of values:

```
redis 127.0.0.1:6379> HMSET user:1 username tutorialspoint password tutorialspoint points 200
OK
redis 127.0.0.1:6379> HGETALL user:1

1) "username"
2) "tutorialspoint"
3) "password"
4) "tutorialspoint"
5) "points"
6) "200"
```

**NOTE:**<em> Every hash can store up to 232 - 1 field-value pairs (more than 4 billion).</em>

###Lists
Redis Lists are simply lists of strings, sorted by insertion order. You can add elements to a Redis List on the head or on the tail.


```
redis 127.0.0.1:6379> lpush tutoriallist redis
(integer) 1
redis 127.0.0.1:6379> lpush tutoriallist mongodb
(integer) 2
redis 127.0.0.1:6379> lpush tutoriallist rabitmq
(integer) 3
redis 127.0.0.1:6379> lrange tutoriallist 0 10

1) "rabitmq"
2) "mongodb"
3) "redis"
```


**NOTE:**<em> The max length of a list is 232 - 1 elements (4294967295, more than 4 billion of elements per list).</em>

###Sets
Redis Sets are an unordered collection of Strings. In redis you can add, remove, and test for existence of members in O(1) time complexity.

```
redis 127.0.0.1:6379> sadd tutoriallist redis
(integer) 1
redis 127.0.0.1:6379> sadd tutoriallist mongodb
(integer) 1
redis 127.0.0.1:6379> sadd tutoriallist rabitmq
(integer) 1
redis 127.0.0.1:6379> sadd tutoriallist rabitmq
(integer) 0
redis 127.0.0.1:6379> smembers tutoriallist

1) "rabitmq"
2) "mongodb"
3) "redis"
```

**NOTE:**<em> In the above example rabitmq is added twice but due to unique property of set it is added only once.

The max number of members in a set is 232 - 1 (4294967295, more than 4 billion of members per set).</em>

###Sorted Sets
Redis Sorted Sets are, similarly to Redis Sets, non repeating collections of Strings. The difference is that every member of a Sorted Set is associated with score, that is used in order to take the sorted set ordered, from the smallest to the greatest score. While members are unique, scores may be repeated.

However while elements inside sets are not ordered, every element in a sorted set is associated with a floating point value, called the score (this is why the type is also similar to a hash, since every element is mapped to a value).
Moreover, elements in a sorted sets are taken in order (so they are not ordered on request, order is a peculiarity of the data structure used to represent sorted sets). They are ordered according to the following rule:

* If A and B are two elements with a different score, then A > B if A.score is > B.score.
* If A and B have exactly the same score, then A > B if the A string is lexicographically greater than the B string. A and B strings can't be equal since sorted sets only have unique elements.

```
redis 127.0.0.1:6379> zadd tutoriallist 0 redis
(integer) 1
redis 127.0.0.1:6379> zadd tutoriallist 0 mongodb
(integer) 1
redis 127.0.0.1:6379> zadd tutoriallist 0 rabitmq
(integer) 1
redis 127.0.0.1:6379> zadd tutoriallist 0 rabitmq
(integer) 0
redis 127.0.0.1:6379> ZRANGEBYSCORE tutoriallist 0 1000

1) "redis"
2) "mongodb"
3) "rabitmq"
```

##Basic-Commands
* [Keys](keys.md)
* [Strings](strings.md)
* [Hashes](hashes.md)
* [Lists](lists.md)
* [Sets](sets.md)
* [Sorted Sets](sorted-sets.md)
* [HyperLogLog](hyperlog.md)
* [Pub/Sub](ps.md)
* [Transactions](transactions.md)
* [Scripting](scripting.md)
* [Connection](connection.md)
* [Server](server.md)

##Advanced-Commands
* [Redis Sentinel](sentinel.md)

##Windows
BTW, if you install the windows version, maybe you should use [chocolatey](https://chocolatey.org/packages/redis-64) to install windows redis nuget packages.
And the detail see the offical site [here](http://redis.io/download)

```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

choco install redis-64
```

####Install windows service

```
#install:
redis-server --service-install redis.windows.conf --loglevel verbose
redis-server --service-install --service-name Redis6380 --port 6380

#uninstall:
redis-server --service-uninstall --service-name Redis6380 --port 6380

#service `start` | `stop`
redis-server --service start | stop

#install redis sentinel
redis-server --service-install --service-name redisSentinel sentinel.conf --sentinel
```

