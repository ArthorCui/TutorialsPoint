##Syntax
The basic syntax of Memcached set command is as shown below
```
set key flags exptime bytes [noreply] 
value
```

The keywords in the syntax are as described below −

* key - It is the name of the unique key by which data is accessed.

* flags - It is the 32-bit unsigned integer that the server stores with the data provided by the user, and returns along with the data when the item is retrieved.

* exptime - It is the expiration time (seconds) of data stored in cache. A 0 value means "never expire", i.e. it should not be removed from the cache unless required. If the exptime is more than 30 days then Memcached interprets it as UNIX timestamp for expiration.

* bytes - This is the length of the data in bytes that needs to be stored in Memcached.

* noreply (optional) - This parameter informs the server not to send any reply.

* value - It is the data that needs to be stored. The data needs to be given on the new line after executing the command with the above options.

##Example
```
set tutorialspoint 0 900 9
memcached
STORED

get tutorialspoint
VALUE tutorialspoint 0 9
memcached

END
```