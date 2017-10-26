## Syntax
Memcached get command is used to get the value stored at key. No value is returned if the key does not exist.

The basic syntax of Memcached get command is as shown below
```
get key

get key1 key2 key3
```

## Example
In the following example, we use tutorialspoint as the key and store memcached in it with an expiration time of 900 seconds.

```
set tutorialspoint 0 900 9
memcached
STORED
get tutorialspoint
VALUE tutorialspoint 0 9
memcached
END
```