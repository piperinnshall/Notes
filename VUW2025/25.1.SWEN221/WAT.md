```stack.java
interface Stack{
    int top(); Stack tail(); boolean isEmpty();
    static Stack empty() { return new Empty(); }
    default Stack push(int i) { return new Full(i, this); }
}

record Full(int top, Stack tail) implements Stack {
    public boolean isEmpty(){ return false; }    
    public String toString() { return "{" + helper(this) + "}"; }
    public String helper(Stack current) {
        return current.tail() instanceof Full ? 
            current.top() + "," + helper(current.tail()) : "" + current.top();   
    }
}
```
