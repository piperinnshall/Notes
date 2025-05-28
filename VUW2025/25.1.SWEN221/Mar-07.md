# Subtyping vs Coercion

## Subtyping

In Java, we can write the following:

`void g(Object y) { … }
void f(String x) { g(x); }`

- This is OK because a String is always a valid Object

But, this does not compile:

`void g(String y) { … }
void f(Object x) { g(x); }`

- Because an Object is not always a valid String.
- E.g. an Integer is not a String

For two classes/interfaces A and B:
- if A extends B, or A implements B, then A <: B

Subtyping properties:
- Transitive
    - If X <: Y and Y <: Z then X <: Z

- Reflexive
    - X <: X always holds!

- So, does Coloured3DPoint <: Point hold?

`class Point { int x; int y; … }
class ColouredPoint extends Point { int colour; }
class Coloured3DPoint extends ColouredPoint { int z; }`

The static type should not changed the behavior.
Sadly, this is not the case for the ugly parts of Java.
Ugly == the static type changes the behavior.

## Coercion

Primitive types do not have normal subtyping/casting.

Numbers (widening coercion)
- less precise <: more precise
    - int <: float
    - float <: double
- Narrowing conversions
    - Requires explicit coercion

What is the correct code?

Explicit coercion
`float a= 3f;
int b= a;`

Implicit Coercion
`int a= 3;
float b= a;`

Explicit coercion
`double a= 3d;
float b= a;`

Implicit Coercion
`float a= 3f;
double b= a;`


- 1 + 2.0 = 3.0 --> 3.0d 
- 1 / 2 = 0
- 1 / 2.0 = 0.5 = 1/2d = 0.5d
- int x= 1 / 2.0; //not compile
- int x= (int)(1 / 2.0); --> x == 0

make sure to use f and d

Type coercion != Class Cast

Comparision: Type coercion V.S. Class cast

Coercion creates a new number.
Class Cast is just a check. Does not create anything.

Coercion makes another entity (the new number), somehow similar to the original one.
Class Cast evaluates in the original object.

It is ok to overload with a different number of parameters

What gets printed?

```clickBang.java
class Person { … }
class StrongPerson extends Person { … }
class Car {
    void shutDoor(Person p) {
        System.out.println("click");
    }
    void shutDoor(StrongPerson s) {
        System.out.println("BANG!");
    }}
Car c= new Car();
Person jim= new StrongPerson();
StrongPerson henry= new StrongPerson();
c.shutDoor(jim);
c.shutDoor(henry);
```

Compiler likes static types so ""click" "BANG!"" is printed.

This is ugly java.

### Method dispatch

- Method dispatch:
    - Two phases - compile time and runtime
- Static checking phase (overloading resolution): `//That is, we have to handle the ugly first`
    - Based on static types of receiver and parameters
    - Only visible methods defined in the receiver static type
- Dynamic dispatch (overriding resolution):
    - Selection of method at runtime
    - Dynamic choice depends only on receiver


Static checking phase (overloading resolution):
- Identify static type of receiver
- Find methods that could possibly apply
    - Correct name (also search in super-types)
    - Visible
    - Correct number of arguments
    - Argument types that could apply
        - By looking at Static types
        - Take into account subtyping and coercion
- Choose the most specific method (overloading)

#### Method descriptor

Method descriptor == Method name and static types of arguments. Not return types.

As result of this phase you have a method descriptor.
The method descriptor is chosen statically.

It is ‘as if’ Javac during compilation were replacing the method names with the more pedantic method descriptors.
