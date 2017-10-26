## Syntax
Memcached gets command is used to get the value with CAS token. No value is returned if the key does not exist.

The basic syntax of Memcached gets command is as shown below
```
get key

gets key1 key2 key3
```

## Example
In the following example, we use tutorialspoint as the key and store memcached in it with an expiration time of 900 seconds.

```
set tutorialspoint 0 900 9
memcached
STORED
gets tutorialspoint
VALUE tutorialspoint 0 9 1
memcached
END
```
In the output of gets command, we see 1 at the end. This 1 is unique CAS token associated with key tutorialspoint.