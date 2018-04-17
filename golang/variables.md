# Variables

## Declaration

There are different ways to declare a variable. Use Method 1 if you are using it in a function and you want to imply that the assigned value is important. Use Method 2 if you want to imply that the initial value is not important.

### Method 1
```
varname := "value"
```
Declares a variable and assigns a value. The type is implied by the value assigned. Can only be used in functions.

### Method 2
```
var varname string
```
Declares a variable and its type, and assigns it the default value for that type.

### Method 3
```
var varname = "value"
```
Similar to the first method and rarely used.

### Method 4
```
var varname string = "value"
```
Declares a variable and assigns a value to it. The type declaration could be construed as redundant, but this method is useful if you need to coerce the initial value (e.g., the initial value is an integer you're storing into a float).
