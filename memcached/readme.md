##Installing

For example in ubuntu
```
$sudo apt-get update
$sudo apt-get install memcached
```

To run Memcached server on a different port, run the command given below:
```
$memcached -p 11111 -U 11111 -u user -d
```
It should start the server and listen on TCP port 11111 and UDP port 11111 as a daemon process.

This command is explained below:
* -p is for TCP port number
* -U is for UDP port number
* -u is for user name
* -d runs memcached as daemon process

####Storage Commands

* [Set Data](mem-set-data.md)
* [Add Data](mem-add-data.md)
* [Replace Data](mem-replace-data.md)
* [Append Data](mem-append-data.md)
* [Prepend Data](mem-prepend-data.md)

####Retrieval Commands

* [Get Data](mem-get-data.md)
* [Get CAS Data](mem-get-cas-data.md)
* [Delete Key](mem-delete-key.md)
* [Incr/Decr Key](mem-incr-desr-key.md)

####Statistics Commands

* [Stats](mem-stats.md)
* [Stats Items](mem-stats.md#Items)
* [Stats Slabs](mem-stats.md#Slabs)
* [Stats sizes](mem-stats.md#Sizes)
* [Clear Data](mem-stats.md#Clear)