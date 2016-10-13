####Syntax
Redis Lists are simply lists of strings, sorted by insertion order. You can add elements in redis lists in head or tail of list.

Maximum length of a list is 232 - 1 elements (4294967295, more than 4 billion of elements per list).

######example
```
redis 127.0.0.1:6379> LPUSH tutorials redis
(integer) 1
redis 127.0.0.1:6379> LPUSH tutorials mongodb
(integer) 2
redis 127.0.0.1:6379> LPUSH tutorials mysql
(integer) 3
redis 127.0.0.1:6379> LRANGE tutorials 0 10

1) "mysql"
2) "mongodb"
3) "redis"
```

####Related Commands

* **RPUSH** key value1 [value2]

> Append one or multiple values to a list

> Redis RPUSH command insert all the specified values at the tail of the list stored at key. If key does not exist, it is created as empty list before performing the push operation. When key holds a value that is not a list, an error is returned.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "bar"
(integer) 3
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "foo"
3) "bar"
> ```

* **RPUSHX** key value

> Append a value to a list, only if the list exists

> Redis RPUSHX command inserts value at the tail of the list stored at key, only if key already exists and holds a list. In contrary to RPUSH, no operation will be performed when key does not yet exist.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 2
redis 127.0.0.1:6379> RPUSHX mylist2 "bar"
(integer) 0
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "foo"
> ```

* **LPUSH** key value1 [value2]

> Prepend one or multiple values to a list

> Redis LPUSH command insert all the specified values at the head of the list stored at key. If key does not exist, it is created as empty list before performing the push operations. When key holds a value that is not a list, an error is returned.

> see [example](#example)

* **LPUSHX** key value

> Prepend a value to a list, only if the list exists

> Redis LPUSHX command inserts value at the head of the list stored at key, only if key already exists and holds a list.
> ```
redis 127.0.0.1:6379> LPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> LPUSHX list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LPUSHX list2 "bar"
(integer) 0
redis 127.0.0.1:6379> LRANGE list1 0 -1
1) "foo"
2) "bar"
> ```

* **LRANGE ** key start stop

> Get a range of elements from a list

> Redis LRANGE command returns the specified elements of the list stored at key. The offsets start and stop are zero-based indexes, with 0 being the first element of the list (the head of the list), 1 being the next element and so on. These offsets can also be negative numbers indicating offsets starting at the end of the list. For example, -1 is the last element of the list, -2 the penultimate, and so on.
> ```
redis 127.0.0.1:6379> LPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> LPUSH list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LPUSHX list1 "bar"
(integer) 0
redis 127.0.0.1:6379> LRANGE list1 0 -1
1) "foo"
2) "bar"
3) "bar"
> ```

* **LREM ** key count value

> Remove elements from a list

> Redis LREM command removes the first count occurrences of elements equal to value from the list stored at key. The count argument influences the operation in the following ways:

> > count > 0: Remove elements equal to value moving from head to tail.

> > count < 0: Remove elements equal to value moving from tail to head.

> > count = 0: Remove all elements equal to value.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 3
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 4
redis 127.0.0.1:6379> LREM mylist -2 "hello"
(integer) 2
> ```

* **LSET ** key index value

> Set the value of an element in a list by its index

> Redis LSET command sets the list element at index to value. For more information on the index argument, see LINDEX. An error is returned for out of range indexes.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 3
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 4
redis 127.0.0.1:6379> LSET mylist 0 "bar"
OK
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1: "bar"
2) "hello"
3) "foo"
4) "hello"
> ```

* **LLEN ** key

> Get the length of a list

> Redis LLEN command returns the length of the list stored at key. If key does not exist, it is interpreted as an empty list and 0 is returned. An error is returned when the value stored at key is not a list.
> ```
redis 127.0.0.1:6379> RPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> RPUSH list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LLEN list1
(integer) 2
> ```

* **LPOP ** key

> Remove and get the first element in a list

> Redis LPOP command removes and returns the first element of the list stored at key.
> ```
redis 127.0.0.1:6379> RPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> RPUSH list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LPOP list1
"foo"
> ```

* **RPOP ** key

> Remove and get the last element in a list

> Redis RPOP command removes and returns the last element of the list stored at key.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 3
redis 127.0.0.1:6379> RPUSH mylist "bar"
(integer) 4
redis 127.0.0.1:6379> RPOP mylist
OK
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "hello"
3) "foo"
> ```

* **LINDEX ** key index

> Get an element from a list by its index

> Redis LINDEX command is used to get the element at index index in the list stored at key. The index is zero-based, so 0 means the first element, 1 the second element and so on. Negative indices can be used to designate elements starting at the tail of the list. Here, -1 means the last element, -2 means the penultimate and so forth.
> ```
redis 127.0.0.1:6379> LPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> LPUSH list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LINDEX list1 0
"foo"
redis 127.0.0.1:6379> LINDEX list1 -1
"bar"
redis 127.0.0.1:6379> LINDEX list1 5
nil
> ```

* **LINSERT ** key BEFORE|AFTER pivot value

> Insert an element before or after another element in a list

> Redis LINSERT command inserts value in the list stored at key either before or after the reference value pivot. When key does not exist, it is considered an empty list and no operation is performed. An error is returned when key exists but does not hold a list value.
> ```
redis 127.0.0.1:6379> RPUSH list1 "foo"
(integer) 1
redis 127.0.0.1:6379> RPUSH list1 "bar"
(integer) 2
redis 127.0.0.1:6379> LINSERT list1 BEFORE "bar" "Yes"
(integer) 3
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "foo"
2) "Yes"
3) "bar"
> ```

* **LTRIM ** key start stop

> Trim a list to the specified range

> Redis LTRIM command trim an existing list so that it will contain only the specified range of elements specified. Both start and stop are zero-based indexes, where 0 is the first element of the list (the head), 1 the next element and so on.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 3
redis 127.0.0.1:6379> RPUSH mylist "bar"
(integer) 4
redis 127.0.0.1:6379> LTRIM mylist 1 -1
OK
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "foo"
3) "bar"
> ```

