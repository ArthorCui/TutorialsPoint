####Syntax
Redis Sorted Sets are similar to Redis Sets with unique feature of values stored in set. The difference is that every member of a Sorted Set is associated with score, that is used in order to take the sorted set ordered, from the smallest to the greatest score.

In redis sorted set add, remove, and test for existence of members in O(1) (constant time regardless of the number of elements contained inside the Set). Maximum length of a list is 232 - 1 elements (4294967295, more than 4 billion of elements per set).

######example
```
redis 127.0.0.1:6379> ZADD tutorials 1 redis
(integer) 1
redis 127.0.0.1:6379> ZADD tutorials 2 mongodb
(integer) 1
redis 127.0.0.1:6379> ZADD tutorials 3 mysql
(integer) 1
redis 127.0.0.1:6379> ZADD tutorials 3 mysql
(integer) 0
redis 127.0.0.1:6379> ZADD tutorials 4 mysql
(integer) 0
redis 127.0.0.1:6379> ZRANGE tutorials 0 10 WITHSCORES

1) "redis"
2) "1"
3) "mongodb"
4) "2"
5) "mysql"
6) "4"

```

####Related Commands

* **ZCARD** key

> Get the number of members in a sorted set

> see the [example](#example)

* **ZADD** key score1 member1 [score2 member2]

> Add one or more members to a sorted set, or update its score if it already exists

> Redis ZADD command add all the specified members with the specified scores to the sorted set stored at key. It is possible to specify multiple score / member pairs. If a specified member is already a member of the sorted set, the score is updated and the element reinserted at the right position to ensure the correct ordering. If key does not exist, a new sorted set with the specified members as sole members is created, like if the sorted set was empty. If the key exists but does not hold a sorted set, an error is returned.

> ```
redis 127.0.0.1:6379> ZADD myset 1 "hello"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 1 "foo"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 2 "world" 3 "bar"
(integer) 2
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "hello"
2) "1"
3) "foo"
4) "1"
5) "world"
6) "2"
7) "bar"
8) "3"
> ```

* **ZCOUNT** key min max

> Count the members in a sorted set with scores within the given values

> Redis ZCOUNT command returns the number of elements in the sorted set at key with a score between min and max.

> ```
redis 127.0.0.1:6379> ZADD myset 1 "hello"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 1 "foo"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 2 "world" 3 "bar"
(integer) 2
redis 127.0.0.1:6379> ZCOUNT myzset (1 3
(integer) 2
> ```

* **ZINCRBY** key increment member

> Increment the score of a member in a sorted set

> Redis ZINCRBY command increment the score of member in the sorted set stored at key by increment. If member does not exist in the sorted set, it is added with increment as its score (as if its previous score was 0.0). If key does not exist, a new sorted set with the specified member as its sole member is created. An error is returned when key exists but does not hold a sorted set.

> ```
redis 127.0.0.1:6379> ZADD myset 1 "hello"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 1 "foo"
(integer) 1
redis 127.0.0.1:6379> ZINCRBY myzset 2 "hello"
(integer) 3
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "foo"
2) "2"
3) "hello"
4) "3"
> ```

* **ZINTERSTORE** destination numkeys key [key ...]

> Intersect multiple sorted sets and store the resulting sorted set in a new key

> Redis ZINTERSTORE command computes the intersection of numkeys sorted sets given by the specified keys, and stores the result in destination. It is mandatory to provide the number of input keys (numkeys) before passing the input keys and the other (optional) arguments.

> ```
redis 127.0.0.1:6379> ZADD myset 1 "hello"
(integer) 1
redis 127.0.0.1:6379> ZADD myset 2 "world"
(integer) 1
redis 127.0.0.1:6379> ZADD myset2 1 "hello"
(integer) 1
redis 127.0.0.1:6379> ZADD myset2 2 "world"
(integer) 1
redis 127.0.0.1:6379> ZADD myset2 3 "foo"
(integer) 1
redis 127.0.0.1:6379> ZINTERSTORE out 2 myset1 myset2 WEIGHTS 2 3"
(integer) 3
redis 127.0.0.1:6379> ZRANGE out 0 -1 WITHSCORES
1) "hello"
2) "5"
3) "world"
4) "10"
> ```

* **ZLEXCOUNT** key min max

> Count the number of members in a sorted set between a given lexicographical range

> When all the elements in a sorted set are inserted with the same score, in order to force lexicographical ordering, this command returns the number of elements in the sorted set at key with a value between min and max.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 0 b 0 c 0 d 0 e
(integer) 5
redis 127.0.0.1:6379> ZADD myzset 0 f 0 g
(integer) 2
redis 127.0.0.1:6379> ZLEXCOUNT myzset - +
(integer) 7
redis 127.0.0.1:6379> ZLEXCOUNT myzset [b [f
(integer) 5
> ```

* **ZRANGE** key start stop [WITHSCORES]

> Return a range of members in a sorted set, by index

> Redis ZRANGE command returns the specified range of elements in the sorted set stored at key. The elements are considered to be ordered from the lowest to the highest score. Lexicographical order is used for elements with equal score. Both start and stop are zero-based indexes, where 0 is the first element, 1 is the next element and so on. They can also be negative numbers indicating offsets from the end of the sorted set, with -1 being the last element of the sorted set, -2 the penultimate element and so on.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 0 b 0 c 0 d 0 e
(integer) 5
redis 127.0.0.1:6379> ZADD myzset 0 f 0 g
(integer) 2
redis 127.0.0.1:6379> ZRANGE myzset 0 -1
1) "a"
2) "b"
3) "c"
4) "d"
5) "e"
6) "f"
7) "g"
redis 127.0.0.1:6379> ZLEXCOUNT myzset [b [f
(integer) 5
> ```

* **ZRANGEBYLEX** key min max [LIMIT offset count]

> Return a range of members in a sorted set, by lexicographical range

> Redis ZRANGEBYLEX command returns the specified range of elements in the sorted set stored at key. The elements are considered to be ordered from the lowest to the highest score. Lexicographical order is used for elements with equal score. Both start and stop are zero-based indexes, where 0 is the first element, 1 is the next element and so on. They can also be negative numbers indicating offsets from the end of the sorted set, with -1 being the last element of the sorted set, -2 the penultimate element and so on.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 0 b 0 c 0 d 0 e
(integer) 5
redis 127.0.0.1:6379> ZADD myzset 0 f 0 g
(integer) 2
redis 127.0.0.1:6379> ZRANGEBYLEX myzset - [c
1) "a"
2) "b"
3) "c"
redis 127.0.0.1:6379> ZRANGEBYLEX myzset - (c
1) "a"
2) "b"
> ```

* **ZRANGEBYSCORE** key min max [WITHSCORES] [LIMIT]

> Return a range of members in a sorted set, by score

> Redis ZRANGEBYSCORE command returns all the elements in the sorted set at key with a score between min and max (including elements with score equal to min or max). The elements are considered to be ordered from low to high scores. The elements having the same score are returned in lexicographical order (this follows from a property of the sorted set implementation in Redis and does not involve further computation).

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 1 b 2 c 3 d 4 e
(integer) 5
redis 127.0.0.1:6379> ZADD myzset 5 f 6 g
(integer) 2
redis 127.0.0.1:6379> ZRANGEBYSCORE myzset 1 2
1) "b"
2) "c"
redis 127.0.0.1:6379> ZRANGEBYSCORE myzset (1 2
1) "b"
> ```

