<h1 style="text-align: center;">The Piper Programming Language</h1>

## Basic types

### Numbers

There is only one number type: `num`. It supports floating-point numbers and integers.

### Strings
There also is only one type for strings: `str`.<br>
Strings can implicity be treated as arrays of characters or integers (the UTF-8 value of each character) in appropriate contexts.

### Arrays and Ranges
An array is defined via square brackets following a list of values separated by spaces (for now, at least).

A range is defined by the format `start..end`, where `start` and `end` are bounds for the range.<br>
You may also define a range with the format `start..=end`. The bound will instead be `end + 1`.
```
[2 4 8 16 32]
["Hello" "World"]
```

You can also construct an array via the use of ranges:

```
[x in 0..10 | even] 
[x in 0..10 | x -> even x]
```

In the example, both return `[0 2 4 6 8]`.

## Comments
A comment in piper is simply a line that begins with `--`

```
-- This is a comment that will be ignored by the compiler/interpreter.
```

## The PIPE symbol
The PIPE (`|`) is used for most of the operations in Piper. <br>\
You can for example use it in type conversions or passing arguments to functions:
```
12345 | str | out
```

The preceding example first turns `12345` into a string `"12345"`, and then prints it to stdout

You can also use the PIPE for things such as mapping arrays:

```
-- Will print "2 4 6 8 10" to stdout.
[1 2 3 4 5] | *2 | join " " | out

```

You can use the `->` operator to bind values to variables in appropriate operations:

```
-- Will also print "2 4 6 8 10" to stdout.
[1 2 3 4 5] | x -> x * 2 | join " " | out
```

The validity of a PIPE operation depends on the context it's used in.<br>

## Variable Declaration
???

## Loops
???


