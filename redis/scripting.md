#### Syntax
Redis scripting is used to evaluate scripts using the Lua interpreter. It is built into Redis starting from version 2.6.0. Command used for scripting is EVAL command.

Basic syntax of EVAL command is as follows:

```
redis 127.0.0.1:6379> EVAL script numkeys key [key ...] arg [arg ...]
```

###### example
```
redis 127.0.0.1:6379> EVAL "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
```

#### Related Commands
* **EVAL** script numkeys key [key ...] arg [arg ...]

> Redis EVAL command is used to evaluate scripts using the Lua interpreter. The first argument of EVAL is a Lua 5.1 script. The script does not need to define a Lua function (and should not). It is just a Lua program that will run in the context of the Redis server. The second argument of EVAL is the number of arguments that follows the script (starting from the third argument) that represent Redis key names. This arguments can be accessed by Lua using the KEYS global variable in the form of a one-based array (so KEYS[1], KEYS[2], ...). All the additional arguments should not represent key names and can be accessed by Lua using the ARGV global variable, very similarly to what happens with keys (so ARGV[1], ARGV[2], ...).

> ```
redis 127.0.0.1:6379> eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
> ```

* **EVALSHA** sha1 numkeys key [key ...] arg [arg ...]

> Redis EVALSHA command evaluates a script cached on the server side by its SHA1 digest. Scripts are cached on the server side using the SCRIPT LOAD command. The command is otherwise identical to EVAL.

> ```
redis 127.0.0.1:6379> EVALSHA "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
> ```

* **SCRIPT EXISTS** script [script ...]

> Check existence of scripts in the script cache.

> Redis SCRIPT EXISTS command returns information about the existence of the scripts in the script cache. This command accepts one or more SHA1 digests and returns a list of ones or zeros to signal if the scripts are already defined or not inside the script cache. This can be useful before a pipelining operation to ensure that scripts are loaded (and if not, to load them using SCRIPT LOAD) so that the pipelining operation can be performed solely using EVALSHA instead of EVAL to save bandwidth.

> Return value: Array reply The command returns an array of integers that correspond to the specified SHA1 digest arguments. For every corresponding SHA1 digest of a script that actually exists in the script cache, an 1 is returned, otherwise 0 is returned.

> ```
redis 127.0.0.1:6379> SCRIPT LOAD "return 1"
ERR Unknown or disabled command 'SCRIPT'
redis 127.0.0.1:6379> SCRIPT EXISTS ff9d4800c877a703b823dsdsfsffewfwefwefweac0578ff8db
ERR Unknown or disabled command 'SCRIPT'
> ```

* **SCRIPT FLUSH**

> Remove all the scripts from the script cache.

> ```
redis 127.0.0.1:6379> SCRIPT FLUSH
OK
> ```

* **SCRIPT KILL**

> Kill the script currently in execution.

> Redis SCRIPT KILL command kills the currently executing Lua script, assuming no write operation was yet performed by the script. This command is mainly useful to kill a script that is running for too much time(for instance because it entered an infinite loop because of a bug). The script will be killed and the client currently blocked into EVAL will see the command returning with an error. If the script already performed write operations it can not be killed in this way because it would violate Lua script atomicity contract. In such a case only SHUTDOWN NOSAVE is able to kill the script, killing the Redis process in an hard way preventing it to persist with half-written information.

> ```
redis 127.0.0.1:6379> SCRIPT KILL
OK
> ```

* **SCRIPT LOAD** script

> Load the specified Lua script into the script cache.

> Redis SCRIPT LOAD command load a script into the scripts cache, without executing it. After the specified command is loaded into the script cache it will be callable using EVALSHA with the correct SHA1 digest of the script, exactly like after the first successful invocation of EVAL. The script is guaranteed to stay in the script cache forever (unless SCRIPT FLUSH is called). The command works in the same way even if the script was already present in the script cache.

> Return Value: Bulk string reply This command returns the SHA1 digest of the script added into the script cache.

> ```
redis 127.0.0.1:6379> SCRIPT LOAD "return 1"
"e0e1f9fabfc9d4800c877a703b823ac0578ff8db"
> ```