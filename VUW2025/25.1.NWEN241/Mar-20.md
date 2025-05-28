# Reassign Ptrs using functions

```c
void assign(int **p, int *v) { *p = v; }

int main(void) {
    int i = 5, j = 10;
    int *ip;

    assign(&ip, &i); // ip = &i
    assign(&ip, &j); // ip = &j
    return 0;
}
```

find memory size of array

`len * sizeof(int)`

 Just store it somewhere
