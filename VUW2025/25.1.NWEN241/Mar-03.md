# Macro Substitution

Recall: Can define symbolic constants using the #define pre-processor.

`#define PI 3.14`

PI is a macro, every occurrence of PI in the program will be replaced by 3.14.

Generally

`#define name replacement`

## Function-like Macro 

To define a function-like macro, just append () to the macro name.

`#define READ_CHAR() getchar()`

Can be invoked.

` int c = READ_CHAR(); `

Just like functions, function-like macros can take arguments.

Insert comma-separated parameter names between ( and ).

`#define max(X, Y) ((X) > (Y) ? (X) : (Y))`

`z = max(1, 3);     ->      z = ((1)>(3)?(1):(3));`

## Problems with Function-like Macros

`#define SQ(X) X * X`

`SQ(r1 + r2);       ->      r1 + r2 * r1 + r2;`

Solution: enclose individual variables with (), including the whole replacement text.

`#define SQ(X) ((X) * (X))`

`SQ(f());           ->      ((f()) * (f()));`

f() is invoked twice.

# Arrays

An array is a collection of data that holds a fixed number of data.

The C language places no limits on the number of dimensions in an array,
though specific implementations may.

## 1 Dimensional Array

Often referred to as a list.

0 indexed.

This is because the index in C is actually an offset from the beginning of the array.

## Declaring Arrays

Syntax for declaring a one-dimensional array:

`data_type array_name[size];`

Array size is fixed at compile-time, cannot be changed during run-time.

Arrays can be partially initialized.

`float data[4] = {22.5, 23.1};`

The rest of the values will be automatically initialized to 0.

## Loops with Arrays

```loops.c
float data[4] = {22.5, 23.1};

int idx = 0;
while(idx < 10) {
/* do something with array[idx] */
idx++;
}

for (int idx = 0; idx < 10; idx++){
/* do something with array[idx] */
}

int idx = 10;
while(idx--) {

}
```

### Off-By-One Error

The most common mistake when working with arrays in C is forgetting
that indices start at 0 and stop one less than the array size.

```offbyone.c
int data[]={1,2,3,4,5}; /* number of elements is 5 */
for (int idx = 0; idx <= 5; idx++){
/* do something with data[idx] */
}
```
## Size Of Array

The size of an array can be determined using the sizeof() operator.

It will return the number of bytes the array "occupies" in the memory.

To determine the number of elements in the array, the returned
value must be divided by the number of bytes reserved for the data type!

```size.c
int data[] = {1, 2, 3, 4, 5};
int bytes, len;

/* Print number of bytes used by array */
bytes = sizeof(data);
printf("Bytes used: %d\n", bytes);

/* Print number of elements or items in array */
len = sizeof(data)/sizeof(int);
printf("Number of items: %d\n", len);

/* To traverse array, use number of elements as limit */
for (int idx = 0; idx < len; idx++) {
/* do some stuff on element data[idx] */
}
```

## Passing Arrays to Functions

When passing an array as an argument to a function, it is passed by its
memory address (starting address of the memory area) and not its value.

```pass.c
float average(int a[]) {
    int sum = 0;
    for (int i = 0; i < 6; ++i)
        sum += a[i];
    float avg = ((float)sum / 6);
    return avg;
}
int main(void) {
    int age[] = {18,19,20,21,22,23};
    float avg = average(age);
    printf("Average age=%.2f\n", avg);
}
```

## 2 Dimensional Arrays

`arr[row][col]`

```2d.c
int two_d[2][3] = {{5, 2, 1}, {6, 7, 8}};
int two_d[2][3] = {5, 2, 1 , 6, 7, 8};
int two_d[][3] = {{5, 2, 1}, {6, 7, 8}};
```

The number of columns must be explicitly stated. The compiler will find the
appropriate amount of rows based on the initializer list.
