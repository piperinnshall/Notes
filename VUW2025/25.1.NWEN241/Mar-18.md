# Storage classes

## Static storage Class Declaration

The static prefix must be included

```static.c
void func1(int a) { }
static int global_static;
void func2(int b) { } 
```

static is stored at a certain location.

scope:
- if you define it in a function you can only refer to it in the function.

## Register storage class

The fastest storage resides within the CPU itself in high-speed memory cells called registers.

The programmer can request the compiler to use a CPU register for storage.

`register int k;`

CPU registers are the fastest type of memory. but theres not a lot of space.

The compiler can ignore the request, in which case the storage class defaults to auto.

A register variable is local to the block which contains it.

Memory space for program code includes space for machine language code and data.

Text / Code Segment Contains program’s machine code.

Data spread over:
- Data Segment - Fixed space for global variables and constants
- Stack Segment - For temporary data, e.g., local variables in a function; expands / shrinks as program runs
- Heap Segment – For dynamically allocated memory; expands / shrinks as program runs

### Layout 

Where are auto, static, and extern variables stored?

- Auto: Stack segment.
- Static, Extern: Data segment.

# Dynamic memory allocation

When running your program you do not have to define all your variables at the start.

Dynamic memory management is the solution

- calloc()
- malloc()
- realloc()
- free()

## Pointer recap

1) Provide an alternative means of accessing information stored in
arrays
2) Provide an alternative (and more efficient) means of passing
parameters to functions
3) Enable dynamic data structures, that are built up from blocks of
memory allocated from the heap at run time

## Lifetime recap

At the start of a program the static varables are allocated.

The automatic ones only appear at the start of a block.

The dynamic ones need explicit allocation and deallocation.

## Why allocate memory dynamically

It may not be possible to know ahead of time the space needed by a variable (e.g., array) for storing data.

If predefined size is small, it may not be enough space to hold data, resulting in program failure.

If predefined size is big, most of the space will not be used causing waste or inefficiency.

## Approach

Program has routines allowing user to request some amount of memory,
the user then uses this memory, and returns it when they are done.

Memory is allocated in the Heap Segment.

- calloc - allocate array of memory.
- malloc - allocate a single block of memory.
- realloc – extend or reduce the amount of space allocated previously.
- free - free up a piece of memory that is no longer needed.

> [!warning] 
> Memory allocated dynamically does not go away at the
> end of functions, you MUST explicitly free it up

### Calloc

Function prototype:

`void *calloc(size_t num, size_t esize)`

size_t – special type used to indicate sizes, unsigned int.

num – number of elements to be allocated in the array.

esize – size (in bytes) of a single element to be allocated.
- to get the correct value, use `sizeof(<type>)`
- memory of size num*esize is allocated

returns the address of the 1st byte of this memory.

If not enough memory is available, calloc returns null.

```example.c
float *nums;
int a_size;
int idx;
printf("Read how many numbers:");
scanf("%d",&a_size);
nums = (float *)calloc(a_size, sizeof(float));
/* nums is now an array of floats of size a_size */
for (idx = 0; idx < a_size; idx++) {
    printf("Please enter number %d: ",idx+1);
    scanf("%f", nums+idx); /* read in the floats */
}
/* Calculate average, etc. */
```

above code does not null check.

```null.c
if(nums == NULL) {
    /* exit or do some other stuff */
}
```

### Free

Memory at location pointed by ptr is released (so that it could be used again).

Program keeps track of each piece of memory allocated by where that memory starts.

If we free a piece of memory allocated with calloc, the entire array is freed (released).

Undefined behaviour if we pass as address to free an address of something that was not allocated dynamically (or has already been freed).

```free.c
float *nums;
int a_size;
printf("Read how many numbers:");
scanf("%d",&a_size);
nums = (float *) calloc(a_size, sizeof(float));
/* Use array nums */
…
/* When done with nums: */
free(nums);
/* Would be an error to do it again - free(nums) */
```

### Malloc

`void *malloc(size_t esize)`

- Similar to calloc, except we use it to allocate a single block of the given size esize
- NULL returned if not enough memory available
- Memory must be released using free if no longer needed
- Following are equivalent:

`malloc(a_size*sizeof(float))` -> `calloc(a_size, sizeof(float))`

```malloc.c
float *nums;
int a_size;
int idx;
printf("Read how many numbers:");
scanf("%d",&a_size);
nums = (float *) malloc(a_size * sizeof(float));
if(nums == NULL) {
    /* exit or do some other stuff */
}
```

### Realloc

`void *realloc(void *ptr, size_t esize)`

- ptr is a pointer to a piece of memory previously dynamically allocated.
- esize is new size to allocate.
- NULL returned if reallocation fails.
- Function performs following action:
    1) allocates memory of size esize,
    2) copies the contents of the memory at ptr to the first part of the new piece of memory, and
    lastly,
    3) old block of memory is freed up
    4) Address to new piece of memory is returned

```realloc.c
float *nums;
int a_size;
nums = (float *)calloc(5, sizeof(float));
/* nums is an array of 5 floating point values */
for (a_size = 0; a_size < 5; a_size++)
nums[a_size] = 2.0 * a_size;
/* nums[0]=0.0, nums[1]=2.0, nums[2]=4.0, etc. */
nums = (float *)realloc(nums, 10*sizeof(float));
/* An array of 10 floating point values is allocated, the
   first 5 floats from the old nums are copied as the first 5
   floats of the new nums, then the old nums is released */
```

## 2d arrays

```irregular.c
float **A;
int X;

A = (float **)calloc(5, sizeof(float *));

for (X = 0; X < 5; X++)
    A[X] = (float *) calloc(X+1, sizeof(float));
```

Array with different length rows.

## Common Issues

> [!important]
> RE-READ lecture slides

## Detecting leaks

> VALGRIND

Valgrind is an open-source tool for detecting memory management and threading bugs.

For more information: [valgrind](http://valgrind.org/)
