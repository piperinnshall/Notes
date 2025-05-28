# Structures

REWATCH

A struct is a derived data type composed of members that are each basic or derived data types.

Syntax of the structure type declaration:

```
struct structure_tag {
    type1 member1;
    type2 member2;
    ...
} variable_list;
```

- structure_tag specifies the name of the structure.
- structure_tag and variable_list are optional.
- If structure_tag is not specified, variable_list should be specified;
otherwise, there is no way to declare variables using the unnamed structure type.

It is possible to initialize a struct at declaration.

```
typedef struct {
    char name [20];
    int student_id;
    int age;
} StudentInfo;
StudentInfo current_student =
{ "John Doe", 12345, 18 };
```

- Order of initializer values should follow order of declaration.

Partial initialization is also possible:

 ```
 typedef struct {
     char name [20];
     int student_id;
     int age;
 } StudentInfo;
StudentInfo current_student =
{"John Doe", 12345 };
```

- Remaining fields will be set to 0.

```
typedef struct {
    char name [20];
    int student_id;
    int age;
} StudentInfo;
StudentInfo s1 = { .age = 18, .name = "John Doe" };
// or StudentInfo s1 = { age: 18, name: "John Doe" };
```

## Accessing and Manipulating structs.

- We can reference a component of a structure by the direct
component selection operator, which is a period, e.g.

```
strcpy(student1.name, "John Smith");
student1.age = 18;
printf("%s is in age %d\n", student1.name, student1.age);
```

- The direct component selection operator has level 1 priority in the operator precedence.
- Copying of an entire structure can be easily done by the assignment operator.

```
student2 = student1;
```

# Pointers

All information accessible to a running computer program are stored somewhere in the computer's memory.

Every memory location is identified by an address.

1000 1 memory location
1001
1002
1003
1004
1005


