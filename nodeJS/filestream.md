##File System

Node implements File I/O using simple wrappers around standard POSIX functions.
The Node File System (fs) module can be imported using the following syntax:

```
var fs = require("fs")
```

###Synchronous & Asynchronous
Every method in the fs module has synchronous as well as asynchronous forms. Asynchronous methods take the last parameter as the completion function callback and the first parameter of the callback function as error. It is better to use an asynchronous method instead of a synchronous method, as the former never blocks a program during its execution, whereas the second one does.

```
var fs = require("fs");

// Asynchronous read
fs.readFile('input.txt', function (err, data) {
   if (err) {
      return console.error(err);
   }
   console.log("Asynchronous read: " + data.toString());
});

// Synchronous read
var data = fs.readFileSync('input.txt');
console.log("Synchronous read: " + data.toString());

console.log("Program Ended");
```

###File and Directory Operations

* **[Open File](#open-file)**
* **[Get File Information](#get-file-info)**
* **[Write File](#write-file)**
* **[Read File](#read-file)**
* **[Close File](#close-file)**
* **[Truncate File](#truncate-file)**
* **[Delete File](#delete-file)**
* **[Create Directory](#create-dir)**
* **[Read Directory](#read-dir)**
* **[Remove Directory](#remove-dir)**

