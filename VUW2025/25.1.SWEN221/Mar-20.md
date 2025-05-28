# Assertions

Capital B Boolean type has true, false, null.

assert can fail because the expression in the assertion can fail.

```java
public static Boolean b;
assert b;
// Throws NullPointerException
```

## Kinds of Testing

- Manual Testing
- Automatic Testing
- (Automatic) Property based testing on a fixed dataset
- Property based testing on automatically generated data sets == Fuzz testing 
- Runtime verification
    -  using assertions inside of methods to verify method contracts (using assert e;)
    - Runtime verification is kick-started from unit tests


Assertions vs Testing


## Programatically enabled assertions

``` assert.java
public class Main {
    public static void main(String[]a){
        ClassLoader.getSystemClassLoader()
            .setDefaultAssertionStatus(true);
        assert false:"Will it break here?";
        System.out.println("Hello");
        Other.method();
    }
}
class Other{
    static void method(){
        assert false:"Or here?";
        System.out.println("World");
    }
}
```
# Contracts and invariants

- Precondition: blame the user of your code
    - Debugging/testing support
    - Active documentation. The error can point to the documentation about your functionality
    - Can be an assert
    - Can be an if(cond){ throw new IllegalArgumentException(..); }``
- Postcondition
    - Debugging/testing support
    - Can be an assert
    - Can be another kind of ‘Error’
- Invariant: some property that holds for all the instances of a type

```invariant.java
record Positive(int x){ Positive{ assert x >= 0; } }
record Even(int x){ Even{ assert x % 2 == 0; } }
record Person(String name, Positive age){
    Person{
        assert name != null;
        assert !name.isEmpty();
        assert !name.contains("\n");
    }
}
```
