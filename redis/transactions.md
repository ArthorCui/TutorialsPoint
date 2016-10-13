####Syntax
Redis transactions allow the execution of a group of commands in a single step. Transactions has two properties in it, which are described below:

> All commands in a transaction are sequentially executed as a single isolated operation. It is not possible that a request issued by another client is served in the middle of the execution of a Redis transaction.

> Redis transaction is also atomic. Atomic means either all of the commands or none are processed.

Redis transaction is initiated by command MULTI and then you need to pass list of commands that should be executed in transaction and after that whole transaction is executed by EXEC command.

######example
```
redis 127.0.0.1:6379> MULTI
OK
redis 127.0.0.1:6379> SET tutorial redis
QUEUED
redis 127.0.0.1:6379> GET tutorial
QUEUED
redis 127.0.0.1:6379> INCR visitors
QUEUED
redis 127.0.0.1:6379> EXEC

1) OK
2) "redis"
3) (integer) 1
```

####Related Commands

* **DISCARD**

> Discard all commands issued after MULTI

* **EXEC**

> Execute all commands issued after MULTI

> Redis EXEC command executes all previously queued commands in a transaction and restores the connection state to normal.

> Return value: Array reply, each element being the reply to each of the commands in the atomic transaction.

* **MULTI**

> Mark the start of a transaction block

> Redis MULTI command marks the start of a transaction block. Subsequent commands will be queued for atomic execution using EXEC.

> Return Value: Simple string reply: always OK.

* **UNWATCH**

> Forget about all watched keys

> Redis UNWATCH command flushes all the previously watched keys for a transaction.

> Return Value: Simple string reply: always OK. 

* **WATCH** key [key ...]

> Watch the given keys to determine execution of the MULTI/EXEC block

> Redis WATCH command marks the given keys to be watched for conditional execution of a transaction.

> Return Value: Simple string reply: always OK. 
