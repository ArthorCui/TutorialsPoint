#Redis Sentinel

Redis Sentinel provides high availability for Redis. In practical terms this means that using Sentinel you can create a Redis deployment that resists without human intervention to certain kind of failures.
Redis Sentinel also provides other collateral tasks such as monitoring, notifications and acts as a configuration provider for clients.

This is the full list of Sentinel capabilities at a macroscopical level (i.e. the big picture):
* **Monitoring**. Sentinel constantly checks if your master and slave instances are working as expected.
* **Notification**. Sentinel can notify the system administrator, another computer programs, via an API, that something is wrong with one of the monitored Redis instances.
* **Automatic failover**. If a master is not working as expected, Sentinel can start a failover process where a slave is promoted to master, the other additional slaves are reconfigured to use the new master, and the applications using the Redis server informed about the new address to use when connecting.
* **Configuration provider**. Sentinel acts as a source of authority for clients service discovery: clients connect to Sentinels in order to ask for the address of the current Redis master responsible for a given service. If a failover occurs, Sentinels will report the new address.

A stable release of Redis Sentinel is shipped since `Redis 2.8`

And offical site see [here](http://redis.io/topics/sentinel)

##Quick Start

Sentinels by default run listening for connections to TCP `port 26379`, so for Sentinels to work, `port 26379` of your servers **must be open** to receive connections from the IP addresses of the other Sentinel instances. Otherwise Sentinels can't talk and can't agree about what to do, so failover will never be performed.

####Running Sentinel

####Configuring Sentinel

A template see [here](sentinel.conf)

```
sentinel monitor mymaster 127.0.0.1 6379 2
sentinel down-after-milliseconds mymaster 60000
sentinel failover-timeout mymaster 180000
sentinel parallel-syncs mymaster 1

sentinel monitor resque 192.168.1.3 6380 4
sentinel down-after-milliseconds resque 10000
sentinel failover-timeout resque 180000
sentinel parallel-syncs resque 5
```

The first line is used to tell Redis to monitor a master called mymaster, that is at `address 127.0.0.1` and `port 6379`, with a **quorum** of 2. Everything is pretty obvious but the quorum argument:
The **quorum** is the number of Sentinels that need to agree about the fact the master is not reachable, in order for really mark the slave as failing, and eventually start a fail over procedure if possible.
However the quorum is only used to detect the failure. In order to actually perform a failover, one of the Sentinels need to be elected leader for the failover and be authorized to proceed. This only happens with the vote of the majority of the Sentinel processes.

> We will never show setups where just two Sentinels are used, since Sentinels always need to talk with the majority in order to start a failover.

> Clients may write indefinitely to both sides, and there is no way to understand when the partition heals what configuration is the right one, in order to prevent a permanent split brain condition.

> So please `deploy at least three Sentinels in three different boxes always`.
