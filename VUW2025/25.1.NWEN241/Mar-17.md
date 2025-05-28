# Pointer Types

FINISH LECTURE

Pointer variables are generally of the same size, but it is
inappropriate to assign an address of one type of pointer variable
to a different type of pointer variable

```
int V = 101;
float *P = &V; /* generally results in a warning */
```

When assigning a memory address of a variable of one type to a
pointer that points to another type, it is best to use the cast
operator to indicate the cast is intentional (this will remove the
        warning).

```
int V = 101;
float *P = (float *) &V;
/* Casts int address to float * */
```

## Void pointer

A void * is considered to be a general pointer, it can point to
any type of pointer variable

No cast is needed to assign an address to a void * or from a
void * to another pointer type

```
int V = 101;
void *G = &V; /* No warning */
float *P = G; /* No warning, still unsafe */
```

## Struct pointer

```structptr.c
typedef struct {
    char name [20];
    int student_id;
    int age;
} StudentInfo;
StudentInfo s = { "John Doe", 12345, 20};
StudentInfo *sp = &s;
```

We can reference a component of a structure pointer by the
indirect component selection operator, which is a ->, e.g.

```select.c
strcpy(sp->name, "John Smith");
sp->age = 18;
printf("%s is in age %d\n", sp->name, sp->age);
```

The indirect component selection operator has level 1 priority in
the operator precedence

## Recap: Usage of Pointers

1) Provide an alternative means of accessing information stored in
arrays
2) Provide an alternative (and more efficient) means of passing
parameters to functions
3) Enable dynamic data structures, that are built up from blocks of
memory allocated from the heap at run time

## Call by reference

Call by Reference for Efficiency 

Recall: When a structure variable is passed as an input argument to a function, all its
component values are copied into the local structure variable

Passing entire copy of a structure can be inefficient, especially for large structs

For efficiency, pass a copy of the address of structure to function

This can be done using pointer to struct as function parameter

```callbyref.c
typedef struct student_info {
    char name[40];
    int student_id;
    int age;
} StudentInfo;

void print_student(StudentInfo s)
{
    printf("Name: %s\n", s.name);
    printf("Student ID: %d\n", s.id);
    printf("Age: %d\n", s.age);
}

StudentInfo s1 = {"John", 12345, 20};
print_student(s1);
```

Doesn't make a copy

```callbyref2.c
typedef struct student_info {
    char name[40];
    int student_id;
    int age;
} StudentInfo;
void print_student(StudentInfo *s)
{
    printf("Name: %s\n", s->name);
    printf("Student ID: %d\n", s->id);
    printf("Age: %d\n", s->age);
}

StudentInfo s1 = {"John", 12345, 20};
print_student(&s1);
```

```callbyref3.c
typedef struct student_info {
    char name[40];
    int student_id;
    int age;
} StudentInfo;
void print_student(const StudentInfo *s)
{
    printf("Name: %s\n", s->name);
    printf("Student ID: %d\n", s->id);
    printf("Age: %d\n", s->age);

    s->age = 1000; // compiler will not allow this
}
```

## Function returning a pointer

```ptrfun.c
float *find_max(float A[], int N)
{
    int i;
    float *the_max = &(A[0]);
    for (i = 1; i < N; i++)
        if (A[i] > *the_max) the_max = &(A[i]);
    return the_max;
}
int main(void)
{
    float scores[5] = {10.0, 8.0, 5.5, 2.0, 4.1};
    float *max_score;
    max_score = find_max(scores, 5);
    printf("%.1f\n",*max_score);
    return 0;
}
```



