# C compilation process

## Phases of a C program

- Preprocessing
    - Modify the original program according to the directives that begin with #
        - a # is a preprocessor command
        - .h header files
    - the result is a C program with a .i suffix
- Compilation
    - Convert .i into assembly lang .s files
        - .s is an assembler file
    - Machine dependant
- Assembly
    - Translantes .i assembly into machine lang .o files
        - Object files
    - Binary
- Linking
    - Look for external object files needed by the program
    - Creates an executable object file 
        - Ready to be loaded into memory

```hello.c
#include <stdio.h>

int main(void) {

    printf("Hello World\n")

    return 0;
}
```

```bash
gcc hello.c -o hello
```

## Exercise 1

Out tonight. Due 7 March 2025 23:59. [Sumbit Here](https://apps.ecs.vuw.ac.nz/submit/NWEN241/Exercise_1).

## C lang

- Identifiers
    - Macros
        - a piece of code in a program that is replaced by the value of the macro. 
    ```Macro.c
    // C program to illustrate macros
    #include <stdio.h>
    
    // Macro definition
    #define LIMIT 5
    
    int main()
    {
        // Print the value of macro defined
        printf("The value of LIMIT" " is %d", LIMIT);
    
        return 0;
    }
    ```
    - Variables
    - Functions
    - Structs
    - Unions
    - Other entities

    - Rules
        - Cannot use $
        - must use a letter to start identifiers
            - (_) can be used

- Data types        Size (Bytes)
    - char          1 
        - unsigned char: 0 to 255
        - signed char: 128 to 127
    - short         Machine-Dependant
    - int           Machine-Dependant
    - long          Machine-Dependant
    - long long     Machine-Dependant
    - float         Machine-Dependant
    - double        Machine-Dependant
    - long double   Machine-Dependant

    - Data type size
        - sizeof()
        - Rules
            - sizeof(char) == 1
            - sizeof(char)
            - sizeof(long)
            - sizeof(float) <= sizeof()
    - signed
    - unsigned

- Declaration
    ```init.c
    int i = 0, j = 1, k = 2;
    char c = 'A';
    float f = 1.25;
    ```
    - Possible initializers
        - constant
        - expression
    - const procesor 
    - #define pre-processor
        - Symbolic constants
- Integer literals
    - 12345     int
    - 12345u    uint
    - 0xbeef    hexadecimal
    - 081       octal (invalid)
    - 0x123uu   (invalid)
- Floating point 
    - 3.1415
    - 3.1415e-4
    - 3.1415e-4L
- Char literals
    - 'A'
    - '\t'
    - 'Aa'
    - '\z'      (invalid)
