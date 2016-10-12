##Stats
###Syntax
Memcached stats command is used to return server statistics such as PID, version, connections, etc.

The basic syntax of Memcached stats command is as shown below
```
stats
```

###Example
```
stats
STAT pid 1162
STAT uptime 5022
STAT time 1415208270
STAT version 1.4.14
STAT libevent 2.0.19-stable
STAT pointer_size 64
STAT rusage_user 0.096006
STAT rusage_system 0.152009
STAT curr_connections 5
STAT total_connections 6
STAT connection_structures 6
STAT reserved_fds 20
STAT cmd_get 6
STAT cmd_set 4
STAT cmd_flush 0
STAT cmd_touch 0
STAT get_hits 4
STAT get_misses 2
STAT delete_misses 1
STAT delete_hits 1
STAT incr_misses 2
STAT incr_hits 1
STAT decr_misses 0
STAT decr_hits 1
STAT cas_misses 0
STAT cas_hits 0
STAT cas_badval 0
STAT touch_hits 0
STAT touch_misses 0
STAT auth_cmds 0
STAT auth_errors 0
STAT bytes_read 262
STAT bytes_written 313
STAT limit_maxbytes 67108864
STAT accepting_conns 1
STAT listen_disabled_num 0
STAT threads 4
STAT conn_yields 0
STAT hash_power_level 16
STAT hash_bytes 524288
STAT hash_is_expanding 0
STAT expired_unfetched 1
STAT evicted_unfetched 0
STAT bytes 142
STAT curr_items 2
STAT total_items 6
STAT evictions 0
STAT reclaimed 1
END
```

##Items
###Syntax
Memcached stats items command is used to get items statistics such as count, age, eviction, etc. organized by slabs ID.

The basic syntax of Memcached stats items command is as shown below
```
stats items
```

###Example
```
stats items
STAT items:1:number 1
STAT items:1:age 7
STAT items:1:evicted 0
STAT items:1:evicted_nonzero 0
STAT items:1:evicted_time 0
STAT items:1:outofmemory 0
STAT items:1:tailrepairs 0
STAT items:1:reclaimed 0
STAT items:1:expired_unfetched 0
STAT items:1:evicted_unfetched 0
END
```

##Slabs
###Syntax
Memcached stats slabs command displays slabs statistics such as size, memory usage, commands, count etc. organized by slabs ID.
The basic syntax of Memcached stats slabs command is as shown below
```
stats slabs
```

###Example
```
stats slabs
STAT 1:chunk_size 96
STAT 1:chunks_per_page 10922
STAT 1:total_pages 1
STAT 1:total_chunks 10922
STAT 1:used_chunks 1
STAT 1:free_chunks 10921
STAT 1:free_chunks_end 0
STAT 1:mem_requested 71
STAT 1:get_hits 0
STAT 1:cmd_set 1
STAT 1:delete_hits 0
STAT 1:incr_hits 0
STAT 1:decr_hits 0
STAT 1:cas_hits 0
STAT 1:cas_badval 0
STAT 1:touch_hits 0
STAT active_slabs 1
STAT total_malloced 1048512
END
```

##Sizes
###Syntax
Memcached stats sizes command provides information about the sizes and number of items of each size within the cache. The information is returned in two columns. The first column is the size of the item (rounded up to the nearest 32 byte boundary) and the second column is the count of the number of items of that size within the cache.
The basic syntax of Memcached stats sizes command is as shown below
```
stats sizes
```

###Example
```
stats sizes
STAT 96 1
END
```
The item size statistics are useful only to determine the sizes of the objects you are storing. Since the actual memory allocation is relevant only in terms of the chunk size and page size, the information is only useful during a careful debugging or diagnostic session.

##Clear
###Syntax
Memcached flush_all command is used to delete all data (key-value pairs) from the Memcached server. It accepts an optional parameter called time, that sets a time after which the Memcached data is to be cleared.
The basic syntax of Memcached flush_all command is as shown below 
```
flush_all [time] [noreply]
```

###Example
```
set tutorialspoint 0 900 9
memcached
STORED
get tutorialspoint
VALUE tutorialspoint 0 9
memcached
END
flush_all
OK
get tutorialspoint
END
```
