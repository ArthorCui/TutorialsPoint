##Scaling Application

Node.js runs in a single-thread mode, but it uses an event-driven paradigm to handle concurrency. It also facilitates creation of child processes to leverage parallel processing on multi-core CPU based systems.

Node provides `child_process` module which has the following three major ways to create a child process.

* **exec** − child_process.exec method runs a command in a shell/console and buffers the output.
* **spawn** − child_process.spawn launches a new process with a given command.
* **fork** − The child_process.fork method is a special case of the spawn() to create child processes.

###Exec

`child_process.exec` method runs a command in a shell and buffers the output. It has the following signature −

```
child_process.exec(command[, options], callback)
```

####Parameters

* **command** (String) The command to run, with space-separated arguments
* **options** (Object) may comprise one or more of the following options −

> `cwd` (String) Current working directory of the child process

> `env` (Object) Environment key-value pairs

> `encoding` (String) (Default: 'utf8')

> `shell` (String) Shell to execute the command with (Default: '/bin/sh' on UNIX, 'cmd.exe' on Windows, The shell should understand the -c switch on UNIX or /s /c on Windows. On Windows, command line parsing should be compatible with cmd.exe.)

> `timeout` (Number) (Default: 0)

> `maxBuffer` (Number) (Default: 200*1024)

> `killSignal` (String) (Default: 'SIGTERM')

> `uid` (Number) Sets the user identity of the process.

> `gid` (Number) Sets the group identity of the process.

* **callback** The function gets three arguments `error`, `stdout`, and `stderr` which are called with the output when the process terminates.

####Example

> File: support.js

```
console.log("Child Process " + process.argv[2] + " executed." );
```

> File: master.js

```
const fs = require('fs');
const child_process = require('child_process');

for(var i=0; i<3; i++) {
   var workerProcess = child_process.exec('node support.js '+i,function 
      (error, stdout, stderr) {
      
      if (error) {
         console.log(error.stack);
         console.log('Error code: '+error.code);
         console.log('Signal received: '+error.signal);
      }
      console.log('stdout: ' + stdout);
      console.log('stderr: ' + stderr);
   });

   workerProcess.on('exit', function (code) {
      console.log('Child process exited with exit code '+code);
   });
}
```

run `$ node master.js`

```
Child process exited with exit code 0
stdout: Child Process 1 executed.

stderr:
Child process exited with exit code 0
stdout: Child Process 0 executed.

stderr:
Child process exited with exit code 0
stdout: Child Process 2 executed.
```

###Spawn

`child_process.spawn` method launches a new process with a given command. It has the following signature −

```
child_process.spawn(command[, args][, options])
```

####Parameters

* **command** (String) The command to run
* **args** (Array) List of string arguments
* **options** (Object) may comprise one or more of the following options −

> `cwd` (String) Current working directory of the child process.

> `env` (Object) Environment key-value pairs.

> `stdio` (Array) String Child's stdio configuration.

> `customFds` (Array) Deprecated File descriptors for the child to use for stdio.

> `detached` (Boolean) The child will be a process group leader.

> `uid` (Number) Sets the user identity of the process.

> `gid` (Number) Sets the group identity of the process.

The `spawn()` method returns streams (`stdout` & `stderr`) and it should be used when the process returns a volume amount of data. `spawn()` starts receiving the response as soon as the process starts executing.

####Example

> File: support.js

```
console.log("Child Process " + process.argv[2] + " executed." );
```

> File: master.js

```
const fs = require('fs');
const child_process = require('child_process');
 
for(var i = 0; i<3; i++) {
   var workerProcess = child_process.spawn('node', ['support.js', i]);

   workerProcess.stdout.on('data', function (data) {
      console.log('stdout: ' + data);
   });

   workerProcess.stderr.on('data', function (data) {
      console.log('stderr: ' + data);
   });

   workerProcess.on('close', function (code) {
      console.log('child process exited with code ' + code);
   });
}
```

run `$ node master.js`

```
stdout: Child Process 0 executed.

child process exited with code 0
stdout: Child Process 1 executed.

stdout: Child Process 2 executed.

child process exited with code 0
child process exited with code 0
```

###Fork

`child_process.fork` method is a special case of spawn() to create Node processes. It has the following signature −

```
child_process.fork(modulePath[, args][, options])
```

####Parameters

* **modulePath** (String) The module to run in the child.
* **args** (Array) List of string arguments
* **options** (Object) may comprise one or more of the following options −

> `cwd` (String) Current working directory of the child process.

> `env` (Object) Environment key-value pairs.

> `execPath` (String) Executable used to create the child process.

> `execArgv` (Array) List of string arguments passed to the executable (Default: process.execArgv).

> `silent` (Boolean) If true, stdin, stdout, and stderr of the child will be piped to the parent, otherwise they will be inherited from the parent, see the "pipe" and "inherit" options for spawn()'s stdio for more details (default is false).

> `uid` (Number) Sets the user identity of the process.

> `gid` (Number) Sets the group identity of the process.

The fork method returns an object with a built-in communication channel in addition to having all the methods in a normal ChildProcess instance.

####Example

> File: support.js

```
console.log("Child Process " + process.argv[2] + " executed." );
```

> File: master.js

```
const fs = require('fs');
const child_process = require('child_process');
 
for(var i=0; i<3; i++) {
   var worker_process = child_process.fork("support.js", [i]); 

   worker_process.on('close', function (code) {
      console.log('child process exited with code ' + code);
   });
}
```

run `$ node master.js`

```
Child Process 0 executed.
Child Process 1 executed.
Child Process 2 executed.
child process exited with code 0
child process exited with code 0
child process exited with code 0
```