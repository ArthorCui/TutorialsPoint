#### Syntax
Redis strings commands are used for managing string values in redis. Syntax for using redis string commands is shown below:
```
redis 127.0.0.1:6379> COMMAND KEY_NAME
redis 127.0.0.1:6379> SET tutorialspoint redis
OK
redis 127.0.0.1:6379> GET tutorialspoint
"redis"
```

#### Related Commands
* **SET** key value

> This command sets the value at the specified key

> In SET command there are many options available, that modify the behaviour of command. Basic syntax of SET command with available options is shown below:
> ```
redis 127.0.0.1:6379> SET KEY VALUE [EX seconds] [PX milliseconds] [NX|XX]
> ```

> > EX seconds - Set the specified expire time, in seconds.

> > PX milliseconds - Set the specified expire time, in milliseconds.

> > NX - Only set the key if it does not already exist.

> > XX - Only set the key if it already exist.

> Above example will set the key tutorialspoint, with expiry of 60 seconds, if the key does not exist.

* **GET** key

> Get the value of a key.

* **GETRANGE** key start end

> Get a substring of the string stored at a key
> ```
redis 127.0.0.1:6379> SET mykey "This is my test key"
OK
redis 127.0.0.1:6379> GETRANGE mykey 0 3
"This"
redis 127.0.0.1:6379> GETRANGE mykey 0 -1
"This is my test key"
> ```

* **GETSET** key value

> Set the string value of a key and return its old value

> Simple string reply, old value of key. If key does not exist, then nil is returned.
> ```
redis 127.0.0.1:6379> GETSET mynewkey "This is my test key"
(nil)
redis 127.0.0.1:6379> GETSET mynewkey "This is my new value to test getset"
"This is my test key"
> ```

* **GETBIT** key offset

> Returns the bit value at offset in the string value stored at key

* **MGET** key1 [key2...]

> Get the values of all the given keys

> ```
redis 127.0.0.1:6379> SET key1 "hello"
OK
redis 127.0.0.1:6379> SET key2 "world"
OK
redis 127.0.0.1:6379> MGET key1 key2 someOtherKey
1) "Hello"
2) "World"
3) (nil)
> ```

* **SETBIT** key offset value

> Sets or clears the bit at offset in the string value stored at key

> ```
redis 127.0.0.1:6379> SETBIT mykey 7 1
(integer) 0
redis 127.0.0.1:6379> GETBIT mykey 0
(integer) 0
redis 127.0.0.1:6379> GETBIT mykey 7
(integer) 1
redis 127.0.0.1:6379> GETBIT mykey 100
(integer) 0
> ```

* **SETEX** key seconds value

> Set the value with expiry of a key

> Simple string reply. OK, if value is set in key or Null, if value does not set.

> ```
redis 127.0.0.1:6379> SETEX mykey 60 redis
OK
redis 127.0.0.1:6379> TTL mykey
60
redis 127.0.0.1:6379> GET mykey
"redis
> ```

* **SETNX** key value

> Set the value of a key, only if the key does not exist

> > 1, if the key is set.

> > 0, if the key is not set.

> ```
redis 127.0.0.1:6379> SETNX mykey redis
(integer) 1
redis 127.0.0.1:6379> SETNX mykey mongodb
(integer) 0
redis 127.0.0.1:6379> GET mykey
"redis"
> ```

* **SETRANGE** key offset value

> Overwrite part of a string at key starting at the specified offset

> Integer reply, the length of the string after it was modified by the command.

> ```
redis 127.0.0.1:6379> SET key1 "Hello World"
OK
redis 127.0.0.1:6379> SETRANGE key1 6 "Redis"
(integer) 11
redis 127.0.0.1:6379> GET key1
"Hello Redis"
> ```

* **STRLEN** key

> Get the length of the value stored in a key

* **MSET** key value [key value ...]

> Set multiple keys to multiple values

> ```
redis 127.0.0.1:6379> MSET key1 "Hello" key2 "World"
OK
redis 127.0.0.1:6379> GET key1
"Hello"
redis 127.0.0.1:6379> GET key2
1) "World"
> ```

* **MSETNX** key value [key value ...]

> Set multiple keys to multiple values, only if none of the keys exist

> > 1, if all keys are set in redis

> > 0, if no keys are set in redis

> ```
redis 127.0.0.1:6379> MSETNX key1 "Hello" key2 "world"
(integer) 1
redis 127.0.0.1:6379> MSETNX key2 "worlds" key3 "third key"
(integer) 0
redis 127.0.0.1:6379> MGET key1 key2 key3
1) "Hello"
2) "world"
3) (nil)
> ```

* **PSETEX** key milliseconds value

> Set the value and expiration in milliseconds of a key

> ```
redis 127.0.0.1:6379> PSETEX mykey 1000 "Hello"
OK
redis 127.0.0.1:6379> PTTL mykey
999
redis 127.0.0.1:6379> GET mykey
1) "Hello"
> ```

* **INCR** key

> Increment the integer value of a key by one

> ```
redis 127.0.0.1:6379> SET visitors 1000
OK
redis 127.0.0.1:6379> INCR visitors
(integer) 1001
redis 127.0.0.1:6379> GET visitors
(integer) 1001
> ```

* **INCRBY** key increment

> Increment the integer value of a key by the given amount

> ```
redis 127.0.0.1:6379> SET visitors 1000
OK
redis 127.0.0.1:6379> INCRBY visitors 5
(integer) 1005
redis 127.0.0.1:6379> GET visitors
(integer) 1005
> ```

* **INCRBYFLOAT** key increment

> Increment the float value of a key by the given amount

> ```
redis 127.0.0.1:6379> SET visitors 1000.20
OK
redis 127.0.0.1:6379> INCRBYFLOAT visitors .50
1000.70
redis 127.0.0.1:6379> GET visitors
1000.70
> ```

* **DECR** key

> Decrement the integer value of a key by one, contruy

* **DECRBY** key decrement

> Decrement the integer value of a key by the given number

> ```
redis 127.0.0.1:6379> SET visitors 1000
OK
redis 127.0.0.1:6379> DECRBY visitors 5
(integer) 995
> ```

* **APPEND** key value

> Append a value to a key

> ```
redis 127.0.0.1:6379> SET mykey "hello"
OK
redis 127.0.0.1:6379> APPEND mykey " tutorialspoint"
(integer) 20
redis 127.0.0.1:6379> GET mykey 
"hello tutorialspoint"
> ```