* **ZRANK**	key member

> Determine the index of a member in a sorted set

> Redis ZRANK command returns the rank of member in the sorted set stored at key, with the scores ordered from low to high. The rank (or index) is 0-based, which means that the member with the lowest score has rank 0.

> > If member exists in the sorted set, Integer reply: the rank of member.

> > If member does not exist in the sorted set or key does not exist, Bulk string reply, nil.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 1 b 2 c 3 d 4 e
(integer) 5
redis 127.0.0.1:6379> ZADD myzset 5 f 6 g
(integer) 2
redis 127.0.0.1:6379> ZRANK myzset b
(integer) 1
redis 127.0.0.1:6379> ZRANK myzset t
nil
> ```

* **ZREM** key member [member ...]

> Remove one or more members from a sorted set

> Redis ZREM command removes the specified members from the sorted set stored at key. Non existing members are ignored. An error is returned when key exists and does not hold a sorted set.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 1 b 2 c 3 d 4 e
(integer) 5
redis 127.0.0.1:6379> ZREM myzset b
(integer) 1
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "a"
2) "0"
3) "c"
4) "2"
5) "d"
6) "3"
7) "e"
8) "4"
> ```

* **ZREMRANGEBYLEX** key min max

> Remove all members in a sorted set between the given lexicographical range

> Redis ZREMRANGEBYLEX command removes all elements in the sorted set stored at key between the lexicographical range specified by min and max.

> ```
redis 127.0.0.1:6379> ZADD myzset 0 a 1 b 2 c 3 d 4 e
(integer) 5
redis 127.0.0.1:6379> ZREMRANGEBYLEX myzset 0 -1
(integer) 1
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
> ```

