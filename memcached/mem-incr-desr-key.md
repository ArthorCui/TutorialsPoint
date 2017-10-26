## Syntax
Memcached incr and decr commands are used to increment or decrement the numeric value of an existing key. 
If the key is not found, then it returns NOT_FOUND. If the key is not numeric, then it returns CLIENT_ERROR cannot increment or decrement non-numeric value. Otherwise, ERROR is returned.

The basic syntax of Memcached delete command is as shown below
```
incr key increment_value
```

incr command may produce one of the following result −

* NOT_FOUND indicates that the key does not exist.

* CLIENT_ERROR indicates that value is not numeraical.

* ERROR indicates any other error such as syntax error.

## Example
In this example, we use visitors as key and set 10 initially into it, there after we increment the visitors by 5.

```
set visitors 0 900 2
10
STORED
get visitors
VALUE visitors 0 2
10
END
incr visitors 5
15
get visitors
VALUE visitors 0 2
15
END
```

decr is contrary to incr.