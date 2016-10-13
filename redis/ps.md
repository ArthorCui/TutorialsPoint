####Syntax
Redis pub sub implements the messaging system where senders (in redis terminology called publishers) sends the messages while receivers (subscribers) receive them. The link by which messages are transferred is called channel.

In redis a client can subscribe any number of channels.

######example
```
redis 127.0.0.1:6379> SUBSCRIBE redisChat

Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "redisChat"
3) (integer) 1

redis 127.0.0.1:6379> PUBLISH redisChat "Redis is a great caching technique"
(integer) 1
redis 127.0.0.1:6379> PUBLISH redisChat "Learn redis by tutorials point"
(integer) 1
1) "message"
2) "redisChat"
3) "Redis is a great caching technique"
1) "message"
2) "redisChat"
3) "Learn redis by tutorials point"
```

####Related Commands

* **PSUBSCRIBE** pattern [pattern ...]

> Subscribe to channels matching the given patterns.

> Redis PSUBSCRIBE command is used to subscribe to channels matching the given patterns.

> Following listing shows some supported patterns in redis

> > h?llo subscribes to hello, hallo and hxllo

> > h*llo subscribes to hllo and heeeello

> > h[ae]llo subscribes to hello and hallo, but not hillo

> ```
redis 127.0.0.1:6379> PSUBSCRIBE mychannel
Reading messages... (press Ctrl-C to quit)
1) "psubscribe"
2) "mychannel"
3) (integer) 1
> ```

* **PUBSUB** subcommand [argument [argument ...]]

> Tells the state of pubsub system eg which clients are active on the server.

> Redis PUBSUB command is an introspection command that allows to inspect the state of the Pub/Sub subsystem. It is composed of subcommands that are documented separately.

> ```
redis 127.0.0.1:6379> PUBSUB CHANNELS
(empty list or set)
> ```

* **PUBLISH** channel message

> Post a message to a channel.

> Return Value: Integer reply: the number of clients that received the message.

> ```
redis 127.0.0.1:6379> PUBLISH mychannel "hello, i m here"
(integer) 1
> ```

* **PUNSUBSCRIBE** [pattern [pattern ...]]

> Stop listening for messages posted to channels matching the given patterns.

> Redis PUNSUBSCRIBE command unsubscribes the client from the given patterns, or from all of them if none is given. When no patterns are specified, the client is unsubscribed from all the previously subscribed patterns. In this case, a message for every unsubscribed pattern will be sent to the client.

> Return Value: Array reply.

> ```
redis 127.0.0.1:6379> PUNSUBSCRIBE mychannel 
1) "punsubscribe"
2) "a"
3) (integer) 1
> ```

* **SUBSCRIBE** channel [channel ...] 

> Listen for messages published to the given channels.

> Return Value: Array reply.

> ```
redis 127.0.0.1:6379> SUBSCRIBE mychannel 
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "mychannel"
3) (integer) 1
1) "message"
2) "mychannel"
3) "a"
> ```

* **UNSUBSCRIBE** [channel [channel ...]]

> Stop listening for messages posted to the given channels.

> Redis UNSUBSCRIBE command unsubscribes the client from the given channels, or from all of them if none is given.

> Return Value: Array reply.

> ```
redis 127.0.0.1:6379> UNSUBSCRIBE mychannel 
1) "unsubscribe"
2) "a"
3) (integer) 0
> ```