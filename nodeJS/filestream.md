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

####Open-File

#####Syntax

Following is the syntax of the method to open a file in asynchronous mode:
```
fs.open(path, flags[, mode], callback)
```
see the example [here](#openfile-example)

#####Parameters

* **path** − This is the string having file name including path.
* **[flags](#flags)** − Flags indicate the behavior of the file to be opened. All possible values have been mentioned below.
* **mode** − It sets the file mode (permission and sticky bits), but only if the file was created. It defaults to 0666, readable and writeable.
* **callback** − This is the callback function which gets two arguments (err, fd).

######Flags
* `r`	Open file for reading. An exception occurs if the file does not exist.
* `r+`	Open file for reading and writing. An exception occurs if the file does not exist.
* `rs`	Open file for reading in synchronous mode.
* `rs+`	Open file for reading and writing, asking the OS to open it synchronously. See notes for 'rs' about using this with caution.
* `w`	Open file for writing. The file is created (if it does not exist) or truncated (if it exists).
* `wx`	Like 'w' but fails if the path exists.
* `w+`	Open file for reading and writing. The file is created (if it does not exist) or truncated (if it exists).
* `wx+`	Like 'w+' but fails if path exists.
* `a`	Open file for appending. The file is created if it does not exist.
* `ax`	Like 'a' but fails if the path exists.
* `a+`	Open file for reading and appending. The file is created if it does not exist.
* `ax+`	Like 'a+' but fails if the the path exists.

#####OpenFile-Example
```
var fs = require("fs");

// Asynchronous - Opening File
console.log("Going to open file!");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
      return console.error(err);
   }
  console.log("File opened successfully!");     
});
```

####Get-File-Info

#####Syntax

```
fs.stat(path, callback)
```
see the example [here](#getfile-example)

#####Parameters

* **path** − This is the string having file name including path.
* **callback** − This is the callback function which gets two arguments (err, stats) where `stats` is an object of `fs.Stats` type which is printed below in the example.

######stat method
`stats.isFile()`			Returns true if file type of a simple file.
`stats.isDirectory()`		Returns true if file type of a directory.
`stats.isBlockDevice()`		Returns true if file type of a block device.
`stats.isCharacterDevice()`	Returns true if file type of a character device.
`stats.isSymbolicLink()`	Returns true if file type of a symbolic link.
`stats.isFIFO()`			Returns true if file type of a FIFO.
`stats.isSocket()`			Returns true if file type of asocket.

#####GetFile-Example
```
var fs = require("fs");

console.log("Going to get file info!");
fs.stat('input.txt', function (err, stats) {
   if (err) {
       return console.error(err);
   }
   console.log(stats);
   console.log("Got file info successfully!");
   
   // Check file type
   console.log("isFile ? " + stats.isFile());
   console.log("isDirectory ? " + stats.isDirectory());    
});
```

####Write-File

#####Syntax

```
fs.writeFile(filename, data[, options], callback)
```
see the example [here](#writefile-example)

#####Parameters

* **path** − This is the string having the file name including path.
* **data** − This is the String or Buffer to be written into the file.
* **options** − The third parameter is an object which will hold {encoding, mode, flag}. By default. encoding is utf8, mode is octal value 0666. and flag is 'w'
* **callback** − This is the callback function which gets a single parameter err that returns an error in case of any writing error.

#####WriteFile-Example
```
var fs = require("fs");

console.log("Going to write into existing file");
fs.writeFile('input.txt', 'Simply Easy Learning!',  function(err) {
   if (err) {
      return console.error(err);
   }
   
   console.log("Data written successfully!");
   console.log("Let's read newly written data");
   fs.readFile('input.txt', function (err, data) {
      if (err) {
         return console.error(err);
      }
      console.log("Asynchronous read: " + data.toString());
   });
});
```

####Read-File

#####Syntax

```
fs.read(fd, buffer, offset, length, position, callback)
```
see the example [here](#Readfile-example)

#####Parameters

* **fd** − This is the file descriptor returned by fs.open().
* **buffer** − This is the buffer that the data will be written to.
* **offset** − This is the offset in the buffer to start writing at.
* **length** − This is an integer specifying the number of bytes to read.
* **position** − This is an integer specifying where to begin reading from in the file. If position is null, data will be read from the current file position.
* **callback** − This is the callback function which gets the three arguments, (err, bytesRead, buffer).

#####ReadFile-Example
```
var fs = require("fs");
var buf = new Buffer(1024);

console.log("Going to open an existing file");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
      return console.error(err);
   }
   console.log("File opened successfully!");
   console.log("Going to read the file");
   fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){
      if (err){
         console.log(err);
      }
      console.log(bytes + " bytes read");
      
      // Print only read bytes to avoid junk.
      if(bytes > 0){
         console.log(buf.slice(0, bytes).toString());
      }
   });
});
```

####Close-File

#####Syntax

```
fs.close(fd, callback)
```
see the example [here](#closefile-example)

#####Parameters

* **fd** − This is the file descriptor returned by file fs.open() method.
* **callback** − This is the callback function No arguments other than a possible exception are given to the completion callback.

#####CloseFile-Example
```
var fs = require("fs");
var buf = new Buffer(1024);

console.log("Going to open an existing file");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
      return console.error(err);
   }
   console.log("File opened successfully!");
   console.log("Going to read the file");
   
   fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){
      if (err){
         console.log(err);
      }

      // Print only read bytes to avoid junk.
      if(bytes > 0){
         console.log(buf.slice(0, bytes).toString());
      }

      // Close the opened file.
      fs.close(fd, function(err){
         if (err){
            console.log(err);
         } 
         console.log("File closed successfully.");
      });
   });
});
```

####Truncate-File

#####Syntax

```
fs.ftruncate(fd, len, callback)
```
see the example [here](#truncatefile-example)

#####Parameters

* **fd** − This is the file descriptor returned by fs.open().
* **len** − This is the length of the file after which the file will be truncated.
* **callback** − This is the callback function No arguments other than a possible exception are given to the completion callback.

#####TruncateFile-Example
```
var fs = require("fs");
var buf = new Buffer(1024);

console.log("Going to open an existing file");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
      return console.error(err);
   }
   console.log("File opened successfully!");
   console.log("Going to truncate the file after 10 bytes");
   
   // Truncate the opened file.
   fs.ftruncate(fd, 10, function(err){
      if (err){
         console.log(err);
      } 
      console.log("File truncated successfully.");
      console.log("Going to read the same file"); 
      
      fs.read(fd, buf, 0, buf.length, 0, function(err, bytes){
         if (err){
            console.log(err);
         }

         // Print only read bytes to avoid junk.
         if(bytes > 0){
            console.log(buf.slice(0, bytes).toString());
         }

         // Close the opened file.
         fs.close(fd, function(err){
            if (err){
               console.log(err);
            } 
            console.log("File closed successfully.");
         });
      });
   });
});
```

####Delete-File

#####Syntax

```
fs.unlink(path, callback)
```
see the example [here](#deletefile-example)

#####Parameters

* **path** − This is the file name including path.
* **callback** − This is the callback function No arguments other than a possible exception are given to the completion callback.

#####DeleteFile-Example
```
var fs = require("fs");

console.log("Going to delete an existing file");
fs.unlink('input.txt', function(err) {
   if (err) {
      return console.error(err);
   }
   console.log("File deleted successfully!");
});
```

####Create-Directory

#####Syntax

```
fs.mkdir(path[, mode], callback)
```
see the example [here](#create-directory-example)

#####Parameters

* **path** − This is the directory name including path.
* **mode** − This is the directory permission to be set. Defaults to 0777.
* **callback** − This is the callback function No arguments other than a possible exception are given to the completion callback.

#####Create-Directory-Example
```
var fs = require("fs");

console.log("Going to create directory /tmp/test");
fs.mkdir('/tmp/test',function(err){
   if (err) {
      return console.error(err);
   }
   console.log("Directory created successfully!");
});
```

####Read-Directory

#####Syntax

```
fs.readdir(path, callback)
```
see the example [here](#read-directory-example)

#####Parameters

* **path** − This is the directory name including path.
* **callback** − This is the callback function which gets two arguments (err, files) where files is an array of the names of the files in the directory excluding '.' and '..'.

#####Read-Directory-Example
```
var fs = require("fs");

console.log("Going to read directory /tmp");
fs.readdir("/tmp/",function(err, files){
   if (err) {
      return console.error(err);
   }
   files.forEach( function (file){
      console.log( file );
   });
});
```

####Remove-Directory

#####Syntax

```
fs.rmdir(path, callback)
```
see the example [here](#remove-directory-example)

#####Parameters

* **path** − This is the directory name including path.
* **callback** − This is the callback function No argume nts other than a possible exception are given to the completion callback.

#####Remove-Directory-Example
```
var fs = require("fs");

console.log("Going to delete directory /tmp/test");
fs.rmdir("/tmp/test",function(err){
   if (err) {
      return console.error(err);
   }
   console.log("Going to read directory /tmp");
   
   fs.readdir("/tmp/",function(err, files){
      if (err) {
         return console.error(err);
      }
      files.forEach( function (file){
         console.log( file );
      });
   });
});
```
