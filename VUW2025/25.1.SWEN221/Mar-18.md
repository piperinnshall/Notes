# Java Exceptions and Norse Mythology

Odin

throwable
the father of all exceptions

Thor
Exception

Loki
Error

Heimdall
RuntimeException

WATCH PREV LECTURE

## Resource handling

```finally.java
void foobar(){
    FileOutputStream tmp= new FileOutputStream("tmp.dat");
    try {
        ... // do some complicated computation
            ... // writing results to temporary file
    }
    catch (IOException e) {
        ... // report write error and return
    }
    finally {
        tmp.close();
        new File("tmp.dat").delete(); // delete temporary file
    }
}
```

We need a Goldilocks hero
- The catch block should use a hero that is ‘just right’
- Not too strong
- Not too weak
Otherwise we would capture more than we intend to == collateral damage

```abc.java
try { /*a*/ }
catch (SomeException e){ /*b*/ }
/*c*/
try { /*a*/ }
catch (SomeException e){ /*b*/ }
finally { /*c*/ }
```

```solution.java
try {
    throw new AnotherException();
}
catch (SomeException e){
    System.out.println(“Hello”);
}
finally {
    System.out.println(“World”);
}

try {
    throw new AnotherException();
}
catch (SomeException e){
    System.out.println(“Hello”);
}
System.out.println(“World”);
```

Problems with checked errors

```wrong.java
interface Statement{
    void execute();
}
class InputStatement implements Statement{
    public void execute(){
        InputStream input= ...;
        input.read(); //throws IOException
    }
}
```

```right.java
interface Statement{
    void execute();
}
class InputStatement implements Statement{
    public void execute(){
        InputStream input= ...;
        try { input.read(); } //throws IOException
        catch (IOException e){ throw new Error(e); }
    }
}
```

# Assertions and contracts

Added in Java 1.4

Basic use is extremely simple:
- assert condition;
Or
- assert condition : message;

- assert x!=null : ErrorHelpers.notNull("x","Reason");