* **ZREMRANGEBYRANK** key start stop

> Remove all members in a sorted set within the given indexes

> Redis ZREMRANGEBYRANK command removes all elements in the sorted set stored at key with rank between start and stop. Both start and stop are 0 -based indexes with 0 being the element with the lowest score. These indexes can be negative numbers, where they indicate offsets starting at the element with the highest score. For example: -1 is the element with the highest score, -2 the element with the second highest score and so forth.

> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZREMRANGEBYRANK myzset 0 3
(integer) 3
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "e"
2) "4"
> ```

* **ZREMRANGEBYSCORE** key min max

> Remove all members in a sorted set within the given scores

> Redis ZREMRANGEBYSCORE command removes all elements in the sorted set stored at key with a score between min and max (inclusive).

> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZREMRANGEBYSCORE myzset -inf (2
(integer) 1
redis 127.0.0.1:6379> ZRANGE myzset 0 -1 WITHSCORES
1) "b"
2) "2"
3) "c"
4) "3"
5) "d"
6) "4"
7) "e"
8) "5"

> ```

* **ZREVRANGE** key start stop [WITHSCORES]

> Return a range of members in a sorted set, by index, with scores ordered from high to low

> Redis ZREVRANGE command returns the specified range of elements in the sorted set stored at key. The elements are considered to be ordered from the highest to the lowest score. Descending lexicographical order is used for elements with equal score.

> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZREVRANGE myzset 0 -1
1) "e"
2) "d"
3) "c"
4) "b"
> ```

* **ZREVRANGEBYSCORE** key max min [WITHSCORES]

> Return a range of members in a sorted set, by score, with scores ordered from high to low

> Redis ZREVRANGEBYSCORE command returns all the elements in the sorted set at key with a score between max and min (including elements with score equal to max or min). In contrary to the default ordering of sorted sets, for this command the elements are considered to be ordered from high to low scores. The elements having the same score are returned in reverse lexicographical order.

> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZREVRANGEBYSCORE myzset +inf -inf
1) "e"
2) "d"
3) "c"
4) "b"
redis 127.0.0.1:6379> ZREVRANGEBYSCORE myzset 2 1
1) "c"
2) "b"
> ```

* **ZREVRANK** key member

> Determine the index of a member in a sorted set, with scores ordered from high to low

> Redis ZREVRANK command returns the rank of member in the sorted set stored at key, with the scores ordered from high to low. The rank (or index) is 0-based, which means that the member with the highest score has rank 0.

> > If member exists in the sorted set, Integer reply: the rank of member.

> > If member does not exist in the sorted set or key does not exist, Bulk string reply: nil.
> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZREVRANK myzset "c"
(integer) 3
redis 127.0.0.1:6379> ZREVRANK myzset "y"
(nil)
> ```

* **ZSCORE** key member

> Get the score associated with the given member in a sorted set

> Redis ZSCORE command returns the score of member in the sorted set at key. If member does not exist in the sorted set, or key does not exist, nil is returned.

> ```
redis 127.0.0.1:6379> ZADD myzset 1 b 2 c 3 d 4 e
(integer) 4
redis 127.0.0.1:6379> ZSCORE myzset "c"
(integer) 3
redis 127.0.0.1:6379> ZSCORE myzset "y"
(nil)
> ```

* **ZUNIONSTORE** destination numkeys key [key ...]

> Add multiple sorted sets and store the resulting sorted set in a new key

> Redis ZUNIONSTORE command calculates the union of numkeys sorted sets given by the specified keys, and stores the result in destination. It is mandatory to provide the number of input keys (numkeys) before passing the input keys and the other (optional) arguments.

> ```
redis 127.0.0.1:6379> ZADD myzset1 1 b 2 c
(integer) 2
redis 127.0.0.1:6379> ZADD myzset2 1 b 2 c 3 d
(integer) 3
redis 127.0.0.1:6379> ZUNIONSTORE out 2 myzset1 myzset2 WEIGHTS 2 3
(integer) 3
redis 127.0.0.1:6379> ZRANGE out 0 -1 WITHSCORES
1) "b"
2) "5"
3) "c"
4) "9"
5) "d"
6) "10"
> ```

* **ZSCAN** key cursor [MATCH pattern] [COUNT count]

> Incrementally iterate sorted sets elements and associated scores

> Redis ZSCAN command iterates elements of Sorted Set types and their associated scores.

> ```
redis 127.0.0.1:6379> ZSCAN key cursor [MATCH pattern] [COUNT count]
> ```