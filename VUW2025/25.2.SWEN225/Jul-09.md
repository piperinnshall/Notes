# Operation Max

# Operation toList

```Java
static List<Integer> toList(Stack s) {
    return fillList(s, new ArrayList<Integer>());
}


static List<Integer> fillList(Stack s) {
}
```

# Operation fromList

```Java
for(var i:is) { res = res.push(i); }
for(var i:is.reversed()) { res = res.push(i); } // J22
```

# Records

```Java
interface Greeter {
}
```

# Compact Code

- Trying to get the work done is a bad idea. 
    - It produces long and verbose code.
- Fail as soon as possible.

# Code Normalization

```Java
final class Point {

}
```

The if is too far away from the else.

Simply invert the if.

```Java
if(!(o instanceof Point p)) { return false; }
return x == p.x && y == p.y;
```

# Becoming a better programmer

- Stop writing code to just make it work.
- The cod should be simple, compact , and safe as possible.

1. Re-learn recursion with dynamic dispatch.
2. Re-learn.
