## Strings

String is a sequence of characters as well as control characters like form feed. String can be initialized with three forms which includes −

> Characters between single quotes		`` ``
> Characters between double quotes		`" "`
> Characters between [[ and ]]			`[[]]`

```
string1 = "Lua"
print("\"String 1 is\"",string1)

string2 = 'Tutorial'
print("String 2 is",string2)

string3 = [["Lua Tutorial"]]
print("String 3 is",string3)
```

### Syntax

* `\a`	Bell
* `\b`	Backspace
* `\f`	Formfeed
* `\n`	New line
* `\r`	Carriage return
* `\t`	Tab
* `\v`	Vertical tab
* `\\`	Backslash
* `\"`	Double quotes
* `\'`	Single quotes
* `\[`	Left square bracket
* `\]`	Right square bracket

### String Manipulation

* `string.upper(arg)`
* `string.lower(arg)`
* [`string.gsub(mainString,findString,replaceString)`](#gusb)
* [`string.strfind(mainString,findString, optionalStartIndex,optionalEndIndex)`](#find-reverse)
* [`string.reverse(arg)`](#find-reverse)
* [`string.format(...)`](#format)
* [`string.char(arg) and string.byte(arg)`](#char-byte)
* `string.len(arg)`
* [`string.rep(string, n))`](#rep)
* [`..`](#d-dot)

#### gsub

> Returns a string by replacing occurrences of findString with replaceString.

```
string = "Lua Tutorial"

-- replacing strings
newstring = string.gsub(string,"Tutorial","Language")
print("The new string is",newstring)

#output
The new string is	Lua Language
```

#### find-reverse

> Returns the start index and end index of the findString in the main string and nil if not found.

```
string = "Lua Tutorial"

-- replacing strings
print(string.find(string,"Tutorial"))
reversedString = string.reverse(string)
print("The new string is",reversedString)

#output
5	12
The new string is	lairotuT auL
```

#### format

> Returns a formatted string.

```
string1 = "Lua"
string2 = "Tutorial"

number1 = 10
number2 = 20

-- Basic string formatting
print(string.format("Basic formatting %s %s",string1,string2))

-- Date formatting
date = 2; month = 1; year = 2014
print(string.format("Date formatting %02d/%02d/%03d", date, month, year))

-- Decimal formatting
print(string.format("%.4f",1/3))

#output
Basic formatting Lua Tutorial
Date formatting 02/01/2014
0.3333
```
#### char-byte

> Returns internal numeric and character representations of input argument.

```
-- Byte conversion

-- First character
print(string.byte("Lua"))

-- Third character
print(string.byte("Lua",3))

-- first character from last
print(string.byte("Lua",-1))

-- Second character
print(string.byte("Lua",2))

-- Second character from last
print(string.byte("Lua",-2))

-- Internal Numeric ASCII Conversion
print(string.char(97))

#output
76
97
97
117
117
a
```
#### rep

> Returns a string by repeating the same string n number times.

```
string1 = "Lua"
string2 = "Tutorial"

-- Repeating strings
repeatedString = string.rep(string1,3)
print(repeatedString)

#output
LuaLuaLua
```
#### d-dot

> Thus operator concatenates two strings.

```
string1 = "Lua"
string2 = "Tutorial"

-- String Concatenations using ..
print("Concatenated string",string1..string2)

#output
Concatenated string	LuaTutorial
```