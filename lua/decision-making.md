## Decision Making

Decision making structures require that the programmer specifies one or more conditions to be evaluated or tested by the program, along with a statement or statements to be executed, if the condition is determined to be true, and optionally, other statements to be executed if the condition is determined to be false.

Lua programming language assumes any combination of Boolean `true` and `non-nil` values as `true`, and if it is either boolean `false` or `nil`, then it is assumed as `false` value. It is to be noted that in Lua, `zero will be considered as true`.

* **[if statement](if)**				An if statement consists of a boolean expression followed by one or more statements.
* **[if...else statement](if-else)**	An if statement can be followed by an optional else statement, which executes when the boolean expression is false.
* **[nested if statements](mix)**	You can use one if or else if statement inside another if or else if statement(s).

### IF

#### Syntax

```
if(boolean_expression)
then
   --[ statement(s) will execute if the boolean expression is true --]
end
```

#### Example

```
--[ local variable definition --]
a = 10;

--[ check the boolean condition using if statement --]

if( a < 20 )
then
   --[ if condition is true then print the following --]
   print("a is less than 20" );
end

print("value of a is :", a);

#output
a is less than 20
value of a is : 10
```

### IF-ELSE

#### Syntax

```
if(boolean_expression)
then
   --[ statement(s) will execute if the boolean expression is true --]
else
   --[ statement(s) will execute if the boolean expression is false --]
end
```

#### Example

```
--[ local variable definition --]
a = 100;

--[ check the boolean condition --]

if( a < 20 )
then
   --[ if condition is true then print the following --]
   print("a is less than 20" )
else
   --[ if condition is false then print the following --]
   print("a is not less than 20" )
end

print("value of a is :", a)

#output
a is not less than 20
value of a is :	100
```

### IF-ELSEIF-ELSE

#### Syntax

```
if(boolean_expression 1)
then
   --[ Executes when the boolean expression 1 is true --]

else if( boolean_expression 2)
   --[ Executes when the boolean expression 2 is true --]

else if( boolean_expression 3)
   --[ Executes when the boolean expression 3 is true --]
else 
   --[ executes when the none of the above condition is true --]
end
```

#### Example

```
--[ local variable definition --]
a = 100

--[ check the boolean condition --]

if( a == 10 )
then
   --[ if condition is true then print the following --]
   print("Value of a is 10" )
elseif( a == 20 )
then   
   --[ if else if condition is true --]
   print("Value of a is 20" )
elseif( a == 30 )
then
   --[ if else if condition is true  --]
   print("Value of a is 30" )
else
   --[ if none of the conditions is true --]
   print("None of the values is matching" )
end
print("Exact value of a is: ", a )

#output
None of the values is matching
Exact value of a is:	100
```

### Mix

#### Syntax

The syntax for a nested if statement is as follows −

```
if( boolean_expression 1)
then
   --[ Executes when the boolean expression 1 is true --]
   if(boolean_expression 2)
   then
      --[ Executes when the boolean expression 2 is true --]
   end
end
```

#### Example

```
--[ local variable definition --]
a = 100;
b = 200;

--[ check the boolean condition --]

if( a == 100 )
then
   --[ if condition is true then check the following --]
   if( b == 200 )
   then
      --[ if condition is true then print the following --]
      print("Value of a is 100 and b is 200" );
   end
end

print("Exact value of a is :", a );
print("Exact value of b is :", b );

#output

Value of a is 100 and b is 200
Exact value of a is :	100
Exact value of b is :	200
```