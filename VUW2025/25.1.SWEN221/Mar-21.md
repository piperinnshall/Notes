# Static Inner classes

Static Inner classes, often called nested classes in other
languages, are just a way to do Hierarchical code organization.

(Non-static) Inner classes, are much more complex, that Static Inner classes!
Note: inner records are implicitly static, and may be better for this use case

```static.java
public interface Exp {
    public static class StringLiteral implements Exp{
        String value;
    }
    public static class FieldAccess implements Exp{
        Exp receiver; String fName;
    }
    public static class MethodCall implements Exp{
        Exp receiver; String mName; List<Exp> parameters;
    }
    public static class BinOp implements Exp{
        Op op; Exp left; Exp right;
        public static enum Op{ Plus, Minus, And, Or, ... }
    }
}
```

```beer.java
class Foo {
    public static class Bar {...}
    private static class Beer {...}
    ...
}
public class Main {
    public static void main(String[] args){
        Foo.Bar bar= new Foo.Bar();
        System.out.println(bar);
        System.out.println(Exp.BinOp.Op.Plus);
    }
}
```

# (Non-static) Inner Classes

- static inner classes -> property of classes
    - a single Foo.Bar class exists
- inner classes -> property of instances
    - each instance have its own (non-static) inner classes

In the same way as
static fields -> property of classes
fields -> property of instances

```nonstatic.java
class IntList implements Iterable<Integer> {
    private int[] data;
    private int size= 0;
    /* ... */
    public IntList() {this.data= new int[4];}
    public Iterator<Integer> iterator() {
        return new InternalIter();
    }
    private class InternalIter implements Iterator<Integer>{
        private int pos= 0;
        public boolean hasNext() {return pos < size;}
        public Integer next(){return data[pos++];}
        /* ... */
    }
}
```

The inner class knows about the instance that created it.

Enclosing class can construct and return instances of inner class.

Other classes cannot construct instances as it’s private.

Inner classes have outer pointers.

For accessing fields/methods of enclosing class (outer).

Outer pointer automatically supplied for new inner class.

IntList.this is a field name that is inside int list declared inside of internal iterator.

This means that we can use this explicit name to acces it.

```internal.java
class IntList implements Iterable<Integer> {
    private int[] data;
    private int size= 0;/* ... */
    private class InternalIter implements Iterator<Integer>{
        private int pos= 0;/* ... */
    }
}
```

External construction

```construct.java
class Shape {
    /* ... */
    public class Square {
        private int x, y, width, height;
        public Square(int x, int y, int width, int height){
            /* ... */
        }
    }
}
/* ... */
Shape outer= new Shape();
Shape.Square square= outer.new Square(0,0,8,42);
square= new Shape().new Square(0,0,8,42);
```

Static Inner Classes have no outer pointer. So you can not access fields/methods of enclosing class.

But, can construct without providing outer pointer.

If no need to access enclosing info, then this is more convenient (and potentially more efficient).

(Non-Static) Inner Classes have outer pointer.

So, they have multiple this and can use it to (implicitly/explicitly) access fields/methods of enclosing instance

But, can not be instantiated without providing the outer pointer.

# Method local inner class

```methodlocal.java
lass Outer {
    public Outer create(final int field) {
        class Inner extends Outer {
            private int myfield= field;
            /*...*/
        };
        return new Inner();
    }
}
```

Non-static method local class Inner (has pointer).

Can access local variables + parameters provided they are (effectively) final.

Can even define classes within a method!
- These are only visible within that method
- But, their instances can still be returned
- Cannot have static method-local classes

# Anonymous classes

```anon.java
public static void main(String[] args) {
    List<String> myList = new ArrayList<String>(){
        // override ArrayList.add
        public boolean add(String x) {
            System.out.println("ADDED: " + x);
            return super.add(x);
        }
    };
}
```

Anonymous Class
- Has no class definition and, hence, no name
- Defined as an extension of existing class
- Can override methods and/or define fields

