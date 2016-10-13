####Syntax
Redis HyperLogLog is a algorithm that use randomization in order to provide an approximation of the number of unique elements in a set using just a constant, and small, amount of memory.

HyperLogLog provides a very good approximation of the cardinality of a set even using a very small amount of memory around 12 kbytes per key with a standard error of 0.81% and there is no limit to the number of items you can count, unless you approach 264 items.

######example
```
redis 127.0.0.1:6379> PFADD tutorials "redis"
1) (integer) 1
redis 127.0.0.1:6379> PFADD tutorials "mongodb"
1) (integer) 1
redis 127.0.0.1:6379> PFADD tutorials "mysql"
1) (integer) 1
redis 127.0.0.1:6379> PFCOUNT tutorials
(integer) 3
```

####Related Commands

* **PFADD** key element [element ...]

> Adds the specified elements to the specified HyperLogLog.

> Redis PFADD command adds all the element arguments to the HyperLogLog data structure stored at the key name specified as first argument.

> Return value: Integer reply, 1 or 0.

> ```
redis 127.0.0.1:6379> PFADD mykey a b c d e f g h i j
(integer) 1
redis 127.0.0.1:6379> PFCOUNT mykey
(integer) 10
> ```

* **PFCOUNT** key [key ...]

> Return the approximated cardinality of the set(s) observed by the HyperLogLog at key(s).

> Redis PFCOUNT command is used to get the approximated cardinality computed by the HyperLogLog data structure stored at the specified variable. If key does not exist, then it returns 0.

> ```
redis 127.0.0.1:6379> PFADD mykey a b c d e f g h i j
(integer) 1
redis 127.0.0.1:6379> PFCOUNT mykey
(integer) 10
redis 127.0.0.1:6379> PFCOUNT mykey
(integer) 10
redis 127.0.0.1:6379> PFCOUNT mykey mynewkey
(integer) 10
> ```

* **PFMERGE** destkey sourcekey [sourcekey ...]

> Merge N different HyperLogLogs into a single one.

> Redis PFMERGE command is used to merge multiple HyperLogLog values into an unique value that will approximate the cardinality of the union of the observed Sets of the source HyperLogLog structures.

> ```
redis 127.0.0.1:6379> PFADD hll1 foo bar zap a
(integer) 1
redis 127.0.0.1:6379> PFADD hll2 a b c foo
(integer) 1
redis 127.0.0.1:6379> PFMERGE hll3 hll1 hll2
OK
redis 127.0.0.1:6379> PFCOUNT hll3
(integer) 6
> ```