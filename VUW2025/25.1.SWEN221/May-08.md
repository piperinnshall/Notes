# Lambdas with mutations

free from streams.

List / Set / Map.

We have seen many of their operations in the first year.

Now, we can see more interesting operations, that often use Lambdas!

## .forEach

You can use directly on collections

Just iterate on the elements one at a time

For sets and maps: the iteration order is undefined

For maps: you get both keys and values

```java
//example for Set.forEach: note the order is arbitrary
void printBookTitles(Set<Book> books) {
  books.forEach(book-> System.out.println(book.title()));
}
//example for Map.forEach:
//A parking lot map where keys are slot IDs and values are Cars.
//We want to print out all cars' license plate numbers.
void printLicensePlates(Map<Integer,Car> parkingLot) {
  parkingLot.forEach((slotId, car)->
      System.out.println("Slot " + slotId + ": " + car.plate()));
}
```

## .removeIf

Removes an element if it satisfy a predicate

Much better then .remove(Object o)

We can remove based on any predicate instead of just .equals(Object)

For mutable array lists

```java
//example for List.removeIf
void removeTempEmails(ArrayList<String> emails){
  emails.removeIf(email -> email.endsWith("@spam4.me"));
}
//example for Set.removeIf
void keepActiveUsers(HashSet<User> users){
  users.removeIf(u-> !u.active());
}
//example for Set.removeIf on HashMap
void removeBoomers(HashMap<String, Integer> nameToAge){
  nameToAge.entrySet().removeIf(e-> e.getValue() >= 60);
  // Removes entries from the map!
}
//removing/adding elements from a collection while iterating over it
//usually triggers ConcurrentModificationException
//removeIf of course does not.
```

A lambda is an object. It must have a type.

A lambda is an anonymous type that implements predicate.

# .replaceAll

Like a .map, but in place.

Replace all the values with the result of an operation

- We have it on Lists and on Maps, but not on Sets:
  - because the set does not accept repetitions
  - What would happen if we have a set with [1,2,3] and we map to n->n/2?

```java
//example for List.replaceAll
void increasePrices(List<Double> prices) {
  prices.replaceAll(oldPrice -> oldPrice * 1.10);
}
//example for Map.replaceAll
//Imagine tracking the number of times certain events happened.
//At the end of the month, you want to reset all counts to zero.
void resetEventCounts(Map<String, Integer> eventCounts) {
  eventCounts.replaceAll((event, oldCount)-> 0);
}
```


## .merge(key, val, whatIfPresent)

Only for Maps

Consider map.put(key,val)

It adds an entry into the map. If the was an entry for ‘key’, the value is overridden.

Can we have some custom behavior instead?

- This is what .merge is doing:
- It is a richer .put that takes a lambda with a way to ‘merge’ the old value with the new value.

```java
/example for Map.merge
//We have a map saving the max score of some players.
//We update the map with a new score
void updateScore(Map<String,Integer> playerScores, String name, int newScore){
  playerScores.merge(name, newScore, Math::max);
}
//equivalent without ::
void updateScore(Map<String,Integer> playerScores, String name, int newScore){
  playerScores.merge(name, newScore, (oldS,newS)-> Math.max(oldS, newS));
}
//Note: the order of the parameters of the lambda is important
void updateScore(Map<String,Integer> playerScores, String name, int newScore{
  playerScores.merge(name, newScore, (oldS,newS)-> {
    if(newS<0){return null;}
    return Math.max(oldS, newS);
  });
}//if the mapping returns null the entry is removed
//so updateScore(map,“bob”,-1) would remove the “bob” entry from the map.
```
