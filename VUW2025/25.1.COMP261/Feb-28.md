# Lists

Currently we have used lists without knowing the inner mechanics.

A part of the collections framework.

## Twists

```twists.java
List<String> fruits= new ArrayList<>(10);
fruits.add("Apple");
fruits.add("Banana");
assert fruits.size() == 2;
fruits.add("Cherry");
assert fruits.size() == 3;
assert fruits.contains("Apple");
assert fruits.indexOf("Mango") == -1;
assert fruits.get(0).equals("Apple");
fruits.add(0, "Apricot");
assert fruits.size() == 4;
assert fruits.get(0).equals("Apricot");
assert fruits.contains("Apple");
```

List functionalities are independant of the capacity

## Merging lists

```merge.java
var fruits= List.of("Apple","Banana","Mango",/*..*/);

var calories= List.of("95","105","135",/*..*/);

var res= new ArrayList<String>(fruits.size());

assert fruits.size() == calories.size();
for (int i= 0; i < fruits.size(); i++){
    res.add(fruits.get(i) + "->" + calories.get(i));
}
```

body of the for is small enough to keep inline.

## Internals

ArrayList is implemented on top of a fixed-size array.

A new ArrayList starts with an initial capacity. 

When the internal array runs out of space, 
it is replaced with a larger array,
which involves copying all elements.

This is costly, but it is only done occasionally.

```resize.java
List<String> list= new ArrayList<>(5); // Initial capacity is 5
list.add("A");
list.add("B");
list.add("C");
list.add("D");
list.add("E");
list.add("F"); // Triggers internal array resizing
```

operations that can resize-grow the internal array include:

- `add(element)`
- `add(index, element)`
- `addAll(otherCollection)`
- `addAll(index,otherCollection)`
- `ensureCapacity(minCapacity)`

The only operation that can resize-shrink the internal array:
- `trimToSize()`

## Example implementation

Components:

- Internal array
- Size (num of elements in a list)
- Size getter

- This constructor with set arguments for initial capacity (8)
- Constructor with an argument exception when initial capacity is less than 0
- Internal array constructor with size of inital capacity

- Index checker
    - Takes an index and a size and throw an error if either parameter is out of bounds

- Ensure capacity method
    - Minimum capacity parameter
    - Miminum capacity < internal array length then return
    - New capacity
        - Internal array length is 0 then new capacity is 1 otherwise double capacity
    - Create a new array with the new capacity size and copy over the old array
        - `Arrays.copyOf(elements, newCapacity);`

- Element getter 
    - Index parameter
    - Check the index
    - Rreturn array[index]`

- Element setter
    - Index parameter
    - Element parameter
    - `array[index] = element`

- Element adder
    - Element parameter
    - Ensure capacity with size + 1
    - `elements[size++] = element;`

- Element adder at index
    - Check the index with size + 1
    - Ensure capacity with size + 1
    - `System.arraycopy(elements, index, elements, index + 1, size - index);`
    - `array[index] = element`
    - add 1 to the size
