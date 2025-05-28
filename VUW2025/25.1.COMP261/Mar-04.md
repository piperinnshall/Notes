# HashMap

We used Maps in first year. Now we begin to understand how they work.

Maps are part of the Java Collections Framework and are used to store connections between keys and values.

```map.java
Map<String,Double> prices= new HashMap<>();
prices.put("Apple", 0.99d);
prices.put("Banana", 1.49d);
assert prices.size() == 2;
prices.put("Cherry", 2.99d);
assert prices.size() == 3;
assert prices.containsKey("Apple");
assert !prices.containsKey("Mango");
assert prices.get("Apple").equals(0.99d);
prices.put("Apple", 1.09d); // Update value
assert prices.get("Apple").equals(1.09d);
assert prices.size() == 3;
```

Make sure to use f and d on floats and doubles.

getOrDefault().

Merging two maps: If the same key is contained in both maps,
we may override some value and replace it with the second
one. Thus, order of composition is important.

```merge.java
Map<String,Double> prices1= Map.of("Apple", 0.99d, "Banana", 1.49d);
Map<String,Double> prices2= Map.of("Apple", 2.29d, "Mango", 3.99d);
Map<String,Double> prices= new HashMap<>(prices1);
prices.putAll(prices2);
assert prices.get("Apple").equals(2.29d);
assert !Collections.disjoint(prices1.keySet(),prices2.keySet());
```

## Internals

Implemented on a fixed-size array.

Keys are associated to an index in the array, where the key-value pair is stored.

When the internal array is too full, it is replaced with a larger array, and all elements are rehashed and redistributed.

```impl.java
record Entry(String key, Double value){}

public class HashMapStringDouble {
    private int size= 0;
    // List of List of Entries:
    // Using Lists makes for an easier to follow code, but actual HashMaps will re-implement their auxiliary data structures internally.
    private List<List<Entry>> buckets= emptyBuckets(16);

    // List containing list. all mutable.
    private List<List<Entry>> emptyBuckets(int capacity){
        var res= new ArrayList<List<Entry>>(capacity);
        for(int i= 0; i < capacity; i++){ res.add(new ArrayList<>()); }
        return res;
    }

    // Find where key is equal to parameter key.
    private int indexOf(String key, List<Entry> b){
        for(int i= 0; i < b.size(); i++){
            if(key.equals(b.get(i).key())){ return i; }
        }
        return -1;
    }

    private int hash(String key){ return hash(key, buckets.size()); }

    // Bitwise and mod size
    // Integer.MAX_VALUE == 01111111 11111111 11111111 11111111
    // because Math.abs sucks.
    private int hash(String key, int size){
        return (key.hashCode() & Integer.MAX_VALUE) % size;
    }

    //.hash uses .hashCode, indexOf uses .equals
    private Double put(Entry e, List<List<Entry>> buckets){
        var b= buckets.get(hash(e.key()));
        int i= indexOf(e.key(), b);
        if(i == -1){ b.add(e); return null; }
        var res= b.set(i, e);//set also returns the previous value in i
        return res.value();
    }

    // 0.75 is a common default, avoids most collisions without getting too space intensive
    private static final double loadFactor= 0.75;
    private void mayResize(){
        if(size <= loadFactor * buckets.size()){ return; }
        var newCapacity= buckets.size() * 2;
        var newBuckets= emptyBuckets(newCapacity);
        for(var b: buckets){ for(var e: b){ put(e,newBuckets); } }
        buckets= newBuckets;
    }

    public int size(){ return size; }
    public boolean isEmpty(){ return size == 0; }

    public Double get(String key){
        var b= buckets.get(hash(key));
        int i= indexOf(key, b);
        if(i == -1){ return null; }
        return b.get(i).value();
    }

    public Double put(String key, Double value){
        Double res= put(new Entry(key, value), buckets);
        if(res != null){ return res; } //size not changed
        size++;
        mayResize();
        return null;
    }

    public Double remove(String key){
        var b= buckets.get(hash(key));
        int i= indexOf(key, b);
        if (i == -1){ return null; }
        size--;
        return b.remove(i).value();
    }
}
```

Don't mess with objects that are already in a HashMap! if they are in the key. for hash.get().


Map.of and Set.of are unmodifiable.

This means that they can be more memory efficient.

HashMaps and HashSet iteration orders are randomised.

## LinkedHashMap and LinkedHashSet
- Use them!
- They are as fast as HashMaps and HashSets
- They use a little bit more memory space
- They are significantly more predictable: the iteration order is fixed and is given by the element insertion order.
- If you use HashMap instead of LinkedHashMap and you assignment non
    deterministically fails to work when the tutor marks you... it is your fault.

