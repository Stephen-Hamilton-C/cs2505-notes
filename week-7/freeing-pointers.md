- [Go back](../README.md)

# Freeing Pointers
Stephen Hamilton
2-28-2023

`malloc` will always return a pointer. However, the memory that is
dynamically allocated with malloc must be freed manually, as
it does not get freed when the variable using it goes out of scope.

That's where `free` comes in.
When you call `free(pointer)`, the memory that the pointer goes to is given
back to the system, or freed. **However!** This does **not** null out the
pointer. Meaning the pointer will still point to the freed memory.

This won't cause an issue unless you try to use the pointer after it is freed.
It is always good practice to null out your pointers after you free them,
like so:
```c
// Dynamically create an int array of size 3
int* memory = malloc(sizeof(int) * 3);

// We're done with the array now, we must free its memory.
// Don't forget to null out the pointer!
free(memory);
memory = NULL;
```

- [Go back](../README.md)
