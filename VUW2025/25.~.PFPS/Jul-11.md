# Meta Lang 

Simple Language.

Write a bar.

Above: Consequence.
Below: Precondition.
Side: Side condition.

Featherweight java.

## Define some grammar

e::=x | e.m(es) | new C(es) |e.f

es ::= e1...en 

x is an expression

e.m(es) is an expression

Everything a bar over it.

The bar has a symbol that separates the stuff on top from the stuff on the
bottom.

# Evaluating a program

Reduction 

Have a big expression, and reduce it to something you cant reduce any further.

Arrow between them

3+(2*7) - reduce
3+14
17

Reduction cannot happen:

`new Bar().Foo`

Stuck, something we would not like to call a value.

Any other term that cannot be reduced is a bad term.

_ whatever is there 

Controversial- how big is the scope of the "I Dont care"


# full -> core

Syntax sugar

Omit parentheses

Etc.

Inference

```meta
foo.bar(x -> x + 1);

foo.<string>bar(new function<T1,T2>(){...})
```


# Structural inductive notation

```meta
# Define
```

No free variable in the regex.

Do not replace with X.

Can get very confusing.

```meta
A(x)[x=B(y)][y=c]

A[B(y)] 
A[B(c)]
```

```meta
new A(new B( new C())).f.g
```

The try catch will be handles specifically.

Manually write propagation rules.

```
        e -> e prime
---
[v].f   e.f -> e prime.f

                e -> e prime
---
new C( Vs e es) -> new C( vs e prime es)
```

Problem -> Solution

Grammar P,S

set of steps that goes towards the solution.


