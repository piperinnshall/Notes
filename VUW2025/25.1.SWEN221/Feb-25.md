# SWEN 221

Marco Servetto

Craig Anslow

## A very hard course

The hardest course yet?

True OO, A lot of actual code.

## Assingments

3 Slip days.

Late penalty 20% per day, max 5 days.

If you cannot get perfection you get 0.

### Grades 

- WAT               05%         Due across the course
- Assignments       05% * 3     Due weeks 3, 7, 10
- Labs              01% * 8     Weeks 2, 3, 4, .. 11
- Pre term test     02%         Lab week 2
- Term test 1       14%         Wed 19th March
- Term test 2       14%         Thu 10 April 
- Term test 3       14%         Thu 22 May 
- Term test 4       28%         Examination Period 

## Learning

The lectures are the most fundamental place where the material is introduced.

### A bad way to approach SWEN221

- Ignore the lectures at first, focus on assignments and labs
- When an assignment refers to a new concept, google it and learn independantly
- Try to pattern-match data you have found to the problem at hand
- you **will** fail

## Java

Made in 1996 and buffed over 20 years

### Code examples

```java
public static String longestString(List<String> ss) {
    if (ss.isEmpty()) { throw new IllegalArgumentException(); }
    String candidate = ss.get(0);
    for (var s : ss) {
        if (s.length() > candidate.length()) { candidate = s; }
    }
    return candidate;
}
```

What about empty lists? Error handling.

```java
if (ss.isEmpty()) { throw new IllegalArgumentException(); }
```
