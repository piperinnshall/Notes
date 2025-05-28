# Time travel

the `this` reciever is the key.

## Static type and Dynamic type

```typing.java
interface Animal {
    default void run(){}
}
class Horse implements Animal{

}
class Dog implements Animal{

}

Horse x = new Horse(“fury”);
Animal y = x;
//y is still a horse.
//But it is ‘dressed’ like an animal
}
```

Static (or Declared) type of y is “Animal”.


Dynamic (or Runtime) type of x and y is “Horse”.

- Static Type
    - Declared type of a variable

- Dynamic Type
    - Type of object referred to by variable
    - potentially different in different moments

Time travel is good because of:

## Open code!

Future users of your code (this includes you) can make better use/reuse of your code.

- Most OO programming patterns are based on dynamic dispatch.
- (we will see later) Enables for better testing and Mock objects.


## Open code :(

``` scary.java
interface Point{ int x(); int y(); }
...
void usePoint(Point p){
System.out.println(p.x());
}
```

## Blocking time travelling

Final classes, final methods.

In Java the ‘final’ keyword means different things depending on where it is used.

- A final field or local variable can not be updated
- A final class can not be extended
    - prevents further time traveling from that type!
- A final method can not be overridden
    - prevents further time traveling from that method

- Record are always final!
- New: 'sealed' interfaces / classes are now available (see more later)

Records can't do time travel :(

Interfaces can never be instanciated

```example.java
interface Destiny{
    default void accept(){
        System.out.println("Oh, well..");
    }

    default int fight(){
        this.accept();
        return Integer.MAX_VALUE;
    }
}

class Future implements Destiny {
    @Override
    void accept() {
        System.out.println("Time Travel!")
    }

    public Future() {
        this.fight();
    }
}

public static void main(String[] args) {
    new Future();
}


// Prints: "Time Travel!"
```

