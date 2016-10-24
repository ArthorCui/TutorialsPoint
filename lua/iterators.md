##Itrators

Iterator is a construct that enables you to traverse through the elements of the so called collection or container. In Lua, these collections often refer to tables, which are used to create various data structures like array.

###Generic For Iterator

A generic `for` iterator provides the key value pairs of each element in the collection.

In Lua we use functions to represent iterators. Based on the state maintenance in these iterator functions, we have two main types −

* **Stateless Iterators**
* **Stateful Iterators**

####Stateless Iterators

By the name itself we can understand that this type of iterator function does not retain any state.
Let us now see an example of creating our own iterator using a simple function that prints the squares of `n` numbers.

#####Syntax
```
function square(iteratorMaxCount,currentNumber)

   if currentNumber<iteratorMaxCount
   then
      currentNumber = currentNumber+1
      return currentNumber, currentNumber*currentNumber
   end
	
end

for i,n in square,3,0
do
   print(i,n)
end
```

The above code can be modified slightly to mimic the way ipairs function of iterators work. It is shown below.

```
function squares(iteratorMaxCount)
   return square,iteratorMaxCount,0
end  

for i,n in squares(3)
do 
   print(i,n)
end
```

####Stateful Iterators

The previous example of iteration using function does not retain the state. Each time the function is called, it returns the next element of the collection based on a second variable sent to the function. To hold the state of the current element, closures are used. Closure retain variables values across functions calls. To create a new closure, we create two functions including the closure itself and a factory, the function that creates the closure.

Let us now see an example of creating our own iterator in which we will be using closures.

#####Example

```
array = {"Lua", "Tutorial"}

function elementIterator (collection)

   local index = 0
   local count = #collection
	
   -- The closure function is returned
	
   return function ()
      index = index + 1
		
      if index <= count
      then
         -- return the current element of the iterator
         return collection[index]
      end
		
   end
	
end

for element in elementIterator(array)
do
   print(element)
end

#output
Lua
Tutorial
```