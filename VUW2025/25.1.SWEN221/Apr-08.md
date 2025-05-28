# Term test 2

Read the tests!

## Longest string index

```str.java
class Exercise{
    public static String longestString(List<String> ss){
        return ss.stream()
            .max( (s1,s2)->Integer.compare(s1.length(),s2.length()) )
            .orElseThrow( IllegalArgumentException::new );
    }
    public static void main(String[] arg){...}
}
```

```indx.java
class Exercise{
    public static int longestStringIndex(List<String> ss){
        return IntStream.range(0,ss.size()).boxed()
            .max((i1,i2)
                    ->Integer.compare(ss.get(i1).length(),ss.get(i2).length()))
            .orElseThrow( IllegalArgumentException::new );
    }
    public static void main(String[] arg){ ... }
}
```

```print.java
class Exercise{
    public static String prettyPrint(List<String> names, List<String> surnames){
        if (names.size() != surnames.size()){ throw new IllegalArgumentException(); }
        return IntStream.range(0,names.size())
            .mapToObj( i->names.get(i) + " " + surnames.get(i) )
            .collect( Collectors.joining("\n") );
    }
    public static void main(String[] arg){
        String bs= "["+ prettyPrint(List.of("Bob", "Bart", "Billy"),
                List.of("McKain","Brown","Jolly"))+"]";
        assert bs.equals("[Bob McKain\nBart Brown\nBilly Jolly]"):bs;
    }
}
```

```class.java
class Exercise {//QUESTION 5
    public static void main(String[] args) {
        A a= new A();
        assert a.b().zero() == 0: a.toString();
        assert a.b().one() == 1: a.toString();
    }
}
class A{
    A b(){ return this; }
    int zero(){ return 0; }
    int one(){ return 1;}
}
```

```count.java
class Exercise {
    public static void main(String[] args) {
        A a= new A();
        assert a.b().zero() == 0: a.toString();
        assert a.b().one() == 1: a.toString();
        assert a.b().zero() == 2: a.toString();
        @SuppressWarnings("unused")
            A aa= new A();
        assert a.b().zero() == 0: a.toString();
        //Yes, it is not a typo.
        //We do mean 'a', not 'aa'.
    }
}
class A {
    A(){ count = 0; }
    A b() { return this; }
    static int count;
    int zero() { return count++; }
    int one() { return count++; }
}
```

```sets.java
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
class Exercise{
    public static List<String> removeDups(List<String> ss){
        return new java.util.ArrayList<String>(
                new java.util.HashSet<String>(ss));
    }
    public static void main(String[] args) {...}
} // Most collections have a constructor that takes another collection.
```

```lhs.java
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
class Exercise{
    public static List<String> removeDups(List<String> ss){
        return new java.util.ArrayList<String>(
                new java.util.LinkedHashSet<String>(ss));
    }
    public static void main(String[] args) {...}
} // LinkedHashSet ensures that the order is preserved.
```

```stream.java
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
class Exercise{
    public static List<String> removeDups(List<String> ss){
            return ss.stream().distinct().toList();
    }
    public static void main(String[] args) {...}
}
```

```reduce.java
return fs.stream()
    .filter(f-> f.city().equals(city))
    .reduce((f1, f2)-> f1.height() > f2.height() ? f1 : f2)
    .orElseThrow(IllegalArgumentException::new);
return fs.stream()
    .filter(f-> f.city().equals(city))
    .max(Comparator.comparing(Flower::height))
    .orElseThrow(IllegalArgumentException::new);
```
