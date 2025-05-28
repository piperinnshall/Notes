# COMP 261

## 4 Sections

1. Introduction and rounding up existing knowledge
    - 4 Lectures + WAT questions
2. Parsing, making sense of text, regular expressions
    - 10 Lectures assignment and a term test covering also intro
3. Graphs, path finding, graph algorithms
    - 10 Lectures assignment and a term test
4. Compression, Coding, Fast Fourier Transform
    - 10 Lectures assignment and a term test

## Software

Building software is complex

Large systems: (SWEN 221, 225, 301)
Intricate components: (COMP 261, 361)

## Assigments

- Term test 1       20%
- Term test 2       20%
- Term test 3       20%
- WAT               04%
- Assignment 1      12%
- Assignment 2      12%
- Assignment 3      12%

Due on Fridays at mid day.

Marking (in-person) will use the nearest tutorial slot.

3 Late Days for the whole course.


START WAT [NOW](https://ecs.wgtn.ac.nz/cgi-bin/comp261-questions).

## Tutorials

Weeks: 2, 3, 4, ... 11

Slots used for tutorials and for in-person marking.

## What is a statement? What is an expression?

```java
    //  Class
public class Museum { 

    //  Method main
    public static void main(String[] a){ 

    //  Statement: variable declaration
        String          sword =         "Excalibur"; 
    //  Variable type,  Variable name,  Initialization expression

    //  Statement: variable declaration
        String bob =    "Bob";
    //                  String literal 

    //  Statement: if
    //  Condition (Binary operator expression)
        if (sword.length()      >       3){ 
    //  Method call                     Int literal
    //  Receiver: ‘sword’               ‘sword’ is an expression: a variable access
    //  Method name: ‘length’

    //  If body: command statement
    //  Expression: local variable update
            bob =                       bob + " takes " + sword;
    //  Variable name                   Update expression
    //                                  " -> Nested binary operator expression
    //  ‘+’ is a left associative binary operator
    //  bob: variable access " takes ": string literal sword: variable access
    //  Add a semicolon (;) to an expression to get the command statement.

        }

    //  Statement: command
        System.out.println(bob); 
    }
}
```
