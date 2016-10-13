####Syntax
Redis connection commands are basically used to manage client connections with redis server.

Following example explains how a client authenticate itself to redis server and checks whether server is running or not.

######example
```
redis 127.0.0.1:6379> AUTH "password"
OK
redis 127.0.0.1:6379> ECHO "Hello World"
"Hello World"
redis 127.0.0.1:6379> PING
PONG
redis 127.0.0.1:6379> SELECT 1
OK
redis 127.0.0.1:6379[1]>
redis 127.0.0.1:6379> QUIT
OK
```

####Related Commands

* **AUTH** password

> Redis AUTH command is used to authenticate to the server with given password. If password matches the password in the configuration file, the server replies with the OK status code and starts accepting commands. Otherwise, an error is returned and the clients needs to try a new password.

> ```
redis 127.0.0.1:6379> AUTH PASSWORD
(error) ERR Client sent AUTH, but no password is set
redis 127.0.0.1:6379> CONFIG SET requirepass "mypass"
OK
redis 127.0.0.1:6379> AUTH mypass
Ok
> ```

* **ECHO** message

> Same like linux's command

> see the [example](#example)

* **PING**

> Check whether server is running or not

> see the [example](#example)


* **SELECT** index

> Change the selected database for the current connection

> Redis SELECT command is used to select the DB with having the specified zero-based numeric index. New connections always use DB 0.

> see the [example](#example)

* **QUIT**

> Redis QUIT command ask the server to close the connection. The connection is closed as soon as all pending replies have been written to the client.

> see the [example](#example)
