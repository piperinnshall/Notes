# I also missed two swen lectures from being sick

relatable content.

# Structured data

"Structured data send to data that is organized and design in a specific way to make it easily readable and understand by both humans and machines."

# Streams

I do love lambdas but I do not know the true nature of them, when can I be worthy.

Streams are all about lambdas.

Lambdas are instructions encapsulated in a box that can be passed around without being instantly executed.

Sounds rather anonymous?

Lambdas can have params: `x -> x * 4` 

Or none: `() -> System.out.println("")`

Streams are great for collections.

The main thing to keep in mind is the size of the input and output.

```Map.java
List<Person> persons = List.of(...);
List<String> names = persons.stream()
    .map( p -> p.name );
    .toList();
```

What if there are elements you don't like?

```Filter.java
List<Person> persons = List.of(...);
List<String> names = persons.stream()
    .filter( p -> imNotTypingThatMethodNameFrom(p) )
    .toList();

public boolean imNotTypingThatMethodNameFrom(Person p) { return p.name() == "Marco" } 

    // Stream<T> filter(Predicate<? super T> predicate)
    // filter(true) does not work
    // filter(p -> p.getAge() >= 18)
    // filter(p -> p.isAdult())
```

```Foreach.java
persons.stream()
    .flatMap( p -> p.friends().stream() )
    .forEach( p -> cat.stealBurger(p))

// I dont really get this one syntax wise...
// What is a cat... probably an instance of some cat record.
// Is the cat stealing a burger from all of the persons friends? 
// I think so. I originally thought it was stealing a burger from the person per the amount of friends they have.
// Okay maybe I get it now.
// what if i want all of a persons friends to steal one burger from the person?
// Would it be p -> p.stealBurger(/*what do i put in here*/)
// How do I talk to the top level person?
``` 

WAIT THIS RELATES TO THE NESTED CLASSES ON 21/03 (today) thats really cool.

because you can foreach on the friends, which are inside of the nested class Friend.
