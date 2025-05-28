# Strings

what is a string in C?

C language does not support strings as a basic data type.

A C string is just an array that contains ASCII characters terminated by the null character '\0'.

A C string is stored in an array of chars.

strlen() in <string.h> returns the string length.

## Literal vs Variable

In C, we distinguish between string literals and string variables.

- A string literal refers to the string constant value which is stored in the read-only memory area of the program.
- A string variable refers to a string that is stored in an array which can be modified.

- Literal 
    - Enclosed in "double quotes" and can conatain char literals (plain and escape chars).
    - Can broken up into multiple lines (each line ends with \) or separated by whitespaces.
    - String literals may contain as few as one or even zero characters.
    - Do not confuse a single-character string literal, e.g. "A" with a character constant, 'A'.
        - The former is actually two characters, because of the null- terminator stored at the end.
    - An empty string, "", consists of only the null-terminator, and is
        considered to have a string length of zero, because the null-
        terminator does not count when determining string lengths.
    - String literals are passed to functions as pointers to a stored string. 
        For example, given the statement: `printf("Hello world!\n");`
        - The string literal "Hello world!\n" will be stored somewhere in memory, and the address will be passed to printf().
        - The first argument to printf() is actually defined as a char *

Use strcopy!! 
