####Syntax
Redis Hashes are maps between string fields and string values, so they are the perfect data type to represent objects

In redis every hash can store up to more than 4 billion field-value pairs.
```
redis 127.0.0.1:6379> HMSET tutorialspoint name "redis tutorial" description "redis basic commands for caching" likes 20 visitors 23000
OK
redis 127.0.0.1:6379> HGETALL tutorialspoint

1) "name"
2) "redis tutorial"
3) "description"
4) "redis basic commands for caching"
5) "likes"
6) "20"
7) "visitors"
8) "23000"
```

####Related Commands
* **HDEL** key field1 [field2]

> Delete one or more hash fields
> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HDEL myhash field1
(integer) 1
redis 127.0.0.1:6379> HDEL myhash field2
(integer) 1
> ```

* **HEXISTS** key field

> Determine whether a hash field exists or not

> > 1, if the hash contains field.

> > 0 if the hash does not contain field, or key does not exist.

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HEXISTS myhash field1
(integer) 1
redis 127.0.0.1:6379> HEXISTS myhash field2
(integer) 0
> ```

* **HGET** key field

> Get the value of a hash field stored at specified key

> String reply, the value associated with field, or nil when field is not present in the hash or key does not exist.

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HGET myhash field1
"foo"
redis 127.0.0.1:6379> HEXISTS myhash field2
(nil)
> ```

* **HGETALL** key

> Get all the fields and values stored in a hash at specified key

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSET myhash field2 "bar"
(integer) 1
redis 127.0.0.1:6379> HGETALL myhash
1) "field1"
2) "Hello"
3) "field2"
4) "World"
> ```

* **HINCRBY** key field increment

> Increment the integer value of a hash field by the given number

> ```
redis 127.0.0.1:6379> HSET myhash field1 20
(integer) 1
redis 127.0.0.1:6379> HINCRBY myhash field 1
(integer) 21
redis 127.0.0.1:6379> HINCRBY myhash field -1
(integer) 20
> ```

* **HINCRBYFLOAT** key field increment

> Increment the float value of a hash field by the given amount

> ```
redis 127.0.0.1:6379> HSET myhash field 20.50
(integer) 1
redis 127.0.0.1:6379> HINCRBYFLOAT mykey field 0.1
"20.60"
> ```

* **HKEYS** key

> Get all the fields in a hash

> ```
redis 127.0.0.1:6379> HKEYS KEY_NAME FIELD_NAME INCR_BY_NUMBER 

redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSET myhash field2 "bar"
(integer) 1
redis 127.0.0.1:6379> HKEYS myhash
1) "field1"
2) "field2"
> ```

* **HLEN** key

> Get the number of fields in a hash

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSET myhash field2 "bar"
(integer) 1
redis 127.0.0.1:6379> HLEN myhash
(integer) 2
> ```

* **HMGET** key field1 [field2]

> Get the values of all the given hash fields

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSET myhash field2 "bar"
(integer) 1
redis 127.0.0.1:6379> HMGET myhash field1 field2 nofield
1) "foo"
2) "bar"
3) (nil)
> ```

* **HMSET** key field1 value1 [field2 value2]

> Set multiple hash fields to multiple values

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo" field2 "bar"
OK
redis 127.0.0.1:6379> HGET myhash field1
"foo"
redis 127.0.0.1:6379> HMGET myhash field2
"bar"
> ```

* **HSET** key field value

> Set the string value of a hash field

> > 1 if field is a new field in the hash and value was set.

> > 0 if field already exists in the hash and the value was updated.

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
OK
redis 127.0.0.1:6379> HGET myhash field1
"foo"
> ```

* **HSETNX** key field value

> Set the value of a hash field, only if the field does not exist

> > 1 if field is a new field in the hash and value was set.

> > 0 if field already exists in the hash and no operation was performed.

> ```
redis 127.0.0.1:6379> HSETNX myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSETNX myhash field1 "bar"
(integer) 0
redis 127.0.0.1:6379> HGET myhash field1
"foo"
> ```

* **HVALS** key

> Get all the values in a hash

> Array reply, list of values in the hash, or an empty list when key does not exist.

> ```
redis 127.0.0.1:6379> HSET myhash field1 "foo"
(integer) 1
redis 127.0.0.1:6379> HSET myhash field2 "bar"
(integer) 1
redis 127.0.0.1:6379> HVALS myhash
1) "foo"
2) "bar"
> ```
* **HSCAN** key cursor [MATCH pattern] [COUNT count]

> Incrementally iterate hash fields and associated values
