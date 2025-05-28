# Type Casting

Type casting is a way to convert a var from one type to another.
C performs automatic type casting (implicit conversion).

```typeCast.c
int i = 2;
double d = 2.5;
i = (int)d; // Explicit type cast

i = d; // Implicitly the same thing.
```

short char
int
long int
u long int
float
double
long double

# Operators

- Arithmetic
- Assignment
- Increment/Decrement
- Relational
- Equality and logical
- Bitwise

## C Specific Operators

- Pointers and references (*, &, ->)
- Others (sizeof, scope, casting)

- / denotes integer division if both operands are of integral types
- 5 / 2 evaluates to 2 (decimal is truncated)

# Control flow

Condition in java must evaluate to a boolean.
In C everything that is not 0 is true.

```while.c
int i = 100;

while (i--) {
    // do stuff
}
```

Break and continue. In java break conditions can have labels. Not in C.

# Functions

## Function Prototypes

`int add(int, int);`


