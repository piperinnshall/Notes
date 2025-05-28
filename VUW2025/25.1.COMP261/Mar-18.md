# Parsing 5

```java
interface Expr{}
record Num(int value) implements Expr{}
record Add(Expr left, Expr right) implements Expr{}
record Mul(Expr left, Expr right) implements Expr{}
record Sub(Expr left, Expr right) implements Expr{}
record Div(Expr left, Expr right) implements Expr{}
```

Abstract Syntax Tree design
How to make it useful?

First: toString, equals, hashCode.
Records already provide those three, but the default toString may be too verbose.
We can replace the default implementation with our own toString.

```java
interface Expr{}
record Num(int value) implements Expr{
    @Override //To fit on slides will omit the @Override
        public String toString(){ return ""+value; }
}
record Add(Expr left, Expr right) implements Expr{
    public String toString(){
        return "("+left+" + "+right+")";
    }
}

record Mul(Expr left, Expr right) implements Expr{/*..*/}
record Sub(Expr left, Expr right) implements Expr{/*..*/}
record Div(Expr left, Expr right) implements Expr{/*..*/}
```

No difference between `"("+left` and `"("+left.toString()`
The .toString method is called internally by the string concatenation.
That is: `""+e == e.toString()`

## OO Recursion

Look again to the toString method of before:
-- it is a recursive method --
So... how does it terminate?

If the left is an 'Add', it will call itself again (recursion continue)
If the left is a 'Num', it will just print the value (recursion stops)

In OOP, recursion often terminates via dynamic dispatch rather than explicit if conditions, which can be surprising.

Here the leaves complete toString directly without further recursion, while Add, Mul, Sub and Div delegates to their children
The recursion stops because the behaviour is chosen at runtime based on the object’s type. No need of an explicit check to stop it.

OO ==> Implicit control flow via recursion + dynamic dispatch

## AST evaluation

Iconic example operation on ASTs

Interpret the AST as code/math and compute the result

Recursion driven by dynamic dispatch (exactly as for toString)

Leaves: produce a result

Nodes: evaluate the sub expression and then combine the results

Declerative programming

```java
interface Expr{ int eval(); }
record Num(int value) implements Expr{
    public int eval(){ return value; }
}
record Add(Expr left, Expr right) implements Expr{
    public int eval(){ return left.eval() + right.eval(); }
}
record Mul(Expr left, Expr right) implements Expr{
    public int eval(){ return left.eval() * right.eval(); }
}
record Sub(Expr left, Expr right) implements Expr{
    public int eval(){ return left.eval() - right.eval(); }
}
record Div(Expr left, Expr right) implements Expr{
    public int eval(){ return left.eval() / right.eval(); }
}
```

Twists: Add with many operands instead of just left, right.
That is, the 'summatory', an operation summing many different things all together.

```java
record Add(List<Expr> operands) implements Expr{
    public String toString(){
        String res= "(" + operands.get(0);
        for (int i= 1; i < operands.size(); i++){
            res += " + "+ operands.get(i);
        }
        return res + ")";
    }
    public int eval(){
        int res= 0;
        for (var e : operands){ res += e.eval(); }
        return res;
    }
    Add{ assert operands.size() >= 2; }
}
```
