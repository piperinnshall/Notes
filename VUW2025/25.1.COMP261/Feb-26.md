# Use Programming to communicate info

Self documenting code

```bad.java
void mayRelax(){
    if(........){//if we are home
        ..... //change
        .....
        ..... //open beer
        ..... //drink
        ..2.. //number of beers
        .....
    }
}
```

```good.java
void mayRelax(){
    var atHome= ........;
    if(!atHome){ return; }
    change();
    openBeer();
    drink(2);
}
void change(){.....}
void openBeer(){.....}
void drink(int numberOfBeers){.....}
```

Limit indentation length!

Use if-return / if-throw. Avoid 'else' when possible. Use sub methods.

## Unreachable code

```bad.java
//Unreachable code - Still bad
String findSomething(){
    for(..){
        if(..){ return x; }
    }
    return null;//unreachable code!
}
```

```good.java
String findSomething(){
    for(..){
        if(..){ return x; }
    }
    throw new Error("Unreachable");
}
```

Throwing an error can ensure we know what our code is doing.

## Collections

```collections.java
var ns= List.of(1,2,3,4);
System.out.println(ns); //[1, 2, 3, 4]
ns.add(10);//fails -- unmodifiable collection!
           //A useful kind of failure.
List<Integer> empty= List.of(); //No object allocation

var mySet= Set.of(1,2,3);
var myMap= Map.of("Bob",27, "Alice",32, "Marco",42);

assert myMap.size() == 3:"assert checks for true facts";
```

### Records

```recordsIntro.java
record Person(String name, int age){}
//Equivalent definitions: the one liner above is equivalent to the code below
class Person{
    private final String name;
    private final int age;
    public Person(String name, int age){ this.name= name; this.age= age; }
    public String name(){ return name; } //name getter (note: not getName)
    public int age(){ return age; } // age getter (changing conventions)
    public String toString(){..}
    public int hashCode(){..}
    public boolean equals(Object o){..}
}

Person bob = new Person("Bob",27); //We instantiate an object of type Person

System.out.println(bob); //Prints Person[name=Bob, age=27]

assert List.of(new Person("Bob",27)).contains(bob):"Ok, thanks to equals+hashCode";
```

Always use records over classes, unless there is a very good reason.

## Compiling Java

```marcosJavaBuilder.java
//On windows build with:
//..\jdk-xxx\bin\java.exe --enable-preview src\build.java
//On Mac or Linux build with:
//../jdk-xxx/bin/java --enable-preview src/build.java
import ...
//------ This part can be changed to fit your needs ------
Path srcDir= Path.of("src");//you can rename those three as you want
Path binDir= Path.of("bin");
Path libDir= Path.of("lib");
String javaVersion= "23";
List<String> vmArguments= List.of(
        "--enable-preview",//other VM arguments may go here
        "-ea"//remove this if your *really* want to disable assertions
        );
//Here you can enable/disable build steps
void main() throws IOException, InterruptedException{
    errOnEmpty(javaFiles, srcDir);
    compile();
    runMain("main.Main",List.of());
    //runMain("Main",List.of());//example outside of package
}
//More code below implementing compile, runMain etc.. 118 lines file
```

New Java has a very interesting feature, allowing Java to run without compiling.
(and without a main class, just a main method!)
