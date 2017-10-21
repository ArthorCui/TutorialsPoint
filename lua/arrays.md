## Arrays

Arrays are ordered arrangement of objects, which may be a one dimensional array containing a collection of rows or a multi-dimensional array containing multiple rows and columns.

In Lua, arrays are implemented using indexing tables with integers. The size of an array is not fixed and it can grow based on our requirements, subject to memory constraints.

### One-Dimensional Array

A `one-dimensional` array can be represented using a simple table structure and can be initialized and read using a simple `for loop`. 

```
array = {"Lua", "Tutorial"}

for i= 0, 2 do
   print(array[i])
end
```

### Multi-Dimensional Array

Multi-dimensional arrays can be implemented in two ways.

> Array of arrays

> Single dimensional array by manipulating indices

#### Example

```
-- Initializing the array
array = {}

for i=1,3 do
   array[i] = {}
	
   for j=1,3 do
      array[i][j] = i*j
   end
	
end

-- Accessing the array

for i=1,3 do

   for j=1,3 do
      print(array[i][j])
   end
	
end
```
output:

```
1
2
3
2
4
6
3
6
9
```

##### The other way

```
-- Initializing the array

array = {}

maxRows = 3
maxColumns = 3

for row=1,maxRows do

   for col=1,maxColumns do
      array[row*maxColumns +col] = row*col
   end
	
end

-- Accessing the array

for row=1,maxRows do

   for col=1,maxColumns do
      print(array[row*maxColumns +col])
   end
	
end
```

output:

```
1
2
3
2
4
6
3
6
9
```
