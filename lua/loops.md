## Loops

There may be a situation when you need to execute a block of code several number of times. 
In general, statements are executed sequentially − the first statement in a function is executed first, followed by the second, and so on.

Programming languages provide various control structures that allow for more complicated execution paths.

Lua provides the following types of loops to handle looping requirements.

* **[while loop](#while-loop)**
* **[for loop](#for-loop)**
* **[repeat...until loop](#repeat-until-loop)**
* **[nested loops](#nested-loops)**

### While-Loop

Repeats a statement or group of statements while a given condition is true. It tests the condition before executing the loop body.

#### Syntax
```
while(condition)
do
   statement(s)
end
```

#### Example
```
a=10

while( a < 20 )
do
   print("value of a:", a)
   a = a+1
end

#output
value of a:	10
...
...
value of a:	19
```

### For-Loop

Executes a sequence of statements multiple times and abbreviates the code that manages the loop variable.

#### Syntax
```
for init,max/min value, increment
do
   statement(s)
end
```

> The init step is executed first, and only once. This step allows you to declare and initialize any loop control variables.

> Next, the max/min. This is the maximum or minimum value till which the loop continues to execute. It creates a condition check internally to compare between the initial value and maximum/minimum value.

> After the body of the for loop executes, the flow of the control jumps back up to the increment/decrement statement. This statement allows you to update any loop control variables.

> The condition is now evaluated again. If it is true, the loop executes and the process repeats itself (body of loop, then increment step, and then again condition). After the condition becomes false, the for loop terminates.

#### Example
```
for i=10,1,-1 
do 
   print(i) 
end

#output
10
...
...
1
```

### Repeat-Until-Loop

A `repeat...until loop` is similar to a while loop, except that a do...while loop is guaranteed to execute at least one time.
Repeats the operation of group of statements till the until condition is met.

#### Syntax
```
repeat
   statement(s)
while(condition)
```

#### Example

```
--[ local variable definition --]
a = 10

--[ repeat loop execution --]
repeat
   print("value of a:", a)
   a = a + 1
until( a > 15 )

#output
value of a:	10
value of a:	11
value of a:	12
value of a:	13
value of a:	14
value of a:	15
```

### Nested-Loops

You can use one or more loop inside any another while, for or do..while loop.

#### Syntax

The syntax for a `nested for loop` statement in Lua is as follows −

```
for init,max/min value, increment
do
   for init,max/min value, increment
   do
      statement(s)
   end
   statement(s)
end
```

The syntax for a `nested while loop` statement in Lua programming language is as follows −

```
while(condition)
do
   while(condition)
   do
      statement(s)
   end
   statement(s)
end
```

The syntax for a `nested repeat...until loop` statement in Lua programming language is as follows −

```
repeat
   statement(s)
   repeat
      statement(s)
   until( condition )
until( condition )
A final note on loop nesting is that you can put any type of loop inside of any other type of loop. For example, a `for loop` can be inside a `while loop` or vice versa.
```

#### Example

```
j =2
for i=2,10 do
   for j=2,(i/j) , 2 do
	
      if(not(i%j)) 
      then
         break 
      end
		
      if(j > (i/j))then
         print("Value of i is",i)
      end
		
   end
end

#output
Value of i is	8
Value of i is	9
Value of i is	10
```