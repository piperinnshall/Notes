# New VS Old Java

RE-VISIT LECTURE

# Super

```super.java
class A{ int x; }
class B extends A{
    int x; //hiding here
    int both(){
        return this.x + super.x;
    }
}
```

We can use “super.” to call the super implementation.

```super2.java
class RoadToll{
    /*..*/
    int payFee(){ /*..*/ }
}
class RoadTollWithLog extends RoadToll{
    List<String> log= new ArrayList<>();
    @Override int payFee(){
        log.add("PayingFee on: " + LocalDateTime.now());
        var res= super.payFee();/*..*/
        log.add("Payed: " + res);
        return res;
    }
}
```

## Abstract classes vs interfaces

From Java8, both Abstract classes and interfaces can be used for code reuse. Both can not be instantiated.

They both can contain abstract methods as well as implemented/default methods.

- Abstract methods have no implementation.
- Concrete subclasses must provide it.

- Abstract classes may also contain (private) fields and constructors.

- Interfaces can have abstract getters and setters to “imagine” the presence of fields.

- When field+constructors are not strictly needed, interfaces should be used instead of abstract classes.

Interfaces
Can't have:
- fields
- constructors
- privates
Can have:
- Many

Abstract Classes
Can't have:
- Many
Can have:
- fields
- constructors
- privates

### Perfect place to use an abstract class

 The abstract class represents a set of operations working together to a goal.
- The various methods are pieces of those operations, that can be independently personalized.
- Those operation depends on some state that must be managed by the operations and not by the user code.
- That is, the abstract class code is the only responsible to
    - initialize this state
    - read/update this state
- A reusable solid foundation with state invariants can be provided by abstract classes.

```abstract.java
abstract class LibraryProperty{
    private final static List<LibraryProperty> all= new ArrayList<>();
    public LibraryProperty(){
        all.add(this);
    }
    public static List<LibraryProperty> inventory(){
        return Collections.unmodifiableList(all);
    }
}
class Book extends LibraryProperty{}
//new Book() will automatically add it to the list!
class Magazine extends LibraryProperty{}
//new Magazine() will automatically add it to the list!
class Newspaper extends LibraryProperty{}
//new Newspaper() will automatically add it to the list!
```

```abstract2.java
abstract class Animal{
    private String name;
    private int age;
    public Animal(String name, int age){
        name(name);
        age(age);
    }
    final public String name(){ return name; }
    final public int age(){ return age; }
    final public void name(String v){
        if ( v == null || v.isBlank()){ throw new IllegalArgumentException(); }
        name = v.trim();
    }
    final public void age(int v){
        if (v < 0 || v > 1000){ throw new IllegalArgumentException(); }
        age = v;
    }
}
class Cat extends Animal{//all subclasses now guarantee properties on the state
    public Cat(String name,int age){ super(name,age); }
    //...
}
```

### Perfect place to use an interface

The interface represents a set of operations working together to a goal.
● The various interface methods are pieces of those operations, that can be independently personalized.
● Those operation are either stateless or depend on state that can be initialized and observed by the USER of the operation.
- A solid foundation with state invariants is provided later by records or classes.

```interface.java
//All concrete subclasses of length must have meters() and yards() methods
interface Length{
    default double meters(){ return yards() * 0.91d; }
    default double yards(){return meters() * 1.09d; }
    default Length add(Length l){
        return new Meters(l.meters() + this.meters());
    }
}
record Yards(double yards) implements Length{}
record Meters(double meters) implements Length{}

// The field name is very relevant here: it generates a method meters() that overrides Length.meters() !!
```

```inheritance2.java
interface Chest{
    List<Item> get();
    default void depositItem(Item i){/*...*/}
}
interface Minecart{
    Point position();
    void position(Point val);
    default void move(Map map){/*...*/}
}
class MinecartChest implements Chest, Minecart{
    Point position;
    List<Item> items = new ArrayList<>();
    public MinecartChest(Point p){ position(p); }
    public List<Item> get(){ return this.items; }
    public Point position(){ return this.position; }
    public void position(Point val){ this.position = val; }
}
```

Multiple inheritance

From Java8, this is now possible!
- A class cannot have more than one superclass
- Other languages (e.g. C++) support this
- But, a class can implement more than one interface
- Interfaces can now have reusable implementation!
`class Goten extends Gohan, Trunks { … }`
`class Goten implements Gohan, Trunks { … }`

Risk of multiple inheritance: we may end up with too much stuff
- A class that is too fat. (violating the single responsibility principle)
- To avoid this, we need to make the interfaces used to modularize our behaviour as slim as possible
- We can have many different interfaces, sometimes with just a single default method (and the private methods that it uses internally)
- The other methods will be abstract and defined in other interfaces.