```test.java
public class Test {
    private int field;
    public Test(int field) { this.field = field; }
    public void aMethod() { /*...*/ }
    public static void main(String[] a) {
        Test x = new Test(1) {
            public void aMethod() {
                System.out.println("GOT "+a+" "+field);
            }
        };
    }
}
```

```sort.java
ArrayList<String> ls=/*...*/;
Collections.sort(ls,new Comparator<String>(){
        public int compare(String s1, String s2) {
        return s1.compareToIgnoreCase(s2);
        }});
```

# Swing

```before8.java
import java.awt.*; import java.awt.event.*; import javax.swing.*;
public class MiniGui extends JFrame {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
                public void run() {
                MiniGui g= new MiniGui();
                g.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
                g.getRootPane().setLayout(new BorderLayout());
                JButton b= new JButton("------Bar------");
                b.addActionListener(new ActionListener() {
                        public void actionPerformed(ActionEvent e) {
                        System.out.println("Button pressed");
                        }});
                g.getRootPane().add(b, BorderLayout.CENTER);
                g.pack();
                g.setVisible(true);
                }});
    }
}
```

```after8.java
import java.awt.*; import java.awt.event.*; import javax.swing.*;
public class MiniGui extends JFrame {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(()->{
                MiniGui g= new MiniGui();
                g.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
                g.getRootPane().setLayout(new BorderLayout());
                JButton b= new JButton("------Bar------");
                b.addActionListener(e->
                        System.out.println("Button pressed"));
                g.getRootPane().add(b, BorderLayout.CENTER);
                g.pack();
                g.setVisible(true);
                });
    }
}
```

# IMPORTANT

A Person have a String name and many Person friends.
A Group of friend represent a set of friendships.
We want to enforce the following:
A Person only belong to a single Group, and have friends only in that Group.

```important.java
public class Group{
    private List<Person> ps= new ArrayList<>();

    // Protected
    public List<Person> persons(){ return Collections.unmodifiableList(ps); } 

    // Doesn't take a person so you cannot pass a person to different group
    public void addPerson(String name){ ps.add(new Person(name)); }

    private void checkInGroup(Person p){ if (!ps.contains(p)){ throw new Error(""); } }

    public void connect(Person p1, Person p2){
        checkInGroup(p1);
        checkInGroup(p2);
        if (p1 == p2){ return; }
        if (p1.friends.contains(p2)){ return; }
        p1.friends.add(p2);
        p2.friends.add(p1);
    }

    public final static class Person{ //important: nested
        private String name; //private mutable state
        public String name(){ return this.name; } //get, but no setter
        private Person(String name){ this.name= name; } //private constructor
        private List<Person> friends= new ArrayList<>(); //private mutable state
        public List<Person> friends(){ return Collections.unmodifiableList(friends); }
        public String toString(){ return ...; }
    }
}
```

Private means private to the whole set of nested classes.

Outermost class and every class inside can access the private members of every top level class.

This is hard to do but good.

This is how to protect yourself from the invariant future.

## A more usable group

```usable.java
public class Group implements ReadGroup,Serializable{...
    public final static class Person implements Serializable{..}
    public Group deepClone(){ return DeepClone.copy(this); }
}


public interface ReadGroup{
    public List<Group.Person> persons();
    public static ReadGroup of(Group g){
        return new ReadGroup(){
            public List<Group.Person> persons(){
                return g.persons();
            }
        };
    }
}

class DeepClone{
    @SuppressWarnings("unchecked")
        public static <T> T copy(T orig){
            var aux= new ByteArrayOutputStream();
            try (var o= new ObjectOutputStream(aux)){ o.writeObject(orig); o.flush(); }
            catch(IOException e){ throw new Error(e); }
            var a= aux.toByteArray();
            try (var i= new ObjectInputStream(new ByteArrayInputStream(a))){
                return (T)i.readObject();
            }
            catch(IOException|ClassNotFoundException e){ throw new Error(e); }
        }
}
```
