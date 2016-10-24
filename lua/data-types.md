##Data Types
Lua is a dynamically typed language, so the variables don't have types, only the values have types. 
Values can be stored in variables, passed as parameters and returned as results.

In Lua, though we don't have variable data types, but we have types for the values. The list of data types for values are given below.

####Type list

* **nil**		Used to differentiate the value from having some data or no(nil) data.
* **boolean**	Includes true and false as values. Generally used for condition checking.
* **number**	Represents real(double precision floating point) numbers.
* **string**	Represents array of characters.
* **function**	Represents a method that is written in C or Lua.
* **userdata**	Represents arbitrary C data.
* **thread**	Represents independent threads of execution and it is used to implement coroutines.
* **table**		Represent ordinary arrays, symbol tables, sets, records, graphs, trees, etc., and implements associative arrays. It can hold any value (except nil).