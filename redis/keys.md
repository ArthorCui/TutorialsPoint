#### Syntax
Redis keys commands are used for managing keys in redis. Syntax for using redis keys commands is shown below:
```
redis 127.0.0.1:6379> COMMAND KEY_NAME
```

#### Related Commands
* **DEL** key

> This command deletes the key, if exists

* **DUMP** key

> This command returns a serialized version of the value stored at the specified key.

* **EXISTS** key

> This command checks whether the key exists or not.

* **EXPIRE** key _seconds_

> Expires the key after the specified time

> > 1, if timeout is set for key.

> > 0, if key does not exists or timeout could not set.
> ```
redis 127.0.0.1:6379> EXPIRE tutorialspoint 60
(integer) 1
> ```

* **EXPIREAT** key timestamp

> Expires the key after the specified time. Here time is in Unix timestamp format
> ```
redis 127.0.0.1:6379> EXPIREAT tutorialspoint 1293840000
(integer) 1
EXISTS tutorialspoint
(integer) 0
> ```

* **PEXPIRE** key milliseconds

> Set the expiry of key in milliseconds

> In the above example 5 seconds time is set for the key tutorialspoint. After 5 seconds key will expire automatically.
> ```
redis 127.0.0.1:6379> PEXPIRE tutorialspoint 5000
(integer) 1
> ```

* **KEYS** pattern

> Find all keys matching the specified pattern
> ```
redis 127.0.0.1:6379> KEYS tutorial*
redis 127.0.0.1:6379> KEYS *
> ```

* > **MOVE** key db

> Move a key to another database
> > 1, if key is moved.
> > 0, if key is not moved.

* **PERSIST** key

> Remove the expiration from the key

> > 1, if timeout is removed from key.
> > 0, if key does not exist or does not have an associated timeout.
> ```
redis 127.0.0.1:6379> EXPIRE tutorial1 60
1) (integer) 1
redis 127.0.0.1:6379> TTL tutorial1
1) (integer) 60
redis 127.0.0.1:6379> PERSIST tutorial1
1) (integer) 1
redis 127.0.0.1:6379> TTL tutorial1
1) (integer) -1
> ```

* **PTTL** key

> Get the remaining time in keys expiry in milliseconds.

> TTL in milliseconds.

> > -1, if key does not have expiry timeout.

> > -2, if key does not exist.
> ```
redis 127.0.0.1:6379> EXPIRE tutorialname 1
1) (integer) 1
redis 127.0.0.1:6379> PTTL tutorialname
1) (integer) 999
> ```

* **TTL** key

> Get the remaining time in keys expiry.

> TTL in milliseconds.

> > -1, if key does not have expiry timeout.

> > -2, if key does not exist.
> ```
redis 127.0.0.1:6379> EXPIRE tutorialname 60
1) (integer) 1
redis 127.0.0.1:6379> TTL tutorialname
1) (integer) 59
> ```

* **RANDOMKEY**

> Return a random key from redis

> String, a random key or nil, if database is empty.

* **RENAME** key newkey

> Change the key name

> String reply OK or error.

> It returns an error if old key and new key names are equal or when key does not exist. If new key already exist, then it overwrite the existing key.
> ```
redis 127.0.0.1:6379> RENAME tutorial1 new-tutorial
OK
> ```

* **RENAMENX** key newkey

> Rename key, if new key doesn't exist

> Integer reply 1 or 0.

> > 1, if key is renamed to new key.

> > 0, if new key already exist.
> ```
redis 127.0.0.1:6379> RENAMENX tutorial1 new-tutorial
(integer) 1
redis 127.0.0.1:6379> RENAMENX tutorial2 new-tutorial
(integer) 0
> ```

* **TYPE** key

> Return the data type of value stored in key.
