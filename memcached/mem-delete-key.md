## Syntax
Memcached delete command is used to delete an existing key from the Memcached server.

The basic syntax of Memcached delete command is as shown below
```
delete key [noreply]
```

CAS command may produce one of the following result:

* DELETED indicates successful deletion.

* ERROR indicates error while deleting data or wrong syntax.

* NOT_FOUND indicates that the key does not exist in the Memcached server.

## Example
In this example, we use tutorialspoint as a key and store memcached in it with an expiration time of 900 seconds. After this, it deletes the stored key.

```
set tutorialspoint 0 900 9
memcached
STORED
get tutorialspoint
VALUE tutorialspoint 0 9
memcached
END
delete tutorialspoint
DELETED
get tutorialspoint
END
delete tutorialspoint
NOT_FOUND
```