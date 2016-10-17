#Lua
Lua is an extensible, light-weight programming language written in C. 

It was designed from the beginning to be a software that can be integrated with the code written in C and other conventional languages. This integration brings many benefits. It does not try to do what C can already do but aims at offering what C is not good at: a good distance from the hardware, dynamic structures, no redundancies, ease of testing and debugging. 
For this, Lua has a safe environment, automatic memory management, and good facilities for handling strings and other kinds of data with dynamic size.

Features:
* Extensible
* Simple
* Efficient
* Portable
* Free and open

##Environment

When we extend Lua to other languages/applications, we need a Software Development Kit with a compiler that is compatible with the Lua Application Program Interface.

> * **Installation on Linux**

```
# the latest version
$ wget http://www.lua.org/ftp/lua-5.3.3.tar.gz
$ tar zxf lua-5.3.3.tar.gz
$ cd lua-5.3.3
$ make linux test

touch helloworld.lua

vi helloworld.lua

#!/usr/local/bin/lua
print("Hello World!")

chmod +x helloworld.lua

$ lua helloWorld
```

##Parts

* **[Data Types](data-types.md)**

* **[Variables](variables.md)**

* **[Operators](operators.md)**

* **[Loops](loops.md)**