* **RPOPLPUSH ** source destination

> Remove the last element in a list, append it to another list and return it

> Redis RPOPLPUSH command returns and removes the last element (tail) of the list stored at source, and pushes the element at the first element (head) of the list stored at destination.
> ```
redis 127.0.0.1:6379> RPUSH mylist "hello"
(integer) 1
redis 127.0.0.1:6379> RPUSH mylist "foo"
(integer) 2
redis 127.0.0.1:6379> RPUSH mylist "bar"
(integer) 3
redis 127.0.0.1:6379> RPOPLPUSH mylist myotherlist
"bar"
redis 127.0.0.1:6379> LRANGE mylist 0 -1
1) "hello"
2) "foo"
> ```

* **BLPOP ** key1 [key2 ] timeout

> Remove and get the first element in a list, or block until one is available

> Redis BLPOP command is used to remove and get the first element in a list, or block until one is available. BLPOP command just return the first element, if available, or block the client for specific time to execute any command.
> ```
redis 127.0.0.1:6379> BLPOP list1 100
> ```

> Above example will block the client for 100 seconds to execute any command. If any data comes in the specified key list1 then it returns otherwise after 100 seconds nil value is returned.

* **BRPOP ** key1 [key2 ] timeout

> Remove and get the last element in a list, or block until one is available

> Redis BRPOP command is used to remove and get the last element in a list, or block until one is available. BRPOP command just return the last element, if available, or block the client for specific time to execute any command.
> ```
redis 127.0.0.1:6379> BRPOP list1 100
> ```

> Above example will block the client for 100 seconds to execute any command. If any data comes in the specified key list1 then it returns otherwise after 100 seconds nil value is returned.

* **BRPOPLPUSH ** source destination timeout

> Pop a value from a list, push it to another list and return it; or block until one is available

> Redis BRPOPLPUSH command is used to pop a value from a list, push it to another list and return it, or block until one is available. BRPOPLPUSH command just return the last element and insert in to another list, if available, or block the client for specific time to execute any command.
> ```
redis 127.0.0.1:6379> BRPOPLPUSH list1 list2 100
> ```

> Above example will block the client for 100 seconds to execute any command. If any data comes in the specified key list1 then it will pop data and push it into another list otherwise after 100 seconds nil value is returned.