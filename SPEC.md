# The Piper Programming Language

## Basic types

### Numbers

There is only one number type: `num`. It supports floating-point numbers and integers.

```
-- The type of x has implicitly been set to num, as the type of 0 is num
x = 0
y: num = 123
```

### Strings
There also is only one type for strings: `str`.<br>
Strings can implicity be treated as arrays of characters or integers (the UTF-8 value of each character) in appropriate contexts.

```
example_string = "Hello, world!"
```

### Tuples
```
x: (num, str, [num]) = (123, "Hey", [4, 5, 6])
```

### Arrays and Ranges
An array is defined via square brackets following a list of values separated by spaces (for now, at least).

A range is defined by the format `start..end`, where `start` and `end` are bounds for the range.<br>
You may also define a range with the format `start..=end`. The bound will instead be set to `end + 1`.
```
[2 4 8 16 32]
["Hello" "World"]
```

You can also construct an array via the use of ranges:

```
-- Both return [0, 2, 4, 6, 8].
[0..10 | even]
[0..10 | x -> even x]
```

Indexing an array is done with the ! operator:

```
-- Prints "5" to stdout.
[0..10] | x -> out x!5
```

NOTE: indexing is zero-based.

Iterating over arrays with indexes and values would look like:

```
[0..10] | enumerate |> (index, element) -> out "Element {element} is at index {index}."
```

You will learn more about this when reading about **The PIPE symbol**.

## Comments
Every line that starts with `--` is treated as a comment.

```
-- This is a comment that will be ignored by the compiler/interpreter.
```

## The PIPE symbol
The PIPE (`|`) is used for  function calls in Piper. It calls a function on the right-hand side with the first argument being the value on the left-hand side: <br>
```
12345 | str | out
```

where `12345` is first turned to a string `"12345"`, and then printed to stdout.

You can also use the PIPE symbol followed by a `>` for iterating over arrays:

```
-- Will print "2 4 6 8 10" to stdout.
[1 2 3 4 5] |> *2 | join " " | out
```

You can use the `->` operator to bind values to variables in appropriate contexts:

```
-- Will also print "2 4 6 8 10" to stdout.
[1 2 3 4 5] |> x -> x * 2 | join " " | out
```

The validity of a PIPE operation depends on the context it's used in.<br>

## Variable Declaration
```
x = 0
x: num = 0

-- Parses the type of 1
x: 1 = 0
```

## Loops
Loops are achieved with the use of arrays and ranges combined with a map:
```
[0..10] |> x -> out "Hello {x}"
```

## Grammar

```
BinaryOperator  ::= '+' | '-' | '*' | '/' | '^' | '%'
Number          ::= ('-' | '+')? (NumberLiteral | Identifier)
Expression      ::= Number (BinaryOperator Number)*
```

### Tokens

```
Identifier      ::=   [a-z] [a-zA-Z0-9]*
OpenBracket     ::=   '['
CloseBracket    ::=   ']'
Pipe            ::=   '|'
Diamond         ::=   '|>'
Arrow           ::=   '->'
Range           ::=   '..'
StringLiteral   ::=   '"' [^"]* '"'
NumberLiteral   ::=   \d+
Unit            ::=   '()'
```
