# Inheritance

Factor out all of the common code into an interface.

Don't copy paste.

```horse.java
record Point2D(double x, double y){}

record Horse(String name, Point2D location){
    
    Horse withLocation(Point2D dest){ return new Horse(name,dest); }

    double speed(){ return 10d; }

    void draw(Graphics2D g){/*...*/}

    Horse run(Point2D dest){
        double s = this.speed(); //Local vars initialized when declared

        double diffX = dest.x() - location.x();
        double diffY = dest.y() - location.y();

        double distance= Math.sqrt(diffX * diffX + diffY * diffY);

        if (distance < s){ return this.withLocation(dest); }//Early exit (guard) when possible
        double dir= Math.atan2(diffY,diffX);//Local vars as late as possible
        return this.withLocation(new Point2D(
                    location.x() + s * Math.cos(dir),//complex subexpressions are fine
                    location.y() + s * Math.sin(dir) //if well formatted
                    ));
    }
}
```

Other running animals would use the same code, so we re-use the run method.

```animal.java
interface Animal{ //interface animal: a generalization of dog/horse
    String name(); //fields are now just methods
    Point2D location(); //speed() was a method originally
    double speed(); //note how there is no difference any more!
    void draw(Graphics2D g); //abstract methods for unique behavior
    Animal withLocation(Point2D dest); //abstract methods for unique behavior

    default Animal run(Point2D dest){ //default methods for common behavior
        double s = this.speed();
        double diffX = dest.x() - location().x();
        double diffY = dest.y() - location().y();
        double distance= Math.sqrt(diffX * diffX + diffY * diffY);

        if (distance < s){ return this.withLocation(dest); }

        double dir= Math.atan2(diffY,diffX);
        return this.withLocation(new Point2D(
                    location().x() + s * Math.cos(dir),
                    location().y() + s * Math.sin(dir)
                    ));
    }
}


// Now the horse is much smaller

record Horse(String name, Point2D location) implements Animal{
    public Horse withLocation(Point2D dest){ return new Horse(name,dest); }
    public double speed(){ return 10d; }
    public void draw(Graphics2D g){/*..*/}
}
```

What if we want a mutable running animal.

```mutable.java
interface Animal{
    String name();
    Point2D location();
    void location(Point2D location); //new method: a setter!
    double speed();
    void draw(Graphics2D g);
    default void run(Point2D dest){
        double s = this.speed();
        double diffX = dest.x() - location().x();
        double diffY = dest.y() - location().y();
        double distance= Math.sqrt(diffX * diffX + diffY * diffY);
        if (distance < s){ this.location(dest); return; } //acceptable in 1 line
        double dir = Math.atan2(diffY,diffX);
        this.location(new Point2D(
                    location().x() + s * Math.cos(dir),
                    location().y() + s * Math.sin(dir)
                    ));
    }
}
```

Overriding is defining a new implementation for an existing method, 1 method with many different implementations.

Implementation hierachry searches for the most specific implementation.

Template method pattern.

```template.java
default void draw(Graphics2D g){
    drawWall(g);
    drawWindows(g);
    drawDoor(g);
    drawRoof(g);
}

// the hook methods

default void drawWall(Graphics2D g){
    g.setColor(Color.GRAY);
    g.fillRect(50,200,300,100);
}
default void drawWindows(Graphics2D g){
    g.setColor(Color.CYAN);
    g.fillRect(60,210,30,20);
    g.fillRect(60,240,30,20);
}
```

# Time travel

good oop can ascend time and change the normal control flow.

code written in the future can call the code in the past and vice versa.

Overriding hook methods causes code from the past (template method) to call code from the future.

the `this.` reciever is the key for time travel in this case.

# Static vs dynamic types.


