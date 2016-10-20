##Global-Objects

Node.js global objects are global in nature and they are available in all modules. 
We do not need to include these objects in our application, rather we can use them directly. These objects are modules, functions, strings and object itself as explained below.

* **__filename**

> The `__filename` represents the filename of the code being executed. This is the resolved absolute path of this code file. For a main program, this is not necessarily the same filename used in the command line. The value inside a module is the path to that module file.

* **__dirname**

> The `__dirname` represents the name of the directory that the currently executing script resides in.

* **setTimeout(cb, ms)**

> The `setTimeout(cb, ms)` global function is used to run callback cb after at least ms milliseconds. The actual delay depends on external factors like OS timer granularity and system load. A timer cannot span more than 24.8 days.

> This function returns an opaque value that represents the timer which can be used to clear the timer.

* **clearTimeout(t)**

> The `clearTimeout(t)` global function is used to stop a timer that was previously created with setTimeout(). Here t is the timer returned by the setTimeout() function.

* **setInterval(cb, ms)**

> The `setInterval(cb, ms)` global function is used to run callback cb repeatedly after at least ms milliseconds. The actual delay depends on external factors like OS timer granularity and system load. A timer cannot span more than 24.8 days.

> This function returns an opaque value that represents the timer which can be used to clear the timer using the function `clearInterval(t)`.