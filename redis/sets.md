####Syntax
Redis Sets are an unordered collection of unique Strings. Unique means sets doesn't allow repition of data in a key.

In redis set add, remove, and test for existence of members in O(1) (constant time regardless of the number of elements contained inside the Set). Maximum length of a list is 232 - 1 elements (4294967295, more than 4 billion of elements per set).

######example
```
redis 127.0.0.1:6379> SADD tutorials redis
(integer) 1
redis 127.0.0.1:6379> SADD tutorials mongodb
(integer) 1
redis 127.0.0.1:6379> SADD tutorials mysql
(integer) 1
redis 127.0.0.1:6379> SADD tutorials mysql
(integer) 0
redis 127.0.0.1:6379> SMEMBERS tutorials

1) "mysql"
2) "mongodb"
3) "redis"
```

####Related Commands

* **SADD** key member1 [member2]

> Add one or more members to a set

> Redis SADD command is used to add members to set stored at key. If the member already exists, then it it ignored. If key does not exist, then a new set is created and members are added into it. If the value stored at key if not set, then an error is returned.

> see the [example](#example)

* **SCARD** key

> Get the number of members in a set

> Redis SCARD command is used to number of elements stored in set.

> ```
redis 127.0.0.1:6379> SADD myset "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset "foo"
(integer) 1
redis 127.0.0.1:6379> SADD myset "hello"
(integer) 0
redis 127.0.0.1:6379> SCARD myset
(integer) 2
> ```

* **SDIFF** key1 [key2]

> Subtract multiple sets

> Redis SDIFF command returns the members of the set resulting from the difference between the first set and all the successive sets. If keys does not exists in redis then it it considered as empty sets.

> ```
redis 127.0.0.1:6379> SADD myset "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset "foo"
(integer) 1
redis 127.0.0.1:6379> SADD myset "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "world"
(integer) 1
redis 127.0.0.1:6379> SDIFF myset myset2
1) "foo"
2) "bar"
> ```

* **SDIFFSTORE** destination key1 [key2]

> Subtract multiple sets and store the resulting set in a key

> Redis SDIFFSTORE command store the members of the set, resulting from the difference between the first set and all the successive sets, into a set set specified in command. If destination already exists, it is overwritten.

> ```
redis 127.0.0.1:6379> SADD myset "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset "foo"
(integer) 1
redis 127.0.0.1:6379> SADD myset "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "world"
(integer) 1
redis 127.0.0.1:6379> SDIFFSTORE destset myset myset2
(integer) 2
redis 127.0.0.1:6379> SMEMBERS destset
1) "foo"
2) "bar"
> ```

* **SINTER** key1 [key2]

> Intersect multiple sets

> Redis SINTER command get elements of a set after intersection of all specified sets. Keys that do not exist are considered to be empty sets. With one of the keys being an empty set, the resulting set is also empty (since set intersection with an empty set always results in an empty set).

> ```
redis 127.0.0.1:6379> SADD myset "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset "foo"
(integer) 1
redis 127.0.0.1:6379> SADD myset "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "world"
(integer) 1
redis 127.0.0.1:6379> SINTER myset myset2
1) "hello"
> ```

* **SINTERSTORE** destination key1 [key2]

> Intersect multiple sets and store the resulting set in a key

> Redis SINTERSTORE command store the elements in a set after intersection of all specified sets. Keys that do not exist are considered to be empty sets. With one of the keys being an empty set, the resulting set is also empty (since set intersection with an empty set always results in an empty set).

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "foo"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "world"
(integer) 1
redis 127.0.0.1:6379> SINTERSTORE myset myset1 myset2
(integer) 1
redis 127.0.0.1:6379> SMEMBERS myset
1) "hello"
> ```

* **SISMEMBER** key member

> Determine if a given value is a member of a set

> Redis SISMEMBER returns, element is already exist in set stored at key key or not.

> > 1 if the element is a member of the set.

> > 0 if the element is not a member of the set, or if key does not exist.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SISMEMBER myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SISMEMBER myset1 "world"
(integer) 0
> ```

* **SMEMBERS** key

> Get all the members in a set

> > 1 if the element is a member of the set.

> > 0 if the element is not a member of the set, or if key does not exist.

> see the [example](#example)

* **SMOVE** source destination member

> Move a member from one set to another

> Redis SMOVE command is used to move an element of a set from one key to another key. If the source set does not exist or does not contain the specified element, no operation is performed and 0 is returned. Otherwise, the element is removed from the source set and added to the destination set. When the specified element already exists in the destination set, it is only removed from the source set. An error is returned if source or destination does not hold a set value.

> > 1 if the element is moved.

> > 0 if the element is not a member of source and no operation was performed.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "foo"
(integer) 1
redis 127.0.0.1:6379> SMOVE myset1 myset2 "bar"
(integer) 1
redis 127.0.0.1:6379> SMEMBERS myset1
1) "World"
2) "Hello"
redis 127.0.0.1:6379> SMEMBERS myset2
1) "foo"
2) "bar"
> ```

* **SPOP** key

> Remove and return a random member from a set

> Redis SPOP command is used to remove and return a random member from set stored at specified key.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SPOP myset1
"bar"
redis 127.0.0.1:6379> SMEMBERS myset1
1) "Hello"
2) "world"
> ```

* **SRANDMEMBER** key [count]

> Get one or multiple random members from a set

> Redis SRANDMEMBER command is used to get a random member from set stored at specified key. If called with the additional count argument, return an array of count distinct elements if count is positive. If called with a negative count the behavior changes and the command is allowed to return the same element multiple times. In this case the numer of returned elements is the absolute value of the specified count.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SRANDMEMBER myset1
"bar"
redis 127.0.0.1:6379> SRANDMEMBER myset1 2
1) "Hello"
2) "world"
> ```

* **SREM** key member1 [member2]

> Remove one or more members from a set

> Redis SREM command is used to remove the specified member from the set stored at key. If member does not exist, then command returns just 0. If stored value at key is not set, then an error is returned.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SREM myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SREM myset1 "foo"
(integer) 0
redis 127.0.0.1:6379> SMEMBERS myset1
1) "bar"
2) "world"
> ```

* **SUNION** key1 [key2]

> Add multiple sets

> Redis SUNION command is used to get the members of the set resulting from the union of all the given sets. Keys that do not exist are considered to be empty sets.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "bar"
(integer) 1
redis 127.0.0.1:6379> SUNION myset1 myset2
1) "bar"
2) "world"
3) "hello"
4) "foo"
> ```

* **SUNIONSTORE** destination key1 [key2]

> Add multiple sets and store the resulting set in a key

> Redis SUNIONSTORE command is used to store, the members of the set resulting from the union of all the given sets. Keys that do not exist are considered to be empty sets.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "world"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset2 "bar"
(integer) 1
redis 127.0.0.1:6379> SUNIONSTORE myset myset1 myset2
(integer) 1
redis 127.0.0.1:6379> SMEMBERS myset
1) "bar"
2) "world"
3) "hello"
4) "foo"
> ```

* **SSCAN**	key cursor [MATCH pattern] [COUNT count]

> Incrementally iterate Set elements

> Redis SSCAN command iterates elements of a set stored at specified key.

> ```
redis 127.0.0.1:6379> SADD myset1 "hello"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "hi"
(integer) 1
redis 127.0.0.1:6379> SADD myset1 "bar"
(integer) 1
redis 127.0.0.1:6379> sscan myset1 0 match h*
1) "0"
2) 1) "hello"
   2) "h1"
> ```
