## Syntax
Memcached append command is used to add data in an existing key. This data is added at the end of the previous value.

The basic syntax of Memcached append command is as shown below
```
append key flags exptime bytes [noreply]
value
```

The keywords in the syntax are as described below −

* key - It is the name of the unique key by which data is accessed.

* flags - It is the 32-bit unsigned integer that the server stores with the data provided by the user, and returns along with the data when the item is retrieved.

* exptime - It is the expiration time (seconds) of data stored in cache. A 0 value means "never expire", i.e. it should not be removed from the cache unless required. If the exptime is more than 30 days then Memcached interprets it as UNIX timestamp for expiration.

* bytes - This is the length of the data in bytes that needs to be stored in Memcached.

* noreply (optional) - This parameter informs the server not to send any reply.

* value - It is the data that needs to be stored. The data needs to be given on the new line after executing the command with the above options.

## Example
```
set tutorials 0 900 9
memcached
STORED
get tutorials
VALUE tutorials 0 14
memcached
END
append tutorials 0 900 5
redis
STORED
get tutorials
VALUE tutorials 0 14
memcachedredis
END
```